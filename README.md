**12490F-MSI-B660M-D4-WIFI-MORTAR-RX6600**

适用于12490F-MSI-B660M-D4-WIFI-MORTAR-技嘉RX6600的黑苹果EFI

**进展里偶尔里我用了一些不错的软件，对于折腾黑苹果很有帮助，大家可以看看。大家遇到什么问题，可以发issue，虽不一定及时回复，但可以让我们共同避坑**。

**目前有部分内容参考借鉴的[EFI](https://github.com/SuperNG6/MSI-B660-Monterey-EFI)，十分推荐！以下是本机详细内容，建议根据自己的macOS版本下载相应的EFI文件。**


| **配置(Hardware)** | **型号(Model)**                         |
| ------------------ | :-------------------------------------- |
| 处理器(CPU)        | Intel i5 12490F                         |
| 主板(Mainboard)    | MSI-B660M-D4-WIFI-MORTAR                |
| 显卡(GPU)          | AMD RX6600                              |
| 内存(RAM)          | 光威 威龙D45 16G DDR4 3200MHz*2         |
| 硬盘(SSD)          | 系统盘： 威刚 XPGS70BLADE PCIE4.0 1T    |
|                    | 附属盘： 爱国者 aigo P7000 Z PCIE4.0 2T |
|                    | 备份盘：东芝 P300 3T 7200转             |
| WiFi + BT          | Intel AX211                             |
| WiFi + BT          | BCM94360CD                            |

**镜像(Mirror)**
现在可采用：macOS Sequoia

最初：
macOS Monterey 12.5 21G72 Installer for OC/CLOVER/PE三分区原版镜像

来源于：黑果小兵的部落阁

**BIOS设置**

**此处注意bios的版本，使用本EFI请确保bios的版本为7D42v13，如果不是，可能会出现卡安装以及WiFi问题，参照[相关问题](https://github.com/zemise/12490F-MSI_MORTAR-WiFi-RX6600-EFI-OC/issues/19])**

关闭

- 安全启动（一定要关，否则错误代码为Drivers XXX at 0 cannot be loaded，我在这个错误卡了很久，得亏Q群内大佬提点才发现）
- CSM（启动模式仅UEFI)
- 快速开机 Fast Boot
- MS快速开机
- Intel VT-D
- CFG Lock

**功能(Functions)**

目前该有的都有，趋近完美

- macOS Sequoia系统中 iPhone镜像不可用

**备注(Additional)**

机型：MacPro7,1  

Intel Xeon W-3245M CPU3.20 GHz

请自行生成三码



**目前进展(Current progress)**

请看最新进展，往期进展仅供参考

***
2024/10/17
- update OpenCore 1.0.2
- update macOS Sequoia
- BCM Wi-Fi patch fix
- 时隔大半年，一直没更新此EFI，主要是本黑苹果还是很流畅的。此次升级到macOS15，纯属因为想学习swift语言的vapor框架
- 博通网卡的带来的隔空投送让我恋恋不舍，所以此次更新，也给博通网卡打了补丁，依旧好用(博通网卡的补丁需要自己下载安装OpenCore-Patcher，打上修复，其他参数配置已在EFI写好)。若需要默认网卡，请参照2023年记录

***

***
2023/8/19
- update OpenCore 0.9.4
- ocvalidate check pass 

***
2023/8/16

- 无聊购入了一块BCM94360CD网卡，目前隔空投送、随航Get
注意：如果没有博通的免驱网卡，而为默认网卡为AX211，需要勾选回我取消的Kext。AX211的使用在之前一个版本就已经调试好了，可以放心，Wi-Fi和蓝牙都正常。
<img width="1176" alt="image" src="https://github.com/zemise/12490F-MSI-B660-MORTAR-WiFi-RX6600-EFI-OC/assets/46216418/9e143845-5965-44cc-97db-b743999ac04f">

- 用Hackintool重新定制了USBPort.kext，除开主板后方的TypeC边的一个USB口不能使用外，其余全正常使用，反复尝试了多次，已经是能达到的最佳状态了
<img width="1093" alt="image" src="https://github.com/zemise/12490F-MSI-B660-MORTAR-WiFi-RX6600-EFI-OC/assets/46216418/2bdde91f-67bc-4bd2-a7df-85dd40859323">

注意：如果首次使用本EFI安装黑苹果，如果主板和我的一模一样，则无需改动USBPort.kext；但如果不同，建议取消勾选USBPort，而勾选USBToolBox、UTBMap，这里UTPMap其实也是强烈建议自行用USBToolBox定制
<img width="1174" alt="image" src="https://github.com/zemise/12490F-MSI-B660-MORTAR-WiFi-RX6600-EFI-OC/assets/46216418/e4247ec1-6d56-4980-8abe-cede008fc1c3">

目前kexts总图，供参考
<img width="1203" alt="image" src="https://github.com/zemise/12490F-MSI-B660-MORTAR-WiFi-RX6600-EFI-OC/assets/46216418/0569cf3f-0b4d-4d1f-a3c1-540da8ed876b">

新发现的问题：
- 睡眠有点小问题，睡眠后，显示屏虽然可以一直保持睡眠，但主机还是会醒，表现为开关呼吸灯由常亮(醒)➡️闪烁(睡眠)➡️常亮(醒)

记得以前似乎正常，与升级系统、插上博通网卡可能有关系，暂时解决方案：
- 从bios界面关闭USB唤醒，上述睡眠问题解决，能稳定睡眠，只是唤醒主机需要点按下电源

这样还是不够优雅，暂且搁置，有机会就再解决，等等大家的建议

***
2023/7/26

更新EFI相关驱动，OTA推送升级至Ventura 13.5

主要修复
- 蓝牙关闭后无法开启问题
- 部分声卡问题
- 某些不知名bug，驱动更新后消失
***
2023/6/01

儿童节快乐～

正逢618活动，购入了一块爱国者P7000 Z固态，安排！

本次更新EFI相关驱动，OTA推送升级至Ventura 13.4

关于AirDrop，暂时不考虑更换博通网卡，因为有比较好的替代方案。[LANDrop](https://landrop.app)不仅也可以实现传送文件，更是多平台支持，很好。

推荐2个黑苹果软件下载网站，悄悄地(纯个人分享，无利益相关)

1. [推荐01](https://www.macyy.cn)
2. [推荐02](https://www.macat.vip)
***
2022/10/28

更新EFI相关驱动，OTA推送升级至Ventura 13.0

相应截图如下，目前比较稳定，会存在软件报错，需要下载新版安装，或者参照这篇解决办法：https://m.sohu.com/a/595559403_120418263/

按这篇操作后，记得在系统的安全与隐私，再点下相应软件仍要打开，这篇文章没有写到这点

![引导界面](https://user-images.githubusercontent.com/46216418/198837052-f7216e74-e3cd-4417-8030-34d014404b86.jpg)

![标识](https://user-images.githubusercontent.com/46216418/198823854-61bc472a-43b2-4870-8f9b-7835fb053d26.jpg)

![跑分](https://user-images.githubusercontent.com/46216418/198823522-6cbe07da-b075-47d3-8ef3-21e53d337b0b.jpg)

![跑分2](https://user-images.githubusercontent.com/46216418/198823524-54e0f79d-589c-44be-ac5d-605731173756.jpg)

![跑分3](https://user-images.githubusercontent.com/46216418/198823625-f96e050e-e040-43e2-9104-82eb03f366d5.jpg)


2022/09/19

⚠️ 屏幕亮度不能调节是本身屏幕问题，现在已经由Lunar软件解决，可以自动调节亮度

⚠️ 现仅存的问题之一是airdrop是不能用

相应截图展示：

![跑分](https://user-images.githubusercontent.com/46216418/191049860-78abe15b-cdad-4056-a322-b0204bf5b16a.jpg)

![跑分2](https://user-images.githubusercontent.com/46216418/191049919-aea3a011-301d-463b-a83d-9c0949cd8777.jpg)

![蓝牙](https://user-images.githubusercontent.com/46216418/191049974-35cfd76d-3bdb-497b-b38f-37ecbd3251d9.jpg)

![Wi-FI](https://user-images.githubusercontent.com/46216418/191049992-518de150-d0a0-4e37-a980-bca6c53a97e7.jpg)

![稳定性](https://user-images.githubusercontent.com/46216418/191050011-ec860b83-76c6-4c6c-b9cc-f713f14310bf.jpg)


**感谢(Acknowledgment)**

1. 国光、黑果小兵

1. 黑苹果安装讨论群的各位大佬

2. 兔子

3. issue的各位

**Link**

* https://apple.sqlsec.com
* https://blog.daliansky.net




