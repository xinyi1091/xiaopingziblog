
---

title: rpm与yum

date: 2019-06-20 23:18:58 +0800

tags: [LINUX,RPM,Yum]
categories: LINUX

---


<a name="kOWju"></a>
# RPM（红帽软件包管理器）
在RPM（红帽软件包管理器）公布之前，要想在Linux系统中安装软件只能采取源码包的方式安装。早期在Linux系统中安装程序是一件非常困难、耗费耐心的事情，而且大多数的服务程序仅仅提供源代码，需要运维人员自行编译代码并解决许多的软件依赖关系，因此要安装好一个服务程序，运维人员需要具备丰富知识、高超的技能，甚至良好的耐心。而且在安装、升级、卸载服务程序时还要考虑到其他程序、库的依赖关系，所以在进行校验、安装、卸载、查询、升级等管理软件操作时难度都非常大。

RPM机制则为解决这些问题而设计的。RPM有点像Windows系统中的控制面板，会建立统一的数据库文件，详细记录软件信息并能够自动分析依赖关系。目前RPM的优势已经被公众所认可，使用范围也已不局限在红帽系统中了。下表是一些常用的RPM软件包命令

| 安装软件的命令格式 | rpm -ivh filename.rpm |
| --- | --- |
| 升级软件的命令格式 | rpm -Uvh filename.rpm |
| 卸载软件的命令格式 | rpm -e filename.rpm |
| 查询软件描述信息的命令格式 | rpm -qpi filename.rpm |
| 列出软件文件信息的命令格式 | rpm -qpl filename.rpm |
| 查询文件属于哪个RPM的命令格式 | rpm -qf filename |

<a name="Pe2q3"></a>
# Yum
尽管RPM能够帮助用户查询软件相关的依赖关系，但问题还是要运维人员自己来解决，而有些大型软件可能与数十个程序都有依赖关系，在这种情况下安装软件会是非常痛苦的。Yum软件仓库便是为了进一步降低软件安装难度和复杂度而设计的技术。Yum软件仓库可以根据用户的要求分析出所需软件包及其相关的依赖关系，然后自动从服务器下载软件包并安装到系统。Yum软件仓库的技术拓扑如下图所示。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561045657869-78f511d3-b49b-480a-92df-f22f6115f0f2.png#align=left&display=inline&height=609&name=image.png&originHeight=761&originWidth=2188&size=130237&status=done&width=1750.4)

Yum软件仓库中的RPM软件包可以是由红帽官方发布的，也可以是第三方发布的，当然也可以是自己编写的。下表是一些常用的yum命令。

| yum repolist all | 列出所有仓库 |
| --- | --- |
| yum list all | 列出仓库中所有软件包 |
| yum info软件包名称 | 查看软件包信息 |
| yum install软件包名称 | 安装软件包 |
| yum reinstall软件包名称 | 重新安装软件包 |
| yum update软件包名称 | 升级软件包 |
| yum remove软件包 | 移除软件包 |
| yum clean all | 清除所有仓库缓存 |
| yum check-update | 检查可更新的软件包 |
| yum grouplist | 查看系统中已经安装的软件包组 |
| yum groupinstall软件包组 | 安装指定的软件包组 |
| yum groupremove软件包组 | 移除指定的软件包组 |
| yum groupinfo软件包组 | 查询指定的软件包组信息 |

<a name="PfCRd"></a>
# 关系
RPM是为了简化安装的复杂度，而Yum软件仓库是为了解决软件包之间的依赖关系。


