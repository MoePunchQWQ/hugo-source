+++
date = '2025-10-18T15:52:25+08:00'
draft = false
title = 'Sony NW-A35 播放器玩机趣谈'
tags = ['Docs','玩机','Android','音频']
series = ['随便谈谈', '音频设备', 'Android']
+++
3个月前，因为服役多年的 iPod nano 2 播放器坏了，我就在网上物色新的播放器。作为一个高三学生，播放器有什么特殊的功能都不重要，我只需要一个音质优秀，支持创建播放列表，系统较为好用，续航过得去的产品。在看了各种各样的设备之后，我选中了 Sony NW-A35，并最终以 230 元人民币的价格拿下。前任机主给播放器刷了 NW-WM1Z 的移植包，比原系统好用的不是一点半点。网上一直流传的说法是，这几代索尼播放器用的都是基于 Linux 的系统，所以我也没有什么去刷机的想法，直到前几天我在网上看见一个有趣的项目，它可以将播放器的 USB DAC 功能的延迟降低至 50ms 左右，而原来的延迟大约在 1~2 秒左右，感兴趣，遂于休息时间研究了一下。

### llusbadc 项目的安装
这里我参考的是 Bilibili 上面的教程[编译 llusbdac 解决索尼 Walkman 系列 DAC 延迟](https://www.bilibili.com/opus/859321452990562325)，原项目的链接如下：[llusbdac](https://github.com/zhangboyang/llusbdac)。我在编译并安装之后并没有成功触发这个插件，不知道是不是移植的系统的问题。

### Android 系统的实质
虽然没有成功激活 llusbdac 插件，但是我偶然间发现了这些播放器用的都是魔改的 Android 5.0 系统。llusbadc 安装时候有一个激活 ADB 调试桥的选项，原理大概是在播放器根目录下 build.prop 文件中添加了`persist.sys.sony.icx.adb=1`语句，激活了 ADB 服务。值得注意的是，虽然可以打开 ADB 服务，但是原来的系统已经被索尼精简到丧失了 Android 基本功能的地步，目前我发现的功能缺失有以下几点：
* Package Manager( 包管理器 ) 的缺失
* Priv-app, app 等预装软件全部消失    
 
这个系统只能说还算是个 Android 系统，指望在播放器上面装什么软件是不可能的。以下是它的分区结构：
```
emmc@android -> /dev/block/mmcblk0p19  
emmc@bootimg -> /dev/block/mmcblk0p8  
emmc@cache -> /dev/block/mmcblk0p20  
emmc@cm4 -> /dev/block/mmcblk0p21  
emmc@contents -> /dev/block/mmcblk0p29  
emmc@db -> /dev/block/mmcblk0p24  
emmc@dkb -> /dev/block/mmcblk0p17  
emmc@ebr1 -> /dev/block/mmcblk0p1  
emmc@expdb -> /dev/block/mmcblk0p13  
emmc@kb -> /dev/block/mmcblk0p16  
emmc@logo -> /dev/block/mmcblk0p12  
emmc@misc -> /dev/block/mmcblk0p11  
emmc@nvp -> /dev/block/mmcblk0p22  
emmc@nvram -> /dev/block/mmcblk0p3  
emmc@option1 -> /dev/block/mmcblk0p25  
emmc@option2 -> /dev/block/mmcblk0p26  
emmc@option3 -> /dev/block/mmcblk0p27  
emmc@pro_info -> /dev/block/mmcblk0p2  
emmc@protect_f -> /dev/block/mmcblk0p4  
emmc@protect_s -> /dev/block/mmcblk0p5  
emmc@recovery -> /dev/block/mmcblk0p9  
emmc@sec_ro -> /dev/block/mmcblk0p10  
emmc@seccfg -> /dev/block/mmcblk0p6  
emmc@tee1 -> /dev/block/mmcblk0p14  
emmc@tee2 -> /dev/block/mmcblk0p15  
emmc@uboot -> /dev/block/mmcblk0p7  
emmc@usrdata -> /dev/block/mmcblk0p28  
emmc@var -> /dev/block/mmcblk0p23  
emmc@xhrome -> /dev/block/mmcblk0p18  
```
也许我会找时间把它的镜像备份出来，感兴趣的朋友们可以自行研究，我手上的 A35 的 soc 是 MT8590，也许可以移植一个完整的安卓系统，但是没有了索尼的独家音效等等功能只能说是得不偿失。用户以 MTP 方式访问的文件夹是根目录下的 /contents，adb pull 也是从这里拉取。暂时没有发现更多有意思的东西，如果有我会再补充。

### LDAC 无法开启
我第一次用支持 LDAC 的耳机连接 A35 的时候，系统无法自动开启 LDAC，只能用 SBC 协议进行传输。可是根据索尼官网的信息，无论是原来的 A35 还是移植后的 WM1Z，均支持 LDAC 音频。后来发现需要在设置-音频设备连接设置-无线播放品质中手动切换到-LDAC-品质优先。切换后，LDAC 协议正常开启。

本文未经授权，严禁转载到 CSDN, GitCode 等平台