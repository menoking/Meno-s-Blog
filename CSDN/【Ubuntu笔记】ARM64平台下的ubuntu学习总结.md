# 【Ubuntu笔记】ARM64平台下的ubuntu学习总结

> 原创 已于 2024-10-11 11:22:16 修改 · 粉丝可见 · 2.1k 阅读 · 6 · 7 · 本内容遵循CC 4.0 BY-SA版权协议 版权声明：本文为博主原创文章，遵循 CC 4.0 BY 版权协议，转载请附上原文出处链接和本声明。 GEO检测 · 编辑
> 文章链接：https://menoking.blog.csdn.net/article/details/142208962

**目录** 

[一.换源问题](#%E4%B8%80.%E6%8D%A2%E6%BA%90%E9%97%AE%E9%A2%98) 

[二.了解dpkg和apt](#%E4%BA%8C.%E4%BA%86%E8%A7%A3dpkg%E5%92%8Capt) 

---



## 一.换源问题

> 注意：
> 
> 感谢鱼香大大开源的一键ROS工具箱
> 
> 链接：wget http://fishros.com/install -O fishros && . fishros
> 
> 亲测ARM64已成功！
> 
> 该工具箱可不仅可进行一键ROS还可以进行一键比对换源等很多黑科技，小白福音！！！
> 
> 这里再次感谢大大开源！@鱼香ROS
> 
> 下面为传统换源方法：

初学ubuntu时要学会的第一件事就是换源，主要是因为在Linux系系统下避免不了频繁的对软件源进行操作，故将源地址换为国内镜像源加快学习开发速度。

我们要明确ubuntu24.04之后的软件源配置文件在以下位置

```cobol
/etc/apt/sources.list.d/ubuntu.sources
```

---

安装vim编辑器

```csharp
sudo apt-get -y install vim
```

首先进行备份

```cobol
sudo cp /etc/apt/sources.list.d/ubuntu.sources  /etc/apt/sources.list.d/ubuntu.sources.bak
```

然后使用vim编辑器进入配置文件

```cobol
sudo vim /etc/apt/sources.list.d/ubuntu.sources
```

将官方文件全部注释之后在文件最末端写入以下配置信息（基于arm64下的清华源）

（按i进入插入模式，完成注释以及修改后按Esc退出到命令模式，最后使用“:wq”命令保存退出）

```cobol
Types: deb
URIs: http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/
Suites: noble noble-updates noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

添加完成后类似于下面的样子

```cobol
#Types: deb
#URIs: http://ports.ubuntu.com/ubuntu-ports
#Suites: noble noble-updates noble-backports
#Components: main universe restricted multiverse
#Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
 
## Ubuntu security updates. Aside from URIs and Suites,
## this should mirror your choices in the previous section.
#Types: deb
#URIs: http://ports.ubuntu.com/ubuntu-ports
#Suites: noble-security
#Components: main universe restricted multiverse
#Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
 
Types: deb
URIs: http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/
Suites: noble noble-updates noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
 
```

然后进入

```cobol
sudo vim /etc/apt/sources.list
```

把其中的官方源注释掉，否则会重复配置!

最后执行更新软件源

```sql
sudo apt-get update
sudo apt-get upgrade
```

## 二.了解dpkg和apt

> dpkg是Debian系Linux系统下默认的deb软件包管理工具，是Debian软件包管理器的基础，它是Debian系统的一个核心组件。
> 
> apt则是基于dpkg构建的一个用于处理复杂依赖关系的高级包管理工具。
> 
> ---
> 
> **dpkg 主要是用来安装已经下载到本地的 deb 软件包，或者对已经安装好的软件进行管理。而 apt-get 可以直接从远程的软件仓库里下载安装软件。** 

> 注意：这里要区分apt与apt-get。
> 
> 我们要知道Linux基础的包管理命令分别由apt-get、apt-cache 和 apt-config 这三条命令来实现。为了精简操作，我们集成了这些命令中最常用的一些操作到apt中。但要注意的是它并不能完全向下兼容 apt-get 命令。
> 
> ***即，apt=*** ***来自*** ***apt-get*** ***和*** ***apt-cache以及* apt-config** ***的常用功能选项。*** 
> 
> | apt 命令 | 取代的命令 | 命令的功能 |
> |:---:|:---:|:---:|
> | apt install | apt-get install | 安装软件包 |
> | apt remove | apt-get remove | 移除软件包 |
> | apt purge | apt-get purge | 移除软件包及配置文件 |
> | apt update | apt-get update | 刷新存储库索引 |
> | apt upgrade | apt-get upgrade | 升级所有可升级的软件包 |
> | apt autoremove | apt-get autoremove | 自动删除不需要的包 |
> | apt full-upgrade | apt-get dist-upgrade | 在升级软件包时自动处理依赖关系 |
> | apt search | apt-cache search | 搜索应用程序 |
> | apt show | apt-cache show | 显示装细节 |
> 
> 
> | 新的apt命令 | 命令的功能 |
> |:---:|:---:|
> | apt list | 列出包含条件的包（已安装，可升级等） |
> | apt edit-sources | 编辑源列表 |

---

如有疏漏错误之处，感谢指正 ！

未完待续... ...