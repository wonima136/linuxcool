---



title: "Linux中有多种检查端口的方法，本文将介绍两种(组图)"
description: "Linux中有多种检查端口的方法，本文将介绍两种(组图)"
keywords: "Linux中有多种检查端口的方法，本文将介绍两种(组图)"
date: "2023-06-18T16:22:52+08:00"
defaultContentLanguage: "zh"
author: "Linux"
twitterSite: ""
thumbnail: "https://www.linuxcool.com/wp-content/uploads/2023/02/1676037893562_0.png"
categories:
  - Linux
type: article
githubURL: "https://www.github.com/"
ShowToc: true
TocOpen: true



---

场景一：了解系统开放的端口，和正在使用的端口，在各类情况下就会有所帮助。

例如：假如你的服务器正在运行着Nginx，这么其端口应当为80或则443，可以检测一下。再例如你可以检测一下SMTP、SSH或则其他服务用的是那个端口。当有新的服务须要开放端口的时侯，你须要晓得目前早已被占用的，都有什么端口。

据悉，可以检测一下是否有开放的可用于入侵测量的端口。

Linux中有多种检测端口的方式，本文将介绍两种。

使用lsof检测当前系统开放的端口

不管你是直接登陆的系统，还是使用ssh联接的，都可以使用lsof命令来检测端口：

```
sudo lsof -i -P -n
```

该命令用于查找用户使用的文件和进程。上述命令中的选项 **查看linux操作系统版本的命令**，包括：

然而，这也会展示许多计算机并没有窃听的其他端口。

我们可以通过管线将此输出传输到grep，并匹配模式“LISTEN”linux怎么查看系统版本，如下所示：

```
sudo lsof -i -P -n | grep LISTEN
```

这样就只显示计算机正在窃听的，以及正在运行的服务器所占用的端口。

![查看linux系统版本 命令_linux命令查看内核版本_查看linux操作系统版本的命令](https://www.linuxcool.com/wp-content/uploads/2023/02/1676037893562_0.png)

使用netcat命令检测远程服务器上的端口

ncNetcat)是一个命令行实用程序，使用TCP和UDP合同在网路计算机之间读取和写入数据。

以下是nc命令的句型：

```
nc [options] host port
```

这个工具有一个很实用的-z选项，它会让nc命令扫描正在窃听的守护进程，而且不会向端口发送任何数据。

将其与-v选项结合，启动详尽信息，会有详尽信息的输出。

#如下是使用nc命令扫描开放的端口：

nc-z-v1-655352>&1|grep-v'Connectionrefused'

#将里面的替换为你要检测的Linux系统的IP地址。

#至于为何我会选择1到65535，那是由于端口的范围是**1到65535**。

#最后，通过管线将输出传到grep，使用-v选项可以排除“拒绝联接(Connectionrefused)”的端口。

#这样才会扫描到计算机上所有开放的端口，这种端口可以被网路上的其他机器访问。

#以上命令没有测试读者可自行测试。，

losf与nc的不同点：

lsof比nc速率要快；

并且使用lsof须要先登入到系统中，而且具有sudo访问权限；

假如你扫描的是你早已登陆到的系统，可以优先选择lsof；

nc命令可以很灵活地扫描端口，而不须要登入。

lsof命令简介

lsof命令用于显示Linux系统当前已打开的所有文件列表。查看进程或系统打开的文件会给调试带来极大的帮助。下边简单地介绍lsof常使用的功能。

(lsof（listopenfiles) 命令用于查看你进程打开的文件，打开文件的进程，进程打开的端口(TCP、UDP),还可以用于寻回/恢复被删掉的文件。lsof命令须要访问核心显存和各类文件，所以须要具备root超级管理员权限的用户能够执行此命令。

句型格式

```
lsof [Options]
```

选项说明

```
-a         #显示打开文件的进程
-c  #显示指定进程所打开的文件
-g         #显示GID号进程详情
-d  #显示占用该文件号的进程
+d   #显示目录下被打开的文件
+D   #递归列出目录下被打开的文件
-n   #显示使用NFS的文件
-l        #在输出显示用户ID而不是用户名
-i   #输出符合条件的进程
-p #输出指定进程号所打开的文件
-u   #显示指定UID号进程详情
-h   #显示帮助信息

-t   #仅获取进程ID
-U   #获取UNIX套接口地址
-F   #格式化输出结果
-v   #显示版本信息
```

nc命令简介

linux的nc命令 **查看linux操作系统版本的命令**，NetCat，在网路工具中有“瑞士军刀”美誉“，是解决这个问题的工具。nc命令安装：yuminstallnc

句型格式

```
nc [-hlnruz][-g][-G][-i][-o][-p][-s][-v...][-w][主机名称][通信端口...]
```

选项说明

```
 -g 设置路由器跃程通信网关，最丢哦可设置8个。
 -G 设置来源路由指向器，其数值为4的倍数。
 -h 在线帮助。

 -i 设置时间间隔，以便传送信息及扫描通信端口。
 -l 使用监听模式，管控传入的资料。
 -n 直接使用IP地址，而不通过域名服务器。
 -o 指定文件名称，把往来传输的数据以16进制字码倾倒成该文件保存。
 -p 设置本地主机使用的通信端口。
 -r 乱数指定本地与远端主机的通信端口。
 -s 设置本地主机送出数据包的IP地址。
 -u 使用UDP传输协议。
 -v 显示指令执行过程。
 -w 设置等待连线的时间。
 -z 使用0输入/输出模式，只在扫描通信端口时使用。
```

以上是看来一些文章的总结分享内容永久免费linux服务器，欢迎补充讨论。