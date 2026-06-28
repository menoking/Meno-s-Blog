# 【总结】ubuntu下安装程序的方式

> 原创 已于 2024-10-13 19:15:24 修改 · 粉丝可见 · 621 阅读 · 5 · 10 · 本内容遵循CC 4.0 BY-SA版权协议 版权声明：本文为博主原创文章，遵循 CC 4.0 BY 版权协议，转载请附上原文出处链接和本声明。 GEO检测 · 编辑
> 文章链接：https://menoking.blog.csdn.net/article/details/142320332

## 一.apt包管理

- apt-get install xxx 安装xxx  。如果带有参数，那么-d 表示仅下载 ，-f 表示强制安装

- apt-get remove xxx 卸载xxx

- apt-get update 更新软件信息数据库

- apt-get upgrade 进行系统升级

- apt-cache search 搜索软件包

> ```
> 当使用sudo apt-get install xxx安装程序时，The following extra packages will be installed:后表示需要安装的依赖
> ```

## 二.dpkg包管理

| dpkg -i package.deb | 安装包 |
|:---:|:---:|
| dpkg -r package | 删除包 |
| dpkg -P package | 删除包（包括配置文件） |
| dpkg -L package | 列出与该包关联的文件 |
| dpkg -l package | 显示该包的版本 |
| dpkg –unpack package.deb | 解开 deb 包的内容 |
| dpkg -S keyword | 搜索所属的包内容 |
| dpkg -l | 列出当前已安装的包 |
| dpkg -c package.deb | 列出 deb 包的内容 |
| dpkg –configure package | 配置包 |


## 三.源代码编译安装

首先要使用

```csharp
sudo apt-get install build-essential
```

这个命令安装build-essentia。

安装分为三步：

1. 配置：这是编译源代码的第一步，通过 `./configure` 命令完成。执行此步以便为编译源代码作准备。常用的选项有 `--` prefix=PREFIX，用以指定程序的安装位置。更多的选项可通过 `--` help 查询。也有某些程序无需执行此步。

2. 编译：一旦配置通过，可即刻使用 `make` 指令来执行源代码的编译过程。视软件的具体情况而定，编译所需的时间也各有差异，我们所要做的就是耐心等候和静观其变。此步虽然仅下简单的指令，但有时候所遇到的问题却十分复杂。较常碰到的情形是程序编译到中途却无法圆满结束。此时，需要根据出错提示分析以便找到应对之策。

3. 安装：如果编译没有问题，那么执行 `sudo make install` 就可以将程序安装到系统中了。

例如：

> //1.解压缩
> tar -zxf nagios-4.0.2.tar.gz
> //2.进入目录
> cd nagios-4.0.2
> //3.配置
> ./configure --prefix=/usr/local/nagios
> //4.编译
> make all
> //5.安装
> make install && make install-init && make install-commandmode && make install-config

