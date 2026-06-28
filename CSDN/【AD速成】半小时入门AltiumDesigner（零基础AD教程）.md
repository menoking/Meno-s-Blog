# 【AD速成】半小时入门AltiumDesigner（零基础AD教程）

> 原创 已于 2024-11-03 20:04:24 修改 · 粉丝可见 · 3.1w 阅读 · 243 · 725 · 本内容遵循CC 4.0 BY-SA版权协议 版权声明：本文为博主原创文章，遵循 CC 4.0 BY 版权协议，转载请附上原文出处链接和本声明。 GEO检测 · 编辑
> 文章链接：https://menoking.blog.csdn.net/article/details/142792954

**目录**

[TOC]





## 一.创建工程

### 1.工程

> **文件->新的->项目** 

 ![14df78d011774c7e9e462dbab209b4dc.png](./assets/16_1.png)

> 
> 
> - PCB选择<Default>
> 
> - Project Name填入自己的工程名称
> 
> - Folder选择工程保存的路径
> 
> 

 ![fd751a329a3541919793995bae751ea8.png](./assets/16_2.png)

创建后如图：

 ![a4020f203da4488f9841d18fa343b71a.png](./assets/16_3.png)

这里的 **.prjPcb** 的文件即为AD的工程文件。

> 如果没有Project栏可以在 **视图->面板->Projects** 中勾选Projects
> 
>  ![6fec59c7203540d390d27bf74a21ec9e.png](./assets/16_4.png)
> 
> 

> **Ctrl+S保存工程** 

 ![ffd0eeb329144c77a8a790bb8f5b7872.png](./assets/16_5.png)

### 2.原理图库

> 右键工程文件 **添加...到工程->Schematic Library** 

 ![eb41c89701664cef903460f982ef3efe.png](./assets/16_6.png)

 ![66f66e6adfb049258d2af36bc75c5565.png](./assets/16_7.png)

这一步添加的是原理图库，我们该工程的所有原理图元件都存放在这里。

### 3.PCB库

> 右键工程文件 **添加...到工程->PCB Library** 

 ![004ede2c9f7e461da11ce50476772b17.png](./assets/16_8.png)

 ![8d2893e6fa054639a1ecb1d8c16eea86.png](./assets/16_9.png)

这一步添加的是PCB库，我们该工程的所有PCB元件都存放在这里。

可见，创建的两个库在菜单栏下方 ![004ec8a7b49f4302838441c2885139c1.png](./assets/16_10.png)

。

### 4.原理图

> 右键工程文件 **添加...到工程->Schematic** 

 ![6e61cbe9a84d44159fe0828424cb4a9d.png](./assets/16_11.png)

 ![a894ad33d3cb4910b49f1412d01cedeb.png](./assets/16_12.png)

这个 **.SchDoc** 就是我们的原理图文件。

### 5.PCB

> 右键工程文件 **添加...到工程->PCB** 

 ![3934025964e646b4a212afd2f1429eed.png](./assets/16_13.png)

 ![05947159f63548e0b43ec2f93b50b5ca.png](./assets/16_14.png)

这个 **.PcbDoc** 就是我们的原理图文件。

至此，我们的整个工程都创建完成：

 ![e1113a4ca2a2482691c24f86949f092e.png](./assets/16_15.png)

 ![f58ca925445a4f6b8efb6375f4997e1a.png](./assets/16_16.png)

## 二.添加元件和封装

### 1.添加元件

单击Schlib1.SchLib原理图库

 ![674aefe7847a40b190d013a8eafe9d1e.png](./assets/16_17.png)

这里是元件管理区域：

 ![f7465f25722245368a2ead94355433f9.png](./assets/16_18.png)

这里是元件属性区域：

 ![188f747d3f2141dd82df6f2c5d0813e9.png](./assets/16_19.png)

> 注意：
> 
> - Design Item ID：设计项目ID，是软件内部用于标识元件的唯一编号。即使两个元件具有相同的设计符，它们的Design Item ID也是不同的。
> 
> - Designator：设计符，是分配给电路板上每个元件的唯一标识符，通常由一个或多个字母和数字组成，如R1、C2、U3等。
> 
> - Comment：注释，通常用于提供关于元件的额外信息，如元件的详细描述、型号、参数、制造商信息等。
> 
> 

中心工具栏，右击 **线可选不同的几何画笔。** 

 ![2c417846f2b54a539f4444a18fb512ad.png](./assets/16_20.png)

我们一般选用矩形，单击画面中某个地方即可开始绘制，再次单击即绘制完成：

 ![d2e7819e843640798cbe2d173832d32a.png](./assets/16_21.png)

单击中心菜单栏 **放置管脚** 

 ![d24a81058965480f9bef0aaffa71bcb8.png](./assets/16_22.png)

放置前按 **Tab键** 可以对属性进行编辑：

 ![0977f0f3033748ed9d5b2bc223721e8b.png](./assets/16_23.png)

 ![aeaaf0e36b9b4ddf8a2813536a1ccde6.png](./assets/16_24.png)

> Designator代表管脚的序号，Name代表后面的文字。
> 
> ！！！尤其是序号Designator一定要按顺序连续，否则后面封装可能会对不上管脚！！！

点击放置（ **十字叉朝外** ）： ![8c1f94572ce04574a29095d639aede81.png](./assets/16_25.png)

稍微调整一下形状，同时修改一下名字：

 ![1197db1cd31d4c15ae25983f57fe2b9d.png](./assets/16_26.png)

 ![f9de63e64461455198eb0fe2a46a3f8e.png](./assets/16_27.png)

**Ctrl+S保存** ：

 ![2f95b140996c45aa95febaeeace09cc6.png](./assets/16_28.png)

然后回到原理图：

 ![b5e76aa133994fe9b1f99a1d8fbcb341.png](./assets/16_29.png)

**单击Panels->Components，选择刚建立的原理图库** 唤出原理图库

 ![4fa9741a58a148cab87936519d72e1fb.png](./assets/16_30.png)

 ![14a1bab964bc493a8535089ce43c6d8f.png](./assets/16_31.png)

就可以看到刚刚绘制的元件了：

 ![eb4e4398c4a14ab082147a519b2068c5.png](./assets/16_32.png)

### 2.添加封装

单击进入PCB封装库：

 ![3a828fa836bb425a959b352fbbceb779.png](./assets/16_33.png)

左侧栏位下方可以切换菜单或者单击Panels，切换到PCBLibrary：

 ![8dcfc61d517e43ca9a53d235b5db799c.png](./assets/16_34.png)

 ![a969cde606fa4f7cbdd8b9503a5cd14e.png](./assets/16_35.png)

双击封装可以设置其属性：

 ![b10704c5c68b43d4a12796e476c4a9b5.png](./assets/16_36.png)

 ![3a237911c1854e17835d03049551bd6a.png](./assets/16_37.png)

单击放置焊盘:

 ![cb694d64e69048ec8b388afc149c0dfc.png](./assets/16_38.png)

同样按住Tab可以修改属性，或放置后双击也可在属性栏修改属性：

 ![53e27590867a47e5815aa2711d46461b.png](./assets/16_39.png)

> 属性主要关注这些，依次是：编号，层级，形状，大小。
> 
> ！！！尤其注意这里的编号要和想要关联的原理图的管脚编号一致！！！

 ![2364f0c2d50b41ed84be64e57cffe328.png](./assets/16_40.png)

 ![0ba1188dd296463fabf7a47b435ca9ff.png](./assets/16_41.png)

 ![858d59ce3a644c779e9219d52b479902.png](./assets/16_42.png)

放置好后，接着开始添加丝印，单击线径，然后改变层级为Top Overlay（顶层丝印层）:

 ![ce4d323b5f064b51b703788c1dd9861c.png](./assets/16_43.png)

绘制丝印：

 ![f3c197fa7e674787bc54bae27b91a73a.png](./assets/16_44.png)

Ctrl+S保存：

 ![14b22b97d0fe495d84ec0f39eeab55b6.png](./assets/16_45.png)

### 3.关联封装

切换到原理图库，右击原理图元件->模型管理器：

 ![9377bc8c8c914d4eb93a4884efb8268b.png](./assets/16_46.png)

单击元件，选择Add Footprint：

 ![9fb21f4fb5f3499891d961547c8c0ef3.png](./assets/16_47.png)

浏览并选择你的封装库，选择刚刚绘制的封装，一路确定：

 ![d650033cab3245d49436d2710874eff1.png](./assets/16_48.png)

 ![9d867cabe33642a6b4076cdc28a9c9eb.png](./assets/16_49.png)

成功关联封装！保存一下！

### 4.放置器件

回到原理图中，单击Components中绘制的元件，拖入原理图中放置：

 ![82358d24efb34a8388a737e9df34e883.png](./assets/16_50.png)

Ctrl+S保存：

 ![0bf94e2939074473a65be47f47802b64.png](./assets/16_51.png)

### 5.更新至PCB

设计->Updata PCB ...

 ![e22abf1676f44e0692a0396098bdf149.png](./assets/16_52.png)

执行变更：

 ![3807b1ba90bb4f2086ef226b83ddef89.png](./assets/16_53.png)

进入PCB中查看：

 ![5fa770b253fa4780844b8939808928d0.png](./assets/16_54.png)

我们可以删除红框：

 ![9026510c0e884fc5823903507581ee43.png](./assets/16_55.png)

底部切换到机械层，点击线径绘制板框，左键框选住所有内容， **设计->板子形状->按照选择对象定义** 。

 ![cc67af5155f14762bb38ec2180b42e1f.png](./assets/16_56.png)

 ![ddb729205c6e43678b72ae0591afdfcd.png](./assets/16_57.png)

编辑->原点->设置。建议将原点设置在板框左下角。

 ![57926e9ebab04a3d9d4fcd6ce67333c9.png](./assets/16_58.png)

 ![0ac6618cf5f243fdacbb208b23182b68.png](./assets/16_59.png)

至此一个PCB就完成了。

## 三.总结

以上只是AD最基本的用法，其他更复杂更有趣的用法只能靠平时的累以及看别的帖子里的详细介绍了，祝各位早日学会使用AD，成为一名合格的PCBLayer！