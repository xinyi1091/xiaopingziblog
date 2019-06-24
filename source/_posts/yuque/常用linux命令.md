
---

title: 常用linux命令
date:  2018-09-07 09:25:00 +0800
tags:  [LINUX,命令]
categories: LINUX

---

<a name="m7JKb"></a>
## 1. 强大好用的shell
![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561101033448-a8c589c5-e392-4c76-ae2d-fb7c80b14ea4.png#align=left&display=inline&height=846&name=image.png&originHeight=1057&originWidth=2047&size=83663&status=done&width=1637.6)<br />Shell是一个命令行工具。Shell（也称为终端或壳）充当的是人与内核（硬件）之间的翻译官，用户把一些命令“告诉”终端，它就会调用相应的程序服务去完成某些工作。现在包括红帽 系统在内的许多主流Linux系统默认使用的终端是Bash（Bourne-Again SHell）解释器。主流Linux系统选择Bash解释器作为命令行终端主要有以下4项优势。

- 通过上下方向键来调取过往执行过的Linux命令；
- 命令或参数仅需输入前几位就可以用Tab键补全；
- 具有强大的批处理脚本；
- 具有实用的环境变量功能
<a name="AeNAu"></a>
## 2. 执行查看帮助命令
要想准确、高效地完成各种任务，仅依赖于命令本身是不够的，还应该根据实际情况来灵活调整各种命令的参数。常见执行Linux命令的格式是这样的：

```bash
命令名称 [命令参数] [命令对象]
```
命令对象一般是指要处理的文件、目录、用户等资源，而命令参数可以用长格式（完整的选项名称），也可以用短格式（单个字母的缩写），两者分别用--与-作为前缀。(见下表的实例)

| 长格式 | man --help |
| --- | --- |
| 短格式 | man -h |

使用 `man man` 命令来查看man命令自身的帮助信息。

```bash
[root@localhost ~]# man man
```
回车:<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561101906122-d542a520-99ec-4891-89cb-fa00169ea494.png#align=left&display=inline&height=525&name=image.png&originHeight=656&originWidth=1604&size=129054&status=done&width=1283.2)<br />在man命令帮助信息的界面中，所包含的常用操作按键及其用途如下表所示:

| **按键** | **用途** |
| :---: | :---: |
| 空格键 | 向下翻一页 |
| page down  | 向下翻一页 |
| page up | 向上翻一页 |
| home | 直接前往首页 |
| end | 直接前往尾页 |
| / | 从上至下搜索某个关键词，如"/linux" |
| ? | 从下至上搜索某个关键词，如“?linux” |
| n | 定位到下一个搜索的关键词 |
| N | 定位到上一个搜索的关键词 |
| q | 退出帮助文档 |

man命令的帮助信息及结构:

| **结构名称** | **代表意义** |
| :---: | :---: |
| NAME | 命令的名称 |
| SYNOPSIS | 参数的大致使用方法 |
| DESCRIPTION | 描述 |
| EXAMPLES | 演示（附带简单说明） |
| OVERVIEW | 概述 |
| DEFAULTS | 默认的功能 |
| OPTIONS | 具体的可用选项（带介绍） |
| ENVIRONMENT | 环境变量 |
| FILES | 用到的文件 |
| SEE ALSO | 相关的资料 |
| HISTORY | 维护历史与联系方式 |

<a name="UUlu6"></a>
## 3.常用系统工作命令
<a name="IROkH"></a>
### 3.1 echo命令
echo命令用于在终端输出字符串或变量提取后的值，格式为“echo [字符串 | $变量]”。

把指定字符串“www.123.com”输出到终端屏幕

```bash
[root@localhost ~]# echo www.123.com
www.123.com
[root@localhost ~]# echo $SHELL   # 使用$变量的方式提取变量SHELL的值
/bin/bash
```
<a name="BXgCl"></a>
### 3.2 date命令
date命令用于显示及设置系统的时间或日期，格式为“date [选项] [+指定的格式]”。

只需在强大的date命令中输入以“+”号开头的参数，即可按照指定格式来输出系统的时间或日期。<br />date命令中常见的参数格式及作用如下表所示。

| **参数** | **作用** |
| :---: | :---: |
| %t | 跳格[Tab键] |
| %H | 小时（00～23） |
| %I | 小时（00～12） |
| %M | 分钟（00～59） |
| %S | 秒（00～59） |
| %j | 今年中的第几天 |

按照默认格式查看当前系统时间的date命令如下所示：

```bash
[root@localhost ~]# date 
2019年 06月 21日 星期五 15:42:07 CST
```
按照“年-月-日 小时:分钟:秒”的格式查看当前系统时间的date命令如下所示：

```bash
[root@localhost ~]# date "+%Y-%m-%d %H:%M:%S"
2019-06-21 15:44:40
```
将系统的当前时间设置为2017年9月1日8点30分的date命令如下所示：

```bash
[root@localhost ~]# date -s "20170901 8:30:00"
2017年 09月 01日 星期五 08:30:00 CST
```
再次使用date命令并按照默认的格式查看当前的系统时间，如下所示:

```bash
[root@localhost ~]# date
2017年 09月 01日 星期五 08:30:17 CST
```
date命令中的参数%j可用来查看今天是当年中的第几天。这个参数能够很好地区分备份时间的新旧，即数字越大，越靠近当前时间。该参数的使用方式以及显示结果如下所示。

```bash
[root@localhost ~]# date "+%j"
244
```
<a name="VuCjg"></a>
### 3.3 reboot
reboot命令用于重启系统，其格式为reboot。<br />由于重启计算机这种操作会涉及硬件资源的管理权限，因此默认只能使用root管理员来重启，其命令如下：

```bash
[root@localhost ~]# reboot
```
<a name="6SmxU"></a>
### 3.4 poweroff
poweroff命令用于关闭系统，其格式为poweroff。<br />该命令与reboot命令相同，都会涉及硬件资源的管理权限，因此默认只有root管理员才可以关闭电脑，其命令如下：

```bash
[root@localhost ~]# poweroff
```
<a name="nw4lT"></a>
### 3.5 wget命令
wget命令用于在终端中下载网络文件，格式为“wget [参数] 下载地址”。

wget命令的参数以及作用

| 参数 | 作用 |
| --- | --- |
| -b | 后台下载模式 |
| -P | 下载到指定目录 |
| -t | 最大尝试次数 |
| -c | 断点续传 |
| -p | 下载页面内所有资源，包括图片、视频等 |
| -r | 递归下载 |

例子:

```bash
[root@localhost ~]# wget http://www.linuxprobe.com/docs/LinuxProbe.pdf --no-check-certificate
--2017-01-01 08:41:38--  http://www.linuxprobe.com/docs/LinuxProbe.pdf
正在解析主机 www.linuxprobe.com (www.linuxprobe.com)... 124.14.2.235
正在连接 www.linuxprobe.com (www.linuxprobe.com)|124.14.2.235|:80... 已连接。
已发出 HTTP 请求，正在等待回应... 301 Moved Permanently
位置：https://www.linuxprobe.com/docs/LinuxProbe.pdf [跟随至新的 URL]
--2017-01-01 08:41:38--  https://www.linuxprobe.com/docs/LinuxProbe.pdf
正在连接 www.linuxprobe.com (www.linuxprobe.com)|124.14.2.235|:443... 已连接。
警告: 无法验证 www.linuxprobe.com 的由 “/C=US/O=DigiCert Inc/OU=www.digicert.com/CN=Encryption Everywhere DV TLS CA - G1” 颁发的证书:
  颁发的证书还未生效。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：17393770 (17M) [application/pdf]
正在保存至: “LinuxProbe.pdf”

100%[=======================================================================================================================================================================>] 17,393,770  7.39MB/s 用时 2.2s   

2017-01-01 08:41:40 (7.39 MB/s) - 已保存 “LinuxProbe.pdf” [17393770/17393770])
```
会直接下载保存在当前目录:

```bash
[root@localhost ~]# ls
anaconda-ks.cfg  initial-setup-ks.cfg  LinuxProbe.pdf
```
接下来，我们使用wget命令递归下载www.linuxprobe.com 网站内的所有页面数据以及文件，下载完后会自动保存到当前路径下一个名为www.linuxprobe.com的目录中。

```bash
[root@localhost ~]# wget http://www.linuxprobe.com --no-check-certificate
```
<a name="BDkqd"></a>
### 3.6 ps命令
ps命令用于查看系统中的进程状态，格式为“ps [参数]”。

ps命令的参数和作用:

| 参数 | 作用 |
| --- | --- |
| -a | 显示所有进程（包括其他用户的进程） |
| -u | 用户以及其他详细信息 |
| -x | 显示没有控制终端的进程 |

Linux系统中时刻运行着许多进程，如果能够合理地管理它们，则可以优化系统的性能。在Linux系统中，有5种常见的进程状态，分别为**运行、中断、不可中断、僵死与停止**，其各自含义如下所示。

- R（运行）：进程正在运行或在运行队列中等待。
- S（中断）：进程处于休眠中，当某个条件形成后或者接收到信号时，则脱离该  状态。
- D（不可中断）：进程不响应系统异步信号，即便用kill命令也不能将其中断。
- Z（僵死）：进程已经终止，但进程描述符依然存在, 直到父进程调用wait4()系统函数后将进程释放。
- T（停止）：进程收到停止信号后停止运行。

执行 `ps aux` (可以省略‘-’)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561106630330-f6413b82-db59-4d2a-bac2-cdcdd1eb2c08.png#align=left&display=inline&height=315&name=image.png&originHeight=394&originWidth=1272&size=59476&status=done&width=1017.6)<br />每列说明:

- USER   进程所有者
- PID 进程ID号
- %CPU 运算器占用率
- %MEM 内存占用率
- VSZ  虚拟内存使用量（单位是KB）
- RSS 占用的固定内存量（单位是KB）
- TTY 所在终端
- STAT 进程状态
- START 被启动的时间
- TIME 实际使用cpu的时间
- COMMAND  命令名称与参数
<a name="sQHXh"></a>
### 3.7 top命令
top命令用于动态地监视进程活动与系统负载等信息，其格式为top。

top命令相当强大，能够动态地查看系统运维状态，完全将它看作Linux中的“强化版的Windows任务管理器”。top命令的运行界面如图所示。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561106969474-79dc9702-de43-4240-a4dd-cf55767bbafd.png#align=left&display=inline&height=516&name=image.png&originHeight=645&originWidth=818&size=85188&status=done&width=654.4)

在图中，top命令执行结果的前5行为系统整体的统计信息，其所代表的含义如下。

- 第1行：系统时间、运行时间、登录终端数、系统负载（三个数值分别为1分钟、5分钟、15分钟内的平均值，数值越小意味着负载越低）。
- 第2行：进程总数、运行中的进程数、睡眠中的进程数、停止的进程数、僵死的进程数。
- 第3行：用户占用资源百分比、系统内核占用资源百分比、改变过优先级的进程资源百分比、空闲的资源百分比等。

> 注:第3行中的数据均为CPU数据并以百分比格式显示，例如“97.1 id”意味着有97.1%的CPU处理器资源处于空闲。


- 第4行：物理内存总量、内存使用量、内存空闲量、作为内核缓存的内存量。
- 第5行：虚拟内存总量、虚拟内存使用量、虚拟内存空闲量、已被提前加载的内存量。
<a name="atdrk"></a>
### 3.8 pidof命令
pidof命令用于查询某个指定服务进程的PID值，格式为“pidof [参数] [服务名称]”。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561107453049-edb4d08b-b878-4765-a510-97e2fd642ce6.png#align=left&display=inline&height=74&name=image.png&originHeight=167&originWidth=1682&size=26920&status=done&width=746)
<a name="klSZC"></a>
### 3.9 kill
kill命令用于终止某个指定PID的服务进程，格式为“kill [参数] [进程PID]”。

```bash
[root@localhost ~]# kill 9949
```
<a name="6bNlY"></a>
### 3.10 killall
killall命令用于终止**某个指定名称的服务**所对应的**全部**进程，格式为：“killall [参数] [进程名称]”。<br />通常来讲，复杂软件的服务程序会有多个进程协同为用户提供服务，如果逐个去结束这些进程会比较麻烦，此时可以使用killall命令来批量结束某个服务程序带有的全部进程。

```bash
[root@localhost ~]# pidof httpd
13581 13580 13579 13578 13577 13576
[root@localhost ~]# killall httpd
[root@localhost ~]# pidof httpd
[root@localhost ~]#
```
<a name="8oM6P"></a>
## 4. 系统检测状态命令
接下来会逐个讲解与网卡网络、系统内核、系统负载、内存使用情况、当前启用终端数量、历史登录记录、命令执行记录以及救援诊断等相关命令的使用方法。
<a name="aeMPe"></a>
### 4.1 ifconfig
ifconfig命令用于获取网卡配置与网络状态等信息，格式为“ifconfig [网络设备] [参数]”。

使用ifconfig命令来查看本机当前的网卡配置与网络状态等信息时，其实主要查看的就是网卡名称、inet参数后面的IP地址、ether参数后面的网卡物理地址（又称为MAC地址），以及RX、TX的接收数据包与发送数据包的个数及累计流量：

```bash
[root@localhost ~]# ifconfig
ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.2.105  netmask 255.255.255.0  broadcast 192.168.2.255
        inet6 fe80::fa0b:715f:dda:140e  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:db:26:cf  txqueuelen 1000  (Ethernet)
        RX packets 73938  bytes 93839195 (89.4 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 16257  bytes 7186837 (6.8 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 144  bytes 15504 (15.1 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 144  bytes 15504 (15.1 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
        ether 52:54:00:5a:3d:3a  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```
<a name="cvvGH"></a>
### 4.2 uname
uname命令用于查看系统内核与系统版本等信息，格式为“uname [-a]”。

在使用uname命令时，一般会固定搭配上-a参数来完整地查看当前系统的内核名称、主机名、内核发行版本、节点名、系统时间、硬件名称、硬件平台、处理器类型以及操作系统名称等信息。

```bash
[root@localhost ~]# uname -a
Linux localhost.localdomain 3.10.0-957.el7.x86_64 #1 SMP Thu Nov 8 23:39:32 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```
顺带一提，如果要查看当前系统版本的详细信息，则需要查看redhat-release文件

```bash
[root@localhost ~]# cat /etc/redhat-release 
CentOS Linux release 7.6.1810 (Core) 
```
<a name="qyhjT"></a>
### 4.3 uptime
uptime用于查看系统的负载信息，格式为uptime。

uptime命令真的很棒，它可以显示当前系统时间、系统已运行时间、启用终端数量以及平均负载值等信息。平均负载值指的是系统在最近1分钟、5分钟、15分钟内的压力情况（下面load average）；负载值越低越好，尽量不要长期超过1，在生产环境中不要超过5。

```bash
[root@localhost ~]# uptime
 17:08:29 up  2:48,  2 users,  load average: 0.01, 0.02, 0.05
```
<a name="5nVfB"></a>
### 4.4 free
free用于显示当前系统中内存的使用量信息，格式为“free [-h]”。

在使用free命令时，可以结合使用-h参数以更人性化的方式输出当前内存的实时使用量信息。

```bash
[root@localhost ~]# free -h
              total        used        free      shared  buff/cache   available
Mem:           972M        667M         71M         11M        233M         81M
Swap:          2.0G         46M        2.0G
```

- total  内存总量 
- used  已用量
- free  可用量
- shared   进程共享的内存量
- buff/cache  磁盘缓存的内存量
- available  缓存的内存量
<a name="zp4g1"></a>
### 4.5 who
who用于查看当前登入主机的用户终端信息，格式为“who [参数]”。

这三个简单的字母可以快速显示出所有正在登录本机的用户的名称以及他们正在开启的终端信息

```bash
[root@localhost ~]# who
xinyi    :0           2019-06-21 15:18 (:0)
root     pts/0        2019-06-21 15:19 (192.168.2.104)
```

- 登录用户名
- 登录终端
- 登录时间
<a name="iTCtL"></a>
### 4.6 last
last命令用于查看所有系统的登录记录，格式为“last [参数]”。

使用last命令可以查看本机的登录记录。但是，由于这些信息都是以日志文件的形式保存在系统中，因此黑客可以很容易地对内容进行篡改。千万不要单纯以该命令的输出信息而判断系统有无被恶意入侵！

```bash
[root@localhost ~]# last
root     pts/0        192.168.2.104    Fri Jun 21 15:19   still logged in   
xinyi    :0           :0               Fri Jun 21 15:18   still logged in   
reboot   system boot  3.10.0-957.el7.x Thu Jun 20 23:12 - 17:15  (18:03)    
root     pts/0        192.168.2.104    Thu Jun 20 23:01 - crash  (00:10)    
root     pts/1        192.168.2.104    Thu Jun 20 22:06 - crash  (01:05)    
xinyi    pts/0        :0               Thu Jun 20 22:05 - 22:37  (00:31)    
xinyi    pts/0        :0               Thu Jun 20 21:47 - 21:49  (00:01)    
xinyi    :0           :0               Thu Jun 20 21:46 - 23:08  (01:22)    
reboot   system boot  3.10.0-957.el7.x Thu Jun 20 21:37 - 17:15  (19:37)    
```
<a name="ZGr1X"></a>
### 4.7 history
history命令用于显示历史执行过的命令，格式为“history [-c]”。

执行history命令能显示出当前用户在本地计算机中执行过的最近1000条命令记录。如果觉得1000不够用，还可以自定义/etc/profile文件中的HISTSIZE变量值。在使用history命令时，如果使用-c参数则会清空所有的命令历史记录。还可以使用“!编码数字”的方式来重复执行某一次的命令。总之，history命令有很多有趣的玩法等待您去开发。

```bash
[root@localhost ~]# history
    1  cd /etc/
    2  ls
    3  ls centos-release
    4  cat centos-release
    5  cat redhat-release 
    6  pwd
    7  cd /home/
    8  ls
    9  man
   10  man man
   11  man ls
   12  man man
[root@localhost ~]# !2
ls
anaconda-ks.cfg  initial-setup-ks.cfg  www.linuxprobe.com
```
历史命令会被保存到用户家目录中的.bash_history文件中。Linux系统中以点（.）开头的文件均代表隐藏文件，这些文件大多数为系统服务文件，可以用cat命令查看其文件内容。

```bash
[root@localhost ~]# cat .bash_history 
```
要清空当前用户在本机上执行的Linux命令历史记录信息，可执行如下命令：

```bash
[root@localhost ~]# history -c
[root@localhost ~]# history
    1  history
```
<a name="2SvPJ"></a>
### 4.8 sosreport命令
sosreport命令用于收集系统配置及架构信息并输出诊断文档，格式为sosreport

```bash
[root@localhost ~]# sosreport
```
当Linux系统出现故障需要联系技术支持人员时，大多数时候都要先使用这个命令来简单收集系统的运行状态和服务配置信息，以便让技术支持人员能够远程解决一些小问题，亦或让他们能提前了解某些复杂问题。在下面的输出信息中，标识的部分是收集好的资料压缩文件以及校验码，将其发送给技术支持人员即可：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561110488588-457b9ef8-00a4-4123-97b1-26fa864f8687.png#align=left&display=inline&height=606&name=image.png&originHeight=758&originWidth=845&size=66811&status=done&width=676)
<a name="GDnCY"></a>
## 5. 工作目录切换命令
<a name="C1PiM"></a>
### 5.1 pwd
pwd命令用于显示用户当前所处的工作目录，格式为“pwd [选项]”。
<a name="ZltIz"></a>
### 5.2 cd
cd命令用于切换工作路径，格式为“cd [目录名称]”。<br />以通过cd命令迅速、灵活地切换到不同的工作目录。除了常见的切换目录方式，还可以使用“cd -”命令返回到上一次所处的目录，使用“cd..”命令进入上级目录，以及使用“cd ~”命令切换到当前用户的家目录，亦或使用“cd ~username”切换到其他用户的家目录。

```bash
[root@localhost ~]# pwd
/root
[root@localhost ~]# cd ..
[root@localhost /]# cd ~
[root@localhost ~]# cd ~xinyi
[root@localhost xinyi]# pwd
/home/xinyi
[root@localhost xinyi]# cd -
/root
```
<a name="IGG6w"></a>
### 5.3 ls
ls命令用于显示目录中的文件信息，格式为“ls [选项] [文件] ”。

使用ls命令的“-a”参数看到全部文件（包括隐藏文件），使用“-l”参数可以查看文件的属性、大小等详细信息。将这两个参数整合之后，再执行ls命令即可查看当前目录中的所有文件并输出这些文件的属性信息。

```bash
[root@localhost ~]# ls -al
总用量 40
dr-xr-x---.  5 root root  241 6月  21 17:43 .
dr-xr-xr-x. 17 root root  224 6月  20 21:30 ..
-rw-------.  1 root root 1798 6月  20 21:36 anaconda-ks.cfg
-rw-------.  1 root root 1150 6月  21 17:35 .bash_history
-rw-r--r--.  1 root root   18 12月 29 2013 .bash_logout
-rw-r--r--.  1 root root  176 12月 29 2013 .bash_profile
-rw-r--r--.  1 root root  176 12月 29 2013 .bashrc
drwx------.  4 root root   31 6月  20 22:06 .cache
drwxr-xr-x.  3 root root   18 6月  20 22:06 .config
-rw-r--r--.  1 root root  100 12月 29 2013 .cshrc
drwx------.  3 root root   25 6月  20 21:38 .dbus
-rw-r--r--.  1 root root 1846 6月  20 21:40 initial-setup-ks.cfg
-rw-------.  1 root root   40 6月  21 15:38 .lesshst
-rw-r--r--.  1 root root  129 12月 29 2013 .tcshrc
-rw-------.  1 root root  132 6月  21 17:43 .xauthBc1uXS
```
如果想要查看目录属性信息，则需要额外添加一个-d参数。

```bash
[root@localhost ~]# ls -dl .config/
drwxr-xr-x. 3 root root 18 6月  20 22:06 .config/
```
<a name="M1kVi"></a>
## 6. 文本文件编辑命令
<a name="LIAcq"></a>
### 6.1 cat
cat命令用于查看纯文本文件（内容较少的），格式为“cat [选项] [文件]”。

cat这个命令也很好记，因为cat在英语中是“猫”的意思，小猫咪是不是给您一种娇小、可爱的感觉呢？

如果在查看文本内容时还想顺便显示行号的话，不妨在cat命令后面追加一个-n参数：

```bash
[root@localhost ~]# cat -n initial-setup-ks.cfg 
     1	#version=DEVEL
     2	# X Window System configuration information
     3	xconfig  --startxonboot
     4	# License agreement
     5	eula --agreed
     6	# System authorization information
     7	auth --enableshadow --passalgo=sha512
     8	# Use CDROM installation media
     9	cdrom
    10	# Use graphical install
    11	graphical
    12	# Run the Setup Agent on first boot
    13	firstboot --enable
....省略....
```
<a name="XqRuB"></a>
### 6.2 more
more命令用于查看纯文本文件（内容较多的），格式为“more [选项]文件”。

使用cat命令阅读长篇的文本内容，信息就会在屏幕上快速翻滚，导致自己还没有来得及看到，内容就已经翻篇了。因此对于长篇的文本内容，推荐使用more命令来查看。more命令会在最下面使用百分比的形式来提示您已经阅读了多少内容。您还可以使用空格键或回车键向下翻页：

```bash
[root@localhost ~]# more initial-setup-ks.cfg
```
![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561111277144-2185d604-5d23-4c54-8089-e4f45c739d1f.png#align=left&display=inline&height=619&name=image.png&originHeight=774&originWidth=1137&size=87473&status=done&width=909.6)
<a name="hTUD6"></a>
### 6.3 head
head命令用于查看纯文本文档的前N行，格式为“head [选项] [文件]”。

如果只想查看文本中前20行的内容，该怎么办呢？head命令可以派上用场了：

```bash
[root@localhost ~]# head -n 20 initial-setup-ks.cfg 
#version=DEVEL
# X Window System configuration information
xconfig  --startxonboot
# License agreement
eula --agreed
# System authorization information
auth --enableshadow --passalgo=sha512
# Use CDROM installation media
cdrom
# Use graphical install
graphical
# Run the Setup Agent on first boot
firstboot --enable
# System services
services --disabled="chronyd"
# Keyboard layouts
keyboard --vckeymap=cn --xlayouts='cn'
# System language
lang zh_CN.UTF-8
```
<a name="oJUo9"></a>
### 6.4 tail
tail命令用于查看纯文本文档的后N行或持续刷新内容，格式为“tail [选项] [文件]”。

tail命令的操作方法与head命令非常相似，只需要执行“tail -n 20 文件名”命令就可以查看文件的后20行。tail命令最强悍的功能是可以持续刷新一个文件的内容，**当想要实时查看最新日志文件时，这特别有用，此时的命令格式为“tail -f 文件名”：**

```bash
[root@localhost ~]# tail -f /var/log/messages
Jun 21 17:46:54 localhost systemd: Starting Time & Date Service...
Jun 21 17:46:54 localhost dbus[6237]: [system] Successfully activated service 'org.freedesktop.timedate1'
Jun 21 17:46:54 localhost systemd: Started Time & Date Service.
Jun 21 17:48:11 localhost journal: JS WARNING: [resource:///org/gnome/shell/ui/popupMenu.js 717]: reference to undefined property "_delegate"
Jun 21 17:48:21 localhost journal: g_simple_action_set_enabled: assertion 'G_IS_SIMPLE_ACTION (simple)' failed
Jun 21 17:50:01 localhost systemd: Started Session 4 of user root.
Jun 21 17:52:24 localhost systemd: Starting Cleanup of Temporary Directories...
Jun 21 17:52:24 localhost systemd: Started Cleanup of Temporary Directories.
Jun 21 18:00:02 localhost systemd: Started Session 5 of user root.
Jun 21 18:01:01 localhost systemd: Started Session 6 of user root.

```
<a name="qTcWE"></a>
### 6.5 tr
tr命令用于替换文本文件中的字符，格式为“tr [原始字符] [目标字符]”。

在很多时候，我们想要快速地替换文本中的一些词汇，又或者把整个文本内容都进行替换，如果进行手工替换，难免工作量太大，尤其是需要处理大批量的内容时，进行手工替换更是不现实。这时，就可以先使用cat命令读取待处理的文本，然后通过管道符把这些文本内容传递给tr命令进行替换操作即可。例如，把某个文本内容中的英文全部替换为大写：

```bash
[root@localhost ~]# cat initial-setup-ks.cfg | tr [a-z] [A-Z]
```
<a name="h79Td"></a>
### 6.6 wc
wc命令用于统计指定文本的行数、字数、字节数，格式为“wc [参数] 文本”。

参数

- -l 只显示行数
- -w 只显示单词数
- -c 只显示字节数

```bash
[root@localhost ~]# wc -l initial-setup-ks.cfg 
68 initial-setup-ks.cfg
[root@localhost ~]# wc -w initial-setup-ks.cfg 
176 initial-setup-ks.cfg
[root@localhost ~]# wc -c initial-setup-ks.cfg 
1846 initial-setup-ks.cfg
```
在Linux系统中，passwd是用于保存系统账户信息的文件，要统计当前系统中有多少个用户，可以使用下面的命令来进行查询。

```bash
[root@localhost ~]# wc -l /etc/passwd
43 /etc/passwd
```
<a name="UjzeP"></a>
### 6.7 stat
stat命令用于查看文件的具体存储信息和时间等信息，格式为“stat 文件名称”。

```bash
[root@localhost ~]# stat initial-setup-ks.cfg 
  文件："initial-setup-ks.cfg"
  大小：1846      	块：8          IO 块：4096   普通文件
设备：fd00h/64768d	Inode：33574981    硬链接：1
权限：(0644/-rw-r--r--)  Uid：(    0/    root)   Gid：(    0/    root)
环境：system_u:object_r:admin_home_t:s0
最近访问：2019-06-21 17:58:39.407957279 +0800
最近更改：2019-06-20 21:40:11.002993295 +0800
最近改动：2019-06-20 21:40:11.002993295 +0800
创建时间：-

```
<a name="kWqE4"></a>
### 6.8 cut

cut命令用于按“列”提取文本字符，格式为“cut [参数] 文本”。

在Linux系统中，如何准确地提取出最想要的数据，这也是我们应该重点学习的内容。一般而言，按基于“行”的方式来提取数据是比较简单的，只需要设置好要搜索的关键词即可。但是如果按列搜索，不仅要**使用-f参数来设置需要看的列数，还需要使用-d参数来设置间隔符号**。passwd在保存用户数据信息时，用户信息的每一项值之间是采用冒号来间隔的，接下来我们使用下述命令尝试提取出passwd文件中的用户名信息，即提取以冒号（：）为间隔符号的第一列内容:

```bash
[root@localhost ~]# head -n 4 /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
[root@localhost ~]# cut -d: -f1 /etc/passwd
root
bin
daemon
adm
lp
sync
shutdown
halt
mail
operator
games
ftp
nobody
systemd-network
dbus
polkitd
libstoragemgmt
colord
rpc
saslauth
abrt
rtkit
pulse
chrony
radvd
rpcuser
nfsnobody
unbound
gluster
qemu
tss
usbmuxd
geoclue
setroubleshoot
saned
gdm
gnome-initial-setup
sshd
avahi
postfix
ntp
tcpdump
xinyi
```
<a name="kUzZo"></a>
### 6.9 diff
diff命令用于比较多个文本文件的差异，格式为“diff [参数] 文件”。

在使用diff命令时，不仅可以使用--brief参数来确认两个文件是否不同，还可以使用-c参数来详细比较出多个文件的差异之处，这绝对是判断文件是否被篡改的有力神器。例如，先使用cat命令分别查看diff_A.txt和diff_B.txt文件的内容，然后进行比较：

```bash
[root@localhost ~]# cat dif_A.txt 
Hello,World
Red Hat certified
Free Linux Lessons
Shanghai,China
[root@localhost ~]# cat dif_B.txt 
Hello,World
Red Hat certified
Shanghai,China
[root@localhost ~]# diff --brief dif_A.txt dif_B.txt 
文件 dif_A.txt 和 dif_B.txt 不同
```
最后使用带有-c参数的diff命令来描述文件内容具体的不同：

```bash
[root@localhost ~]# diff -c dif_A.txt dif_B.txt 
*** dif_A.txt	2019-06-21 18:24:32.188890759 +0800
--- dif_B.txt	2019-06-21 18:25:44.801887648 +0800
***************
*** 1,4 ****
  Hello,World
  Red Hat certified
- Free Linux Lessons
  Shanghai,China
--- 1,3 ----
```
<a name="qdnNr"></a>
## 7. 文件目录管理命令
<a name="DI49C"></a>
### 7.1 touch
touch命令用于创建空白文件或设置文件的时间，格式为“touch [选项] [文件]”。

在创建空白的文本文件方面，这个touch命令相当简捷，简捷到没有必要铺开去讲。比如，touch linuxprobe命令可以创建出一个名为linuxprobe的空白文本文件。对touch命令来讲，有难度的操作主要是体现在设置文件内容的修改时间（mtime）、文件权限或属性的更改时间（ctime）与文件的读取时间（atime）上面。

参数说明

- -a  仅修改“读取时间”（atime）
- -m 仅修改“修改时间”（mtime）
- -d 同时修改atime与mtime

接下来，我们先使用ls命令查看一个文件的修改时间，然后修改这个文件，最后再通过touch命令把修改后的文件时间设置成修改之间的时间（很多黑客就是这样做的呢）：
```bash
[root@localhost ~]# ls -l dif_A.txt 
-rw-r--r--. 1 root root 70 6月  21 18:35 dif_A.txt
[root@localhost ~]# touch -d "2018-05-01 19:21" dif_A.txt 
[root@localhost ~]# ls -l dif_A.txt 
-rw-r--r--. 1 root root 70 5月   1 2018 dif_A.txt
```
<a name="F95wH"></a>
### 7.2 mkdir

mkdir命令用于创建空白的目录，格式为“mkdir [选项] 目录”。

在Linux系统中，文件夹是最常见的文件类型之一。除了能创建单个空白目录外，mkdir命令还可以结合-p参数来递归创建出具有嵌套叠层关系的文件目录。

```bash
[root@localhost ~]# mkdir l1
[root@localhost ~]# ll
总用量 16
-rw-------. 1 root root 1798 6月  20 21:36 anaconda-ks.cfg
-rw-r--r--. 1 root root   70 5月   1 2018 dif_A.txt
-rw-r--r--. 1 root root   45 6月  21 18:25 dif_B.txt
-rw-r--r--. 1 root root 1846 6月  20 21:40 initial-setup-ks.cfg
drwxr-xr-x. 2 root root    6 6月  21 18:42 l1
[root@localhost ~]# mkdir -p a/b/c
[root@localhost ~]# ll
总用量 16
drwxr-xr-x. 3 root root   15 6月  21 18:42 a
-rw-------. 1 root root 1798 6月  20 21:36 anaconda-ks.cfg
-rw-r--r--. 1 root root   70 5月   1 2018 dif_A.txt
-rw-r--r--. 1 root root   45 6月  21 18:25 dif_B.txt
-rw-r--r--. 1 root root 1846 6月  20 21:40 initial-setup-ks.cfg
drwxr-xr-x. 2 root root    6 6月  21 18:42 l1
```
<a name="TZ16x"></a>
### 7.3 cp
cp命令用于复制文件或目录，格式为“cp [选项] 源文件 目标文件”。

在Linux系统中，复制操作具体分为3种情况：

- 如果目标文件是目录，则会把源文件复制到该目录中；
- 如果目标文件也是普通文件，则会询问是否要覆盖它；
- 如果目标文件不存在，则执行正常的复制操作

cp命令的参数及作用

| 参数 | 作用 |
| --- | --- |
| -p | 保留原始文件的属性 |
| -d | 若对象为“链接文件”，则保留该“链接文件”的属性 |
| -r | 递归持续复制（用于目录） |
| -i | 若目标文件存在则询问是否覆盖 |
| -a | 相当于-pdr（p、d、r为上述参数） |

使用touch创建一个名为install.log的普通空白文件，然后将其复制为一份名为x.log的备份文件，最后再使用ls命令查看目录中的文件

```bash
[root@localhost ~]# touch install.log
[root@localhost ~]# cp install.log x.log
[root@localhost ~]# ls
a  anaconda-ks.cfg  dif_A.txt  dif_B.txt  initial-setup-ks.cfg  install.log  l1  x.log
```

<a name="ReFm2"></a>
### 7.4 mv
mv命令用于剪切文件或将文件重命名，格式为“mv [选项] 源文件 [目标路径|目标文件名]”。

剪切操作不同于复制操作，因为它会默认把源文件删除掉，只保留剪切后的文件。**如果在同一个目录中对一个文件进行剪切操作，其实也就是对其进行重命名**：

```bash
[root@localhost ~]# mv dif_B.txt dif.txt
[root@localhost ~]# ls
a  anaconda-ks.cfg  dif_A.txt  dif.txt  initial-setup-ks.cfg  l1
```
<a name="V7jA1"></a>
### 7.5 rm
rm命令用于删除文件或目录，格式为“rm [选项] 文件”。

在Linux系统中删除文件时，系统会默认向您询问是否要执行删除操作，如果不想总是看到这种反复的确认信息，可在rm命令后跟上-f参数来强制删除。另外，想要删除一个目录，需要在rm命令后面一个-r参数才可以，否则删除不掉。我们来尝试删除前面创建的install.log和x.log文件

```bash
[root@localhost ~]# rm -rf install.log x.log 
[root@localhost ~]# ls
a  anaconda-ks.cfg  dif_A.txt  dif.txt  initial-setup-ks.cfg  l1
```
<a name="BRFQt"></a>
### 7.6 dd
dd命令用于按照指定大小和个数的数据块来复制文件或转换文件，格式为“dd [参数]”。

dd命令是一个比较重要而且比较有特色的一个命令，它能够让用户按照指定大小和个数的数据块来复制文件的内容。当然如果愿意的话，还可以在复制过程中转换其中的数据。Linux系统中有一个名为/dev/zero的设备文件，每次在课堂上解释它时都充满哲学理论的色彩。因为这个文件不会占用系统存储空间，但却可以提供无穷无尽的数据，因此可以使用它作为dd命令的输入文件，来生成一个指定大小的文件。dd命令的参数及其作用如下表所示。

| 参数 | 作用 |
| :--- | :--- |
| if | 输入的文件名称 |
| of | 输出的文件名称 |
| bs | 设置每个“块”的大小 |
| count | 设置要复制“块”的个数 |

例如我们可以用dd命令从/dev/zero设备文件中取出一个大小为560MB的数据块，然后保存成名为560_file的文件。

```bash
[root@localhost ~]# dd if=/dev/zero of=560_file count=1 bs=560M
记录了1+0 的读入
记录了1+0 的写出
587202560字节(587 MB)已复制，52.3141 秒，11.2 MB/秒
[root@localhost ~]# ll -h 560_file 
-rw-r--r--. 1 root root 560M 6月  21 19:34 560_file
```
dd命令的功能也绝不仅限于复制文件这么简单。如果您想把光驱设备中的光盘制作成iso格式的镜像文件，在Windows系统中需要借助于第三方软件才能做到，但在Linux系统中可以直接使用dd命令来压制出光盘镜像文件，将它变成一个可立即使用的iso镜像：
```bash
[root@localhost ~]# dd if=/dev/cdrom of=RHEL-server-7.0-x86_64.iso
记录了8962048+0 的读入
记录了8962048+0 的写出
4588568576字节(4.6 GB)已复制，146.279 秒，31.4 MB/秒
[root@localhost ~]# ll -h RHEL-server-7.0-x86_64.iso 
-rw-r--r--. 1 root root 4.3G 6月  21 19:50 RHEL-server-7.0-x86_64.iso
```
考虑到有些读者会纠结bs块大小与count块个数的关系，下面举一个吃货的例子进行解释。假设小明的饭量（即需求）是一个固定的值，用来盛饭的勺子的大小即bs块大小，而用勺子盛饭的次数即count块个数。小明要想吃饱（满足需求），则需要在勺子大小（bs块大小）与用勺子盛饭的次数（count块个数）之间进行平衡。勺子越大，用勺子盛饭的次数就越少。由上可见，bs与count都是用来指定容量的大小，只要能满足需求，可随意组合搭配方式。
<a name="Tz7nA"></a>
### 7.7 file
file命令用于查看文件的类型，格式为“file 文件名”。

在Linux系统中，由于文本、目录、设备等所有这些一切都统称为文件，而我们又不能单凭后缀就知道具体的文件类型，这时就需要使用file命令来查看文件类型了。

```bash
[root@localhost ~]# file RHEL-server-7.0-x86_64.iso 
RHEL-server-7.0-x86_64.iso: # ISO 9660 CD-ROM filesystem data 'CentOS 7 x86_64' (bootable)
[root@localhost ~]# file dif.txt 
dif.txt: ASCII text
[root@localhost ~]# file /dev/sda
/dev/sda: block special
```
<a name="r4v9j"></a>
## 8 打包压缩与搜索命令
<a name="d0k4h"></a>
### 8.1 tar
tar命令用于对文件进行打包压缩或解压，格式为“tar [选项] [文件]”。<br />在Linux系统中，常见的文件格式比较多，其中主要使用的是.tar或.tar.gz或.tar.bz2格式，我们不用担心格式太多而记不住，其实这些格式大部分都是由tar命令来生成的。下表列出了tar命令的常用参数及作用

| 参数 | 作用 |
| :--- | :--- |
| -c | 创建压缩文件 |
| -x | 解开压缩文件 |
| -t | 查看压缩包内有哪些文件 |
| -z | 用Gzip压缩或解压 |
| -j | 用bzip2压缩或解压 |
| -v | 显示压缩或解压的过程 |
| -f | 目标文件名 |
| -p | 保留原始的权限与属性 |
| -P | 使用绝对路径来压缩 |
| -C | 指定解压到的目录 |

说明:

1. -c参数用于创建压缩文件，-x参数用于解压文件，因此这两个参数不能同时使用
2. -z参数指定使用Gzip格式来压缩或解压文件，-j参数指定使用bzip2格式来压缩或解压文件。用户使用时则是根据文件的后缀来决定应使用何种格式参数进行解压。
3. 在执行某些压缩或解压操作时，可能花费很久，为了判断解压是否在进行，推荐使用-v参数向用户不断显示压缩或解压的过程。
4. -C参数用于指定要解压到哪个指定的目录。
5. -f参数特别重要，它必须放到参数的最后一位，代表要压缩或解压的软件包名称。

一般使用 -zcvf 来压缩，-zxvf来解压

使用tar命令把/etc目录通过gzip格式进行打包压缩，并把文件命名为etc.tar.gz：

```bash
[root@localhost ~]# tar -zcvf etc.tar.gz /etc
..。省略压缩过程....
[root@localhost ~]# ls etc.tar.gz 
etc.tar.gz
```
接下来将打包后的压缩包文件指定解压到/root/etc目录中（先使用mkdir命令来创建/root/etc目录）：

```bash
[root@localhost ~]# mkdir /root/etc
[root@localhost ~]# tar -zxvf etc.tar.gz -C /root/etc

```
<a name="Wmm6i"></a>
### 8.3 grep:grep (global search regular expression(RE) and print out the line
grep命令用于在文本中执行关键词搜索，并显示匹配的结果，格式为“grep [option] pattern file”。<br />grep命令的参数及其作用如表所示。

| 参数 | 作用 |
| :--- | :--- |
| -b | 将可执行文件(binary)当作文本文件（text）来搜索 |
| -c | 仅显示找到的行数 |
| -i | 忽略大小写 |
| -n | 显示行号 |
| -v | 反向选择——仅列出没有“关键词”的行。 |

grep命令是**用途最广泛**的文本搜索匹配工具，虽然有很多参数，但是大多数基本上都用不到。我们在这里只讲两个最最常用的参数：-n参数用来显示搜索到信息的行号；-v参数用于反选信息（即没有包含关键词的所有信息行）。这两个参数几乎能完成您日后80%的工作需要，至于其他上百个参数，即使以后在工作期间遇到了，再使用man grep命令查询也来得及。

在Linux系统中，/etc/passwd文件是保存着所有的用户信息，而一旦用户的登录终端被设置成/sbin/nologin，则不再允许登录系统，因此可以使用grep命令来查找出当前系统中不允许登录系统的所有用户信息：

```bash
[root@localhost ~]# grep /sbin/nologin  /etc/passwd
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
………………省略部分输出过程信息………………
```
<a name="RqlKc"></a>
### 8.4 find
find命令用于按照指定条件来查找文件，格式为“find [查找路径] 寻找条件 操作”。<br />
<br />在Linux系统中，搜索工作一般都是通过find命令来完成的，它可以使用不同的文件特性作为寻找条件（如文件名、大小、修改时间、权限等信息），一旦匹配成功则默认将信息显示到屏幕上。find命令的参数以及作用如下表所示。

| 参数 | 作用 |
| :--- | :--- |
| -name | 匹配名称 |
| -perm | 匹配权限（mode为完全匹配，-mode为包含即可） |
| -user | 匹配所有者 |
| -group | 匹配所有组 |
| -mtime -n +n | 匹配修改内容的时间（-n指n天以内，+n指n天以前） |
| -atime -n +n | 匹配访问文件的时间（-n指n天以内，+n指n天以前） |
| -ctime -n +n | 匹配修改文件权限的时间（-n指n天以内，+n指n天以前） |
| -nouser | 匹配无所有者的文件 |
| -nogroup | 匹配无所有组的文件 |
| -newer f1 !f2 | 匹配比文件f1新但比f2旧的文件 |
| --type b/d/c/p/l/f | 匹配文件类型（后面的字幕字母依次表示块设备、目录、字符设备、管道、链接文件、文本文件） |
| -size | 匹配文件的大小（+50KB为查找超过50KB的文件，而-50KB为查找小于50KB的文件） |
| -prune | 忽略某个目录 |
| -exec …… {}\\; | 后面可跟用于进一步处理搜索结果的命令（下文会有演示） |

这里需要重点讲解一下-exec参数重要的作用。这个参数用于把find命令搜索到的结果交由紧随其后的命令作进一步处理，它十分类似于管道符技术，并且由于find命令对参数的特殊要求，因此虽然exec是长格式形式，但依然只需要一个减号（-）。<br />
<br />根据文件系统层次标准（Filesystem Hierarchy Standard）协议，Linux系统中的配置文件会保存到/etc目录中。如果要想获取到该目录中所有以host开头的文件列表，可以执行如下命令：

```bash
[root@localhost ~]# find /etc -name "host*" -print
/etc/host.conf
/etc/hosts
/etc/hosts.allow
/etc/hosts.deny
/etc/selinux/targeted/active/modules/100/hostname
/etc/hostname
/etc/avahi/hosts
```
如果要在整个系统中搜索权限中包括SUID权限的所有文件，只需使用-4000即可：

```bash
[root@localhost ~]# find / -perm -4000 -print
```
<a name="D3ijF"></a>
## 9.复习
 1．在RHEL 7系统及众多的Linux系统中，最常使用的Shell终端是什么？<br />答：Bash（Bourne-Again SHell）解释器。<br />2．执行Linux系统命令时，添加参数的目的是什么？<br />答：为了让Linux系统命令能够更贴合用户的实际需求进行工作。<br />3．Linux系统命令、命令参数及命令对象之间，普遍应该使用什么来间隔？<br />答：应该使用一个或多个空格进行间隔。<br />4．请写出用echo命令把SHELL变量值输出到屏幕终端的命令。<br />答：echo $SHELL。<br />5．简述Linux系统中5种进程的名称及含义。<br />答：在Linux系统中，有下面5种进程名称。<br />R（运行）：进程正在运行或在运行队列中等待。<br />S（中断）：进程处于休眠中，当某个条件形成后或者接收到信号时，则脱离该状态。<br />D（不可中断）：进程不响应系统异步信号，即便用kill命令也不能将其中断。<br />Z（僵死）：进程已经终止，但进程描述符依然存在, 直到父进程调用wait4()系统函数后将进程释放。<br />T（停止）：进程收到停止信号后停止运行。<br />6．请尝试使用Linux系统命令关闭PID为5529的服务进程。<br />答：执行kill 5529命令即可；若知道服务的名称，则可以使用killall命令进行关闭。<br />7．使用ifconfig命令查看网络状态信息时，需要重点查看的4项信息分别是什么？<br />答：这4项重要信息分别是网卡名称、IP地址、网卡物理地址以及RX/TX的收发流量数据大小。<br />8．使用uptime命令查看系统负载时，对应的负载数值如果是0.91、0.56、0.32，那么最近15分钟内负载压力最大的是哪个时间段？<br />答：通过负载数值可以看出，最近1分钟内的负载压力是最大的。<br />9．使用history命令查看历史命令的执行记录时，命令前面的数字除了排序外还有什么用处？<br />答：还可以用“!数字”的命令格式重复执行某一次的命令记录，从而避免了重复输入较长命令的麻烦。<br />10．若想查看的文件具有较长的内容，那么使用cat、more、head、tail中的哪个命令最合适？<br />答：文件内容较长，使用more命令；反之使用cat命令。<br />11．在使用mkdir命令创建有嵌套关系的目录时，应该加上什么参数呢？<br />答：应该加上-p递归迭代参数，从而自动化创建有嵌套关系的目录。<br />12．在使用rm命令删除文件或目录时，可使用哪个参数来避免二次确认呢？<br />答：可使用-f参数，这样即可无需二次确认。<br />13．若有一个名为backup.tar.gz的压缩包文件，那么解压的命令应该是什么？<br />答：应该用tar命令进行解压，执行tar -xzvf backup.tar.gz命令即可。<br />14．使用grep命令对某个文件进行关键词搜索时，若想要进行文件内容反选，应使用什么参数？<br />答：可使用-v参数来进行匹配内容的反向选择，即显示出不包含某个关键词的行。

