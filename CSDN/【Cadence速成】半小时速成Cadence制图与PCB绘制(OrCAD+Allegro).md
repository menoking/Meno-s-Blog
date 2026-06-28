# 【Cadence速成】半小时速成Cadence制图与PCB绘制(OrCAD+Allegro)

> 原创 已于 2025-03-31 20:55:10 修改 · 粉丝可见 · 8.9k 阅读 · 104 · 157 · 本内容遵循CC 4.0 BY-SA版权协议 版权声明：本文为博主原创文章，遵循 CC 4.0 BY 版权协议，转载请附上原文出处链接和本声明。 GEO检测 · 编辑
> 文章链接：https://menoking.blog.csdn.net/article/details/142833337

## 一.初识Cadence

Cadence软件是全球的EDA设计软件巨头，拥有超过30年的计算软件专业积累。主要有 **两大部分工具组** 成，ORCAD（原理图设计工具）、Allegro（PCB设计+仿真工具)。

Cadence是公司名，allegro（俗称阿狸狗）是该公司旗下的EDA工具品牌，OrCAD是该公司收购公司的EDA工具品牌。可以参考以下理清这些工具之间的关系：

> 
> 
> - OrCAD品牌
> 
>   - 原理图工具OrCAD Capture/Capture CIS(含有元件库管理之功能)
> 
>   - 原理图仿真工具PSpice（PSpiceAD、PSpiceAA）
> 
>   - PCB Layout工具 OrCAD PCB Editor
> 
>   - 信号完整性分析工具OrCAD Signal Explorer
> 
> - Allegro SPB品牌
> 
>   - 原理图工具Design Entry CIS(与OrCAD Capture CIS完全相同)
> 
>   - Concept HDL（Cadence自有之原理图工具）
> 
>   - 原理图仿真工具Allegro AMS Simulator（即PSpiceAD、PSpiceAA）
> 
>   - PCB Layout工具 Allegro PCB Editor（有L、Performance、XL、GXL版本）
> 
>   - 信号完整性分析工具Allegro PCB SI（有L、Performance、XL、GXL版本）
> 
> 

做原理图PCB设计我们一般只使用： **OrCAD Capture CIS + Allegro PCB Editor** 

> 下载安装过程可以参照行业大佬吴川斌的博客，这里建议安装个人学习版，无需破解简单易上手： [Cadence SPB 17.4 个人学习版下载及安装说明 – 吴川斌的博客](https://www.mr-wu.cn/cadence-spb-17-4-personal-learning-edition-download-and-installation-instructions/) 

下载安装完成后应该有以下工具组：

 ![](./assets/39_1.png)

## 二.快速上手Candence

### 0.创建工程文件夹

每次新建工程前一定要先做好工程管理：

 ![](./assets/39_2.png)

### 1.绘制元件符号

打开软件 ![](./assets/39_3.png)

选择OrCADCaptureCIS

 ![](./assets/39_4.png)

初始界面如图

 ![](./assets/39_5.png)

> 从上至下分别代表：
> 
>  ![](./assets/39_6.png)
> 
> - **项目文件** 用于整体管理。
> 
> - **设计文件** 用于绘制原理图。
> 
> - **库文件** 用于存储自定义元件。
> 
> - **VHDL/Verilog文件** 用于硬件描述语言设计。
> 
> - **文本文件** 用于文档记录。
> 
> - **PSpice库文件** 用于仿真模型管理。
> 
> 

建立新工程，保存至SCH文件夹内

 ![](./assets/39_7.png)

 ![](./assets/39_8.png)

新建工程页如图

 ![](./assets/39_9.png)

初学只需要清楚1是原理图，2是元件库

 ![](./assets/39_10.png)

新建原理图库

 ![](./assets/39_11.png)

 ![](./assets/39_12.png)

右击库文件新建元件符号

 ![](./assets/39_13.png)

> 符号信息页详情如下：
> 
>  ![](./assets/39_14.png)
> 
> - **封装类型** 
> 
>   - **同质封装：** 元件的所有部分（Part）都是相同的。例如，一个包含4个相同逻辑门的IC（如74LS00，包含4个相同的NAND门）。
> 
>   - **异质封装：** 元件的各部分（Part）是不同的。例如，一个包含不同功能模块的IC（如MCU，包含CPU、RAM、GPIO等不同部分）。
> 
> 

创建一个0805的电阻元件

 ![](./assets/39_15.png)

 ![](./assets/39_16.png)

添加管脚

 ![](./assets/39_17.png)

> ![](./assets/39_18.png)
> 
> - **Shape（形状）** 
> 
>   - **Line** ：默认形状，一条直线。
> 
>   - **Clock** ：带有时钟符号的形状，用于时钟信号管脚。
> 
>   - **Dot** ：带有一个小圆点的形状，用于表示低电平有效或反相信号。
> 
>   - **Dot-Clock** ：带有时钟符号和小圆点的形状。
> 
>   - **Short** ：短直线，用于缩短管脚的长度。
> 
>   - **Zero Length** ：零长度，用于隐藏管脚的图形部分。
> 
> - **Type（类型）** **​​​​** 
> 
>   - **Passive** ：被动类型，用于无源元件（如电阻、电容）或普通信号管脚。
> 
>   - **Input** ：输入类型，用于输入信号管脚。
> 
>   - **Output** ：输出类型，用于输出信号管脚。
> 
>   - **Bidirectional** ：双向类型，用于双向信号管脚（如数据总线）。
> 
>   - **Power** ：电源类型，用于电源管脚（如 `VCC` 、 `GND` ）。
> 
>   - **Open Collector** ：开漏类型，用于开漏输出管脚。
> 
>   - **Open Emitter** ：开发射极类型，用于开发射极输出管脚。
> 
>   - **3-State** ：三态类型，用于三态输出管脚。
> 
> - **Width（宽度）** 
> 
>   - **Scalar** ：单信号管脚。
> 
>   - **Bus** ：总线管脚，用于多信号组合（如 `A[0:7]` ）。
> 
> - **Additional Options（附加选项）** 
> 
>   - **Pin# Increment for Next Pin** ：设置下一个管脚的编号增量值。
> 
>   - **Pin# Increment for Next Section** ：设置下一个部分（Section）的管脚编号增量值（适用于多部分元件）。
> 
> 

这里笔者只对管脚做简单设置

 ![](./assets/39_19.png)

最后根据管脚个数调整框的大小并添加矩形边框即可

 ![](./assets/39_20.png)

 ![](./assets/39_21.png)

右侧参数配置后保存即可

 ![](./assets/39_22.png)

### 2.绘制焊盘及过孔

#### 焊盘

选择Padstack Editor来进行焊盘的绘制

 ![](./assets/39_23.png)

新建焊盘保存至前面建立的工程文件夹PcbLib文件夹内部

 ![](./assets/39_24.png)

焊盘绘制界面

 ![](./assets/39_25.png)

> **Select padstack usage：** 
> 
> 1. **Thru Pin** ：通孔焊盘，贯穿PCB，用于通孔元件。
> 
> 2. **SMD Pin** ：表面贴装焊盘，用于SMD元件。
> 
> 3. **Via** ：过孔，连接PCB不同层。
> 
> 4. **BBVia** ：盲孔，连接外层和内层，不贯穿整个PCB。
> 
> 5. **Microvia** ：微孔，用于高密度互连。
> 
> 6. **Slot** ：槽孔，长方形或椭圆形，用于特殊元件或机械固定。
> 
> 7. **Mechanical Hole** ：机械孔，用于固定PCB或元件。
> 
> 8. **Hole Tooling** ：工具孔，用于PCB制造或组装的定位。
> 
> 9. **Mounting Hole** ：安装孔，用于固定PCB或安装散热器。
> 
> 10. **Fiducial** ：基准点，用于光学定位。
> 
> 11. **Bond Finger** ：绑定焊盘，用于芯片与PCB的金线绑定。
> 
> 12. **Die Pad** ：芯片焊盘，用于芯片封装的底部连接。
> 
> **Select pad geometry:** 
> 
> 1. **Circle** ：圆形。
> 
> 2. **Square** ：正方形。
> 
> 3. **Oblong** ：椭圆形或长方形（带圆角）。
> 
> 4. **Rectangle** ：长方形。
> 
> 5. **Rounded Rectangle** ：圆角长方形。
> 
> 6. **Chamfered Rectangle** ：切角长方形（带斜角）。
> 
> 7. **Octagon** ：八边形。
> 
> 8. **Donut** ：圆环（环形）。
> 
> 9. **n-Sided** ：n边形（自定义边数）。
> 
> 10. **Polygon** ：多边形（自定义形状）。
> 
> **一般我们只需要知道Thru Pin是插件，SMD Pin是贴片就行了。** 

笔者这里以嘉立创0805焊盘尺寸为标准，一般是长*宽

 ![](./assets/39_26.png)

切换单位至毫米

 ![](./assets/39_27.png)

设置焊盘大小

 ![](./assets/39_28.png)

> ![](./assets/39_29.png)
> 
> - **SOLDERMASK** ：控制焊盘在阻焊层的开窗，影响焊接区域。
> 
> - **PASTEMASK** ：控制焊盘在焊膏层的开窗，影响焊膏印刷。
> 
> - **FILMMASK** 和 **COVERLAY** ：通常用于柔性PCB，定义焊盘在薄膜层和覆盖层的属性。
> 
> 

顶层阻焊层长宽均设置大0.1mm

 ![](./assets/39_30.png)

总览保存即可

 ![](./assets/39_31.png)

#### 过孔

创建过孔

 ![](./assets/39_32.png)

 ![](./assets/39_33.png)

 ![](./assets/39_34.png)

 ![](./assets/39_35.png)

> 
> 
> - **Regular Pad** ：焊盘的实际形状和尺寸。
> 
> - **Thermal Pad** ：用于散热或接地的焊盘。
> 
> - **Anti Pad** ：用于隔离焊盘与铜皮的反焊盘。
> 
> - **Keep Out** ：定义焊盘周围的禁止区域。
> 
> 后面的比原大小大一点

依旧正反阻焊层

 ![](./assets/39_36.png)

完成后左上角保存

 ![](./assets/39_37.png)

### 3.绘制原理图

重新回到原理图页面单机右侧工具栏放置元件

 ![](./assets/39_38.png)

接着放置电源和地并以导线连接即可

 ![](./assets/39_39.png)

最终如下图

 ![](./assets/39_40.png)

接着双击元件进入属性界面设置其封装名称

 ![](./assets/39_41.png)

Tools选项卡中可以导出网表及BOM单

 ![](./assets/39_42.png)

### 4.绘制封装

接下来打开PCB Editor17.4选择Allegro PCB Designer

 ![](./assets/39_43.png)

 ![](./assets/39_44.png)

新建封装文件，这里选择封装符号

 ![](./assets/39_45.png)

设置焊盘路径

 ![](./assets/39_46.png)

 ![](./assets/39_47.png)

 ![](./assets/39_48.png)

添加焊盘

 ![](./assets/39_49.png)

设置图表参数

 ![](./assets/39_50.png)

设置栅格

 ![](./assets/39_51.png)

修改数量和间距 ：x轴两个，间距2mm

 ![](./assets/39_52.png)

命令行键入x -1 y 0回车后使我们放置的焊盘正好处于中心对称位置

 ![](./assets/39_53.png)

 ![](./assets/39_54.png)

快捷键F6或右键Done结束则退出放置模式

 ![](./assets/39_55.png)

接着切换到Place_Bound_Top层

 ![](./assets/39_56.png)

工具栏选择放置矩形框

 ![](./assets/39_57.png)

 ![](./assets/39_58.png)

切换到Sikscreen_Top层放置Line

 ![](./assets/39_59.png)

 ![](./assets/39_60.png)

线宽0.2，折角90度

 ![](./assets/39_61.png)

点击某个点然后命令行查看该点的坐标，输入对角坐标即可画矩形

 ![](./assets/39_62.png)

 ![](./assets/39_63.png)

再回到Assembly_Top层添加一个矩形

 ![](./assets/39_64.png)

 ![](./assets/39_65.png)

添加位号

 ![](./assets/39_66.png)

最终效果如图，保存即可

 ![](./assets/39_67.png)

### 5.绘制PCB

#### 绘制板框

仍然打开PCB Editor17.4选择Allegro PCB Designer，创建Board

 ![](./assets/39_68.png)

设置图纸单位参数

 ![](./assets/39_69.png)

选择Cross-section设置板层，可以根据自己需要设置，这里笔者保持默认

 ![](./assets/39_70.png)

 ![](./assets/39_71.png)

在Outline层画板框草图（Outline是画任何草图的图层，真正板框层是Design_Outline层）

 ![](./assets/39_72.png)

 ![](./assets/39_73.png)

绘制草图后单击Compose Shape，选择Design_Outline层并设置圆角，设置完后鼠标单机草图，右击完成即可

 ![](./assets/39_74.png)

 ![](./assets/39_75.png)

 ![](./assets/39_76.png)

接下来设置禁止布线区

 ![](./assets/39_77.png)

 ![](./assets/39_78.png)

 ![](./assets/39_79.png)

#### 导入网表

导入网表，选择之前导出网表存储的allegro文件夹即可

 ![](./assets/39_80.png)

 ![](./assets/39_81.png)

Display->Status中检查未放置器件与未连接网络均不为0/0即为导入成功

 ![](./assets/39_82.png)

打开器件管理器添加器件

 ![](./assets/39_83.png)

 ![](./assets/39_84.png)

然后就可以开始愉快的布线辣

 ![](./assets/39_85.png)

## 三.总结

本文只是简单地阐述了如何从绘制元件封装到原理图PCB的简略过程，主要是笔者的学习笔记，顺便用以帮助小白快速上手了解Cadence这款软件。

以下是笔者学习过程中的一些错误总结，望读者以往鉴来。

> ### 笔者遇到的错误合集
> 
> - Number of pins in footprint 'R0805'and instance 'R1'does not match. ![](./assets/39_86.png)
> 
> - 尤其是这几个路径一定要设置对，一定要设置为自己的PcbLib下
> 
>  ![](./assets/39_87.png)
> 
>  ![](./assets/39_88.png)
> 
> - (SPMHGE-82): Pin numbers do not match between symbol and component. Run dev_check on device file for more information.
> 
> 如遇以上引脚问题请一定要检查原理图引脚以及封装引脚数量和编号是否对应，如不对应请修改。笔者这里由于封装编号不对报错无法在PCB里放置器件。封装修改引脚按照如下步骤即可。
> 
> 
> 
>  ![](./assets/39_89.png)
> 
> 

