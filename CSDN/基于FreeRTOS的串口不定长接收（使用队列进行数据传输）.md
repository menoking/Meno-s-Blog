# 基于FreeRTOS的串口不定长接收（使用队列进行数据传输）

> 原创 已于 2025-07-13 22:52:30 修改 · 粉丝可见 · 4.3k 阅读 · 17 · 44 · 本内容遵循CC 4.0 BY-SA版权协议 版权声明：本文为博主原创文章，遵循 CC 4.0 BY 版权协议，转载请附上原文出处链接和本声明。 GEO检测 · 编辑
> 文章链接：https://menoking.blog.csdn.net/article/details/138390307

**目录** 

[一.基本收发](#%E4%B8%80.%E5%9F%BA%E6%9C%AC%E6%94%B6%E5%8F%91) 

[二.测试部分](#%E4%BA%8C.%E6%B5%8B%E8%AF%95%E9%83%A8%E5%88%86%C2%A0) 

[三.实验现象](#%E4%B8%89.%E5%AE%9E%E9%AA%8C%E7%8E%B0%E8%B1%A1%C2%A0) 

---

2024.5.2日五一假期埋头苦战串口收发数据

以下为心得备忘：

## 一.基本收发

首先是仿照江科大标准库移植的串口基本收发函数，进行了一些改写，能够在单字节以及数据包之间进行模式转换：

```cpp
uint8_t Receive_Mode = 0;//接收模式：单字节或数据包
uint8_t Receive_State;//状态机变量
uint8_t Receive_Byte[1],Receive_ITFlag;//接收单字节数据；接收标志位//!!!这里单字节接收缓冲一定要用数组形式!!!
uint8_t Receive_PocketData[Receive_Pocket_Max_Len] = {0};//接收数据包数组
uint16_t Receive_Pocket_Index = 0;//接收指向
 
extern QueueHandle_t xQueueHandle_Usart3;//队列句柄
 
void Serial_ChangeMode(Serial_Mode Mode)
{
	Receive_Mode = (uint8_t)Mode;
}
 
void Serial_SendByte(uint8_t Byte)
{
	//这里非阻塞发送暂时不能用，否则数据会传输错误，原因暂不明
	//HAL_UART_Transmit_IT(&huart3,&Byte,1);
	HAL_UART_Transmit(&huart3,&Byte,1,HAL_MAX_DELAY);
}
 
void Serial_SendString(uint8_t *String)
{
	HAL_UART_Transmit(&huart3,String,strlen((const char*)String),HAL_MAX_DELAY);
}
 
void Serial_SendArray(uint8_t* ArrayData,uint16_t Length)
{
	HAL_UART_Transmit(&huart3,ArrayData,Length,HAL_MAX_DELAY);
}
 
void Serical_SendPocket(uint8_t* PocketData)
{
	Serial_SendByte(0xFD);
	Serial_SendArray(PocketData,Receive_Pocket_Index);
	Serial_SendByte(0xFE);
	Serial_SendByte(0xFF);
}
//接收单字节和数据包标志位
uint8_t Serial_GetReceiveFlag(void)
{
	if(Receive_ITFlag == 1)
	{
		Receive_ITFlag = 0;
		return 1;
	}
	return 0;
}
 
//单字节数据
uint8_t Serial_ReceiveByte(void)
{
	return Receive_Byte[0];
}
//数据包数据
void Serial_ReceivePocket(uint8_t *PocketArray)
{
	uint8_t i = 0;
	Receive_GetDataState = 0;
	for (i = 0; Receive_PocketData[i] != '\0'; i ++)
	{
		PocketArray[i] = Receive_PocketData[i];
	}
}
//数据包长度
uint16_t Serial_GetPocketLength(void)
{
	return Receive_Pocket_Index;
}
```

下面是中断回调函数：

注意中断回调函数中一定要使用中断安全API：xQueueSendToBackFromISR

否则不能正确接收数据或者程序卡死

```cpp
void HAL_UART_RxCpltCallback(UART_HandleTypeDef *huart)
{
	if(huart->Instance == USART3)
	{
		switch(Receive_Mode)
		{
		case 0:
			Receive_ITFlag = 1;
			xQueueSendToBackFromISR(xQueueHandle_Usart3,&Receive_Byte,0);
		break;
		case 1:
				if(Receive_State == 0)
				{
					if (Receive_Byte[0] == 0xFD)
					{
						Receive_Pocket_Index = 0;
						Receive_State = 1;
					}
				}
				else if(Receive_State == 1)
				{
					 if(Receive_Byte[0] == 0xFE)
						Receive_State = 2;
					 else
					 {
						Receive_PocketData[Receive_Pocket_Index] = Receive_Byte[0];
						Receive_Pocket_Index++;
					 }
					 if(Receive_Pocket_Index >= Receive_Pocket_Max_Len)
					 {
						Receive_ITFlag = 1;
						Receive_PocketData[Receive_Pocket_Index] = '\0';
						Receive_State = 0;
					 }
					 
				}
				else if(Receive_State == 2)
				{
					if(Receive_Byte[0] == 0xFF)
					{
						Receive_ITFlag = 1;
						Receive_PocketData[Receive_Pocket_Index] = '\0';
						Receive_State = 0;
						xQueueSendToBackFromISR(xQueueHandle_Usart3,&Receive_PocketData,0);
					}
				}
		break;
		}
		HAL_UART_Receive_IT(&huart3,Receive_Byte,1);//使能中断函数，每次使用完就要调用
	}
}
```

## 二.测试部分

以下是在freertos.c中写的测试代码：

这里是一些定义声明：

```cpp
/**********串口相关变量************/
extern uint8_t Receive_Byte[1];
BaseType_t ret;
 
/**********************************/
 
/**********任务句柄声明************/
TaskHandle_t  xLedTaskHandle;
/**********************************/
 
/**********队列句柄声明************/
QueueHandle_t xQueueHandle_Usart3;//串口3队列句柄
/**********************************/
```

这里是初始化代码，删除了部分不重要的注释：

这里的队列单元大小要注意，必须设置为sizeof(uint8_t*)，在stm32这种32位MCU中指针的大小通常是4个字节，即32位，所以这里要把队列单元设置为指针的大小，代表存储地址，

如果这里设置的不对，那么接收的数据就会出现丢包，数据错误。

```cpp
void MX_FREERTOS_Init(void) 
{
	Serial_ChangeMode(Pocket);
	HAL_UART_Receive_IT(&huart3,Receive_Byte,1);//启动串口3
 
    xQueueHandle_Usart3 = xQueueCreate(128,sizeof(uint8_t*));
 
    ret = xTaskCreate(Led_Task,"Led_Task",512,NULL,24,&xLedTaskHandle);
}
```

这里是测试函数：

这里非常重要，因为在串口模块中我们是将数据的地址写入队列中的，故这里接收必须使用二重指针，*Signal来接收队列里储存的地址，将地址取出后解引**Signal即可读取数据

```cpp
void Led_Task(void *params)
{
	uint8_t **Signal = 0;//这里必须是二维指针
	while(1)
	{
		if (xQueueReceive(xQueueHandle_Usart3,*Signal, portMAX_DELAY) == pdPASS)
		{
			//Serial_SendByte(**Signal);
			Serical_SendPocket(*Signal);//传入字符或字符串地址
			//Led_SetState((Led_State)(**Signal));
			
		}
		vTaskDelay(pdMS_TO_TICKS(1000));
	}
}
```

## 三.实验现象

<div style="text-align:center;">以下是实验现象：<img src="https://i-blog.csdnimg.cn/blog_migrate/a4f9bebd6bf9427a14c50d2f33f85239.png"></div>

<div style="text-align:center;">&nbsp;</div>

这里单字节和不定长数据包都能实现相应功能，就只展示数据包的接收过程了。