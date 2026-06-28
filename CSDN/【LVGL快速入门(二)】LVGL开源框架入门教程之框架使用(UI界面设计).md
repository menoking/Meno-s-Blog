# 【LVGL快速入门(二)】LVGL开源框架入门教程之框架使用(UI界面设计)

> 原创 已于 2024-10-31 15:07:46 修改 · 粉丝可见 · 7.1k 阅读 · 71 · 110 · 本内容遵循CC 4.0 BY-SA版权协议 版权声明：本文为博主原创文章，遵循 CC 4.0 BY 版权协议，转载请附上原文出处链接和本声明。 GEO检测 · 编辑
> 文章链接：https://menoking.blog.csdn.net/article/details/142915534

**目录**

[TOC]





## 零.前置篇章

本篇前置文章为 [【LVGL快速入门(一)】LVGL开源框架入门教程之框架移植](https://blog.csdn.net/2203_75993546/article/details/142684876?fromshare=blogdetail&sharetype=blogdetail&sharerId=142684876&sharerefer=PC&sharesource=2203_75993546&sharefrom=from_link) 

## 一.UI设计

介绍使用之前，我们要学习一款LVGL官方的UI设计工具SquareLine Studio，使用图形化设计方式设计出我们想要的界面，然后生成对应源文件导入工程使用。

> 详情参考这篇文章： [【学习笔记】SquareLine Studio安装教程（LVGL官方工具）-CSDN博客](https://blog.csdn.net/2203_75993546/article/details/142731854?fromshare=blogdetail&sharetype=blogdetail&sharerId=142731854&sharerefer=PC&sharesource=2203_75993546&sharefrom=from_link) 

 <img src="./assets/23_1.png" alt="" style="max-height:1080px; box-sizing:content-box;" />

另一种非官方工具GuiGuider(恩智浦开发)也可以进行UI设计：

> Gui Guider官方下载地址： [GUI Guider | NXP 半导体](https://www.nxp.com.cn/design/design-center/software/development-software/gui-guider:GUI-GUIDER) 

 <img src="./assets/23_2.png" alt="" style="max-height:1080px; box-sizing:content-box;" />

个人比较喜欢恩智浦这个工具，界面看着更简洁，而且免费。

## 二.简单测试

在while前添加以下代码来简单测试是否移植成功：

```cpp
    // 按钮
    lv_obj_t *myBtn = lv_btn_create(lv_scr_act());                               // 创建按钮; 父对象：当前活动屏幕
    lv_obj_set_pos(myBtn, 10, 10);                                               // 设置坐标
    lv_obj_set_size(myBtn, 120, 50);                                             // 设置大小
   
    // 按钮上的文本
    lv_obj_t *label_btn = lv_label_create(myBtn);                                // 创建文本标签，父对象：上面的btn按钮
    lv_obj_align(label_btn, LV_ALIGN_CENTER, 0, 0);                              // 对齐于：父对象
    lv_label_set_text(label_btn, "Test");                                        // 设置标签的文本
 
    // 独立的标签
    lv_obj_t *myLabel = lv_label_create(lv_scr_act());                           // 创建文本标签; 父对象：当前活动屏幕
    lv_label_set_text(myLabel, "Hello world!");                                  // 设置标签的文本
    lv_obj_align(myLabel, LV_ALIGN_CENTER, 0, 0);                                // 对齐于：父对象
    lv_obj_align_to(myBtn, myLabel, LV_ALIGN_OUT_TOP_MID, 0, -20);               // 对齐于：某对象
```

 <img src="./assets/23_3.png" alt="" style="max-height:867px; box-sizing:content-box;" />

可以看到一个Test按钮以及Hello world!

 <img src="./assets/23_4.jpeg" alt="" style="max-height:1200px; box-sizing:content-box;" />

> 遇到错误或者奇怪的现象可以参考： [LCD典型问题及解决方案_hx8399c-CSDN博客](https://blog.csdn.net/qq_27516841/article/details/80367434?fromshare=blogdetail&sharetype=blogdetail&sharerId=80367434&sharerefer=PC&sharesource=2203_75993546&sharefrom=from_link) 

## 三.正式开发

这里笔者使用GUI Guider来做演示。

### 1.创建工程

Create a new project来创建新工程：

 <img src="./assets/23_5.png" alt="" style="max-height:323px; box-sizing:content-box;" />

貌似只适配8.3的 框架，next下一步：

 <img src="./assets/23_6.png" alt="" style="max-height:965px; box-sizing:content-box;" />

选择设备模拟器为模板： <img src="./assets/23_7.png" alt="" style="max-height:955px; box-sizing:content-box;" />

选择空工程：

 <img src="./assets/23_8.png" alt="" style="max-height:970px; box-sizing:content-box;" />

根据自己的屏幕选择尺寸，以及自命名工程和保存路径：

 <img src="./assets/23_9.png" alt="" style="max-height:188px; box-sizing:content-box;" />

 <img src="./assets/23_10.png" alt="" style="max-height:103px; box-sizing:content-box;" />

单击Create即可创建成功： <img src="./assets/23_11.png" alt="" style="max-height:1051px; box-sizing:content-box;" />

### 2.设计界面

依次单击以下图标可以呼出组件界面： <img src="./assets/23_12.png" alt="" style="max-height:67px; box-sizing:content-box;" />

 <img src="./assets/23_13.png" alt="" style="max-height:55px; box-sizing:content-box;" />

 <img src="./assets/23_14.png" alt="" style="max-height:433px; box-sizing:content-box;" />

先添加一个容器覆盖我们的界面：

 <img src="./assets/23_15.png" alt="" style="max-height:533px; box-sizing:content-box;" />

组件中选择图片，然后导入几张图片：

 <img src="./assets/23_16.png" alt="" style="max-height:471px; box-sizing:content-box;" />

修缮一下：

 <img src="./assets/23_17.png" alt="" style="max-height:531px; box-sizing:content-box;" />

选择标签，加点文字：

 <img src="./assets/23_18.png" alt="" style="max-height:421px; box-sizing:content-box;" />

### 3.运行测试

点击右上角的三角运行无误后，即可开始移植

 <img src="./assets/23_19.png" alt="" style="max-height:997px; box-sizing:content-box;" />

 <img src="./assets/23_20.png" alt="" style="max-height:149px; box-sizing:content-box;" />

### 4.移植代码

将代码导出至指定路径：

 <img src="./assets/23_21.png" alt="" style="max-height:394px; box-sizing:content-box;" />

打开我们移植好LVGL的STM32的工程以及工程文件夹，在LVGL文件夹中创建一个guider文件夹，将guider生成的源码src文件夹全部放入（删除生成的main.c）： <img src="./assets/23_22.png" alt="" style="max-height:379px; box-sizing:content-box;" />

 <img src="./assets/23_23.png" alt="" style="max-height:246px; box-sizing:content-box;" />

工程管理中创建组并添加文件：

 <img src="./assets/23_24.png" alt="" style="max-height:572px; box-sizing:content-box;" />

魔术棒中添加头文件路径：

 <img src="./assets/23_25.png" alt="" style="max-height:306px; box-sizing:content-box;" />

打开GUI Guider导出的main.c文件，将main.c中的头文件加入到我们自己工程的头文件中：

```cpp
//Guider
#include "../generated/gui_guider.h"
#include "../generated/events_init.h"
```

 <img src="./assets/23_26.png" alt="" style="max-height:173px; box-sizing:content-box;" />

在main.c主函数上方添加全局变量：

```cpp
lv_ui guider_ui;
```

 <img src="./assets/23_27.png" alt="" style="max-height:208px; box-sizing:content-box;" />

在主函数中调用（LVGL框架初始化之后）：

```cpp
setup_ui(&guider_ui);
events_init(&guider_ui);
```

 <img src="./assets/23_28.png" alt="" style="max-height:867px; box-sizing:content-box;" />

编译成功即可。

### 5.错误解决方案

以下是笔者移植时遇到的错误总结：

> **1.error:#8：missing closing quote** 
> 
> 这个错误主要由编码错误引起，在魔术棒->C/C++->Misc Controls中添加：--locale=english
> 
> 后即可解决
> 
>  <img src="./assets/23_29.png" alt="" style="max-height:33px; box-sizing:content-box;" />
> 
> 

> 2. **画面倒置** 
> 
> 烧入成功后发现画面是旋转的或者倒置的话，可以使用LVGL自带的属性进行修改旋转
> 
> 打开lv_port_disp.c这个文件，找到 **void lv_port_disp_init(void)** 这个函数 <img src="./assets/23_30.png" alt="" style="max-height:57px; box-sizing:content-box;" />
> 
> 在 **lv_disp_drv_register(&disp_drv);** 前添加堆属性的修改即可
> 
> ```cpp
> disp_drv.sw_rotate = 1;
> disp_drv.rotated = LV_DISP_ROT_90;
> ```
> 
> 这两句是开启旋转并旋转90度，其他宏如：
> 
> **`LV_DISP_ROT_NONE` , `LV_DISP_ROT_90` , `LV_DISP_ROT_180` , `LV_DISP_ROT_270`** 
> 
> 分别可旋转不同的角度
> 
>  <img src="./assets/23_31.png" alt="" style="max-height:214px; box-sizing:content-box;" />
> 
> 

## 四.移植成功

 <img src="./assets/23_32.jpeg" alt="" style="max-height:1200px; box-sizing:content-box;" />

 <img src="./assets/23_33.jpeg" alt="" style="max-height:1200px; box-sizing:content-box;" />

哈哈很浪漫的啊！