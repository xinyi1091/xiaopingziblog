
---

title: VMWARE中安装LINUX

date: 2018-09-07 09:25:00 +0800

tags: [LINUX,环境变量]

categories: LINUX

---


<a name="mNyKI"></a>
# 软硬件准备

- 软件：推荐使用VMwear，我用的是VMwear 12
- 镜像：CentOS7 ,如果没有镜像可以在阿里云开源镜像下载: [https://mirrors.aliyun.com/centos/7.6.1810/isos/x86_64/](https://mirrors.aliyun.com/centos/7.6.1810/isos/x86_64/) 
- 镜像说明可以参考:[https://mirrors.aliyun.com/centos/7.6.1810/isos/x86_64/0_README.txt](https://mirrors.aliyun.com/centos/7.6.1810/isos/x86_64/0_README.txt) 
<a name="IYdBY"></a>
# 虚拟机准备

1. 打开VMwear选择新建虚拟机

![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561039656329-c0aeb8df-7588-4db8-986d-8b9539467e4b.png#align=left&display=inline&height=387&name=image.png&originHeight=484&originWidth=884&size=130442&status=done&width=707.2)

2. 典型安装与自定义安装
- 典型安装：VMwear会将主流的配置应用在虚拟机的操作系统上，对于新手来很友好。
- 自定义安装：自定义安装可以针对性的把一些资源加强，把不需要的资源移除。避免资源的浪费。

这里我选择自定义安装。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561039695759-29d505fd-6a46-481e-8cdb-f7538d1afcec.png#align=left&display=inline&height=418&name=image.png&originHeight=523&originWidth=623&size=102508&status=done&width=498.4)

3. 虚拟机兼容性选择

这里要注意兼容性，如果是VMwear12创建的虚拟机复制到VM11、10或者更低的版本会出现一不兼容的现象。如果是用VMwear10创建的虚拟机在VMwear12中打开则不会出现兼容性问题<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561039722684-2868e50b-a0e5-4977-82f3-9c99ac3e79ab.png#align=left&display=inline&height=427&name=image.png&originHeight=534&originWidth=624&size=70301&status=done&width=499.2)

4. 选择稍后安装操作系统

![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561039746642-35317271-3f6c-4c79-8bb7-316ff413ae9e.png#align=left&display=inline&height=431&name=image.png&originHeight=539&originWidth=624&size=76465&status=done&width=499.2)

5. 操作系统的选择

这里选择之后安装的操作系统，正确的选择会让vm tools更好的兼容。这里选择linux下的CentOS<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561039782886-479c1e44-09b6-4c91-909c-ffe665fc9aa2.png#align=left&display=inline&height=428&name=image.png&originHeight=535&originWidth=623&size=66586&status=done&width=498.4)

6. 虚拟机位置与命名

虚拟机名称就是一个名字，在虚拟机多的时候方便自己找到。<br />VMwear的默认位置是在C盘下，我这里改成F盘。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561039957276-13b9db4e-39fc-4b6b-94af-014ad9bd8bfe.png#align=left&display=inline&height=426&name=image.png&originHeight=532&originWidth=626&size=52237&status=done&width=500.8)

7.  处理器与内存的分配

处理器分配要根据自己的实际需求来分配。在使用过程中CPU不够的话是可以再增加的。这次只做安装CentOS演示，所以处理器与核心都选1<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561039986100-642c39dc-b7cd-4c9a-a332-9713a23a8e0e.png#align=left&display=inline&height=427&name=image.png&originHeight=534&originWidth=622&size=48417&status=done&width=497.6)<br />内存也是要根据实际的需求分配。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040010044-889372d3-650a-49eb-854a-1bfa2e3076b5.png#align=left&display=inline&height=426&name=image.png&originHeight=533&originWidth=618&size=83092&status=done&width=494.4)

8. 网络连接类型的选择，网络连接类型一共有桥接、NAT、仅主机和自定义四种。
- 桥接：选择桥接模式的话虚拟机和宿主机在网络上就是平级的关系，相当于连接在同一交换机上。
- NAT：NAT模式就是虚拟机要联网得先通过宿主机才能和外面进行通信。在真机中NAT虚拟机网卡对应的物理网卡是VMnet8
- 仅主机：仅让虚拟机内的主机与物理主机通信，不能访问外网，在真机中仅主机模式模拟网卡对应的物理网卡是VMnet1。

桥接与NAT模式访问互联网过程，如下图所示。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040260733-4ce73b7f-fb86-4bee-8f7e-449d486380d6.png#align=left&display=inline&height=292&name=image.png&originHeight=365&originWidth=866&size=95116&status=done&width=692.8)

这里选择桥接模式。

9. 其余两项按虚拟机默认选项即可

![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040315094-a9b7efe0-5eb4-4e53-bffd-28c27c12f4b5.png#align=left&display=inline&height=426&name=image.png&originHeight=532&originWidth=622&size=58831&status=done&width=497.6)

10. 磁盘容量

勾选将虚拟磁盘拆分成多个文件，这样可以使虚拟机方便用储存设备拷贝复制。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040398784-ca856788-2bee-4dac-92dd-5d35511e1903.png#align=left&display=inline&height=426&name=image.png&originHeight=533&originWidth=620&size=96323&status=done&width=496)

11. 磁盘名称，默认即可

![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040426917-c46e58cd-491c-4a55-84e5-985b07c17ec1.png#align=left&display=inline&height=430&name=image.png&originHeight=538&originWidth=621&size=56890&status=done&width=496.8)

12. 取消不需要的硬件

点击自定义硬件<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040477954-691192ba-3aa1-4c60-ad8d-cc0a2342cfc0.png#align=left&display=inline&height=426&name=image.png&originHeight=533&originWidth=623&size=83075&status=done&width=498.4)

选择声卡、打印机等不需要的硬件然后移除。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040505281-f137cc99-79fe-4fff-9af8-3990b4152d47.png#align=left&display=inline&height=596&name=image.png&originHeight=745&originWidth=870&size=123520&status=done&width=696)

13. 点击完成，已经创建好虚拟机。
<a name="4VQJm"></a>
# 安装**CentOS**

1. 连接iso镜像，右击刚创建的虚拟机，选择设置

![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040619715-0ac1b521-25d9-4176-926d-077f6060f6e9.png#align=left&display=inline&height=582&name=image.png&originHeight=727&originWidth=908&size=252803&status=done&width=726.4)<br />先选择CD/DVD，再选择使用ISO映像文件，最后选择浏览找到下载好的镜像文件。启动时连接一定要勾选上后确定。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040795870-006a93bb-f405-4781-9e2f-ebbd52c23d3b.png#align=left&display=inline&height=359&name=image.png&originHeight=449&originWidth=877&size=121384&status=done&width=701.6)

2. 开启虚拟机

![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040819005-d705ffa9-d12b-4518-bc6b-dff2fec2ddf6.png#align=left&display=inline&height=498&name=image.png&originHeight=622&originWidth=866&size=189492&status=done&width=692.8)

3.  安装操作系统

开启虚拟机后会出现以下界面

1. Install CentOS 7  # 安装CentOS 7
1. Test this media & install CentOS 7 # 测试安装文件并安装CentOS 7
1. Troubleshooting # 修复故障

选择第一项，安装直接CentOS 7，回车，进入下面的界面<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040874086-ecfe8895-75ce-45aa-beff-5884afbe38b2.png#align=left&display=inline&height=440&name=image.png&originHeight=550&originWidth=794&size=21868&status=done&width=635.2)<br />选择安装过程中使用的语言，这里选择英文、键盘选择美式键盘。点击Continue<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040895660-f3a32933-5caf-46af-8df2-7089a6a4b180.png#align=left&display=inline&height=517&name=image.png&originHeight=646&originWidth=870&size=205208&status=done&width=696)<br />首先设置时间:<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040916462-a792ac4a-0604-4c28-8cc4-d01dca71c8de.png#align=left&display=inline&height=526&name=image.png&originHeight=657&originWidth=874&size=228544&status=done&width=699.2)

时区选择上海，查看时间是否正确。然后点击Done<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040937516-f4ccbc79-50be-488f-9ffa-4b01a72b5ad7.png#align=left&display=inline&height=525&name=image.png&originHeight=656&originWidth=876&size=291302&status=done&width=700.8)

选择需要安装的软件<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040968858-4c3b313d-0a02-4c4f-b4bd-bfdda2ea6fcb.png#align=left&display=inline&height=530&name=image.png&originHeight=663&originWidth=882&size=229731&status=done&width=705.6)

选择 Server with Gui，然后点击Done<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561040990454-ac9d995e-c65c-4561-bdc5-721518cb0fa6.png#align=left&display=inline&height=492&name=image.png&originHeight=615&originWidth=874&size=303362&status=done&width=699.2)

选择安装位置，在这里可以进行磁盘划分。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041055417-0b4245d7-7b0d-46f5-b2f6-83a4d522d4a0.png#align=left&display=inline&height=527&name=image.png&originHeight=659&originWidth=879&size=243992&status=done&width=703.2)

选择i will configure partitioning（我将会配置分区），然后点击done<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041089601-3792ba3c-2f75-4fe3-bd58-e7edf1b28cfa.png#align=left&display=inline&height=522&name=image.png&originHeight=653&originWidth=882&size=232989&status=done&width=705.6)

如下图所示，点击加号，选择/boot，给boot分区分200M。最后点击Add<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041114259-16c456c9-9c15-4183-8e45-b616723ad323.png#align=left&display=inline&height=525&name=image.png&originHeight=656&originWidth=869&size=218995&status=done&width=695.2)

然后以同样的办法给其他三个区分配好空间后点击Done<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041143855-65fc4b5f-de3d-42a4-ae8f-2c50f2ffe0e6.png#align=left&display=inline&height=518&name=image.png&originHeight=648&originWidth=884&size=210006&status=done&width=707.2)

然后会弹出摘要信息，点击AcceptChanges(接受更改)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041168308-a6460cfc-9f36-42ab-88b7-4ce2b72ef341.png#align=left&display=inline&height=517&name=image.png&originHeight=646&originWidth=862&size=239225&status=done&width=689.6)

设置主机名与网卡信息<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041187424-3b36f708-d39e-47fb-bd02-933fd4287339.png#align=left&display=inline&height=522&name=image.png&originHeight=652&originWidth=873&size=199773&status=done&width=698.4)

首先要打开网卡，然后查看是否能获取到IP地址(我这里是桥接)，再更改主机名后点击Done。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041228037-384a218d-cab2-4302-9c49-e6f1c1029f49.png#align=left&display=inline&height=521&name=image.png&originHeight=651&originWidth=885&size=230807&status=done&width=708)

最后选择Begin Installation(开始安装)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041249355-11470085-4506-457e-ad5e-f56ab12ee4b4.png#align=left&display=inline&height=521&name=image.png&originHeight=651&originWidth=875&size=202759&status=done&width=700)

设置root密码<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041268909-5522a1b8-b3a2-4843-aab2-9e1ecc085ee5.png#align=left&display=inline&height=527&name=image.png&originHeight=659&originWidth=873&size=261180&status=done&width=698.4)

设置root密码后点击Done<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041293249-1e92b8ad-5727-4ae9-9740-1b6b49e2ac5c.png#align=left&display=inline&height=494&name=image.png&originHeight=618&originWidth=881&size=143548&status=done&width=704.8)

点击USER CREATION 创建管理员用户<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041313105-1e8e94d0-d0cd-4076-bf1b-d55ad80af30c.png#align=left&display=inline&height=526&name=image.png&originHeight=657&originWidth=877&size=243000&status=done&width=701.6)

输入用户名密码后点击Done<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041334377-62144f43-b486-4857-b4eb-62835d7e6867.png#align=left&display=inline&height=525&name=image.png&originHeight=656&originWidth=885&size=175465&status=done&width=708)

等待系统安装完毕重启系统即可<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041361210-4f9bc014-7b40-43ab-859e-111854026eaa.png#align=left&display=inline&height=511&name=image.png&originHeight=639&originWidth=885&size=243037&status=done&width=708)
<a name="wvGnq"></a>
# 最终效果截图
![image.png](https://cdn.nlark.com/yuque/0/2019/png/352947/1561041662727-5c27892b-c10b-451b-9914-837c8aa15ede.png#align=left&display=inline&height=614&name=image.png&originHeight=768&originWidth=1280&size=549417&status=done&width=1024)

