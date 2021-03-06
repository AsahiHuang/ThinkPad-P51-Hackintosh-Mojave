# ThinkPad P51 Hackintosh

>2019.12.6
>
>* 系统版本更新至 Catalina 15.2，相关 EFI 到新的 [repo](https://github.com/AsahiHuang/ThinkPadP51-Hackintosh-Catalina)
>* QQ讨论群：951898568



> 2019.8.11 
>
> * 系统版本已更新至Mojava 10.14.6 18G87，升级clover版本至5032
> * 添加 小红点及三指驱动
> * 添加 对Thinkpad dock for workstation usb 的支持



**基于大量前人经验及帮助完成,在这里向他们表示敬意及感谢!**

~~系统版本Mojava 10.14.2 , clover版本4976(*目前已经系统内更新至10.14.6，无大问题*)~~

目前升级到10.14.6 18G97
clover版本 5032

![](http://ww2.sinaimg.cn/large/006tNc79gy1g5w0vrvzw2j319g0u0dlr.jpg)





~~原帖的镜像下载地址:http://bbs.pcbeta.com/viewthread-1800347-1-1.html~~

原帖的镜像[下载](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1823920)（注意该系统版本10.14.6 18G84，自带clover为5027）

**注意下载完成后核对文件md5,文件缺失会造成安装失败**

*本EFI已移除SMbios中序列号信息有需要自行加上*



## 设备大概配置情况

|  类别  |   型号    |  状态  | 其他                                                         |
| :----: | :-------: | :----: | :----------------------------------------------------------- |
| 处理器 | i7-7700HQ |  正常  |                                                              |
|  屏幕  |    4k     |  正常  | 可选显示效果                                                 |
|  集显  |   HD630   |  正常  | P5x系列M1200及其他独显均无解(*关于P70,1vbios有解,具体自行查找,这里不适用*) |
|  电池  |           |  正常  | 正常显示电池信息及电池图标,双系统win10内启用电池阈值mac内已可生效 |
|  键盘  |           |  正常  | 能打字                                                       |
| 触控板 |           |  正常  | 移动,~~其余能且只能双指滚动~~ 增加三指手势                      |
| 小红点 |           | 能用 | ~~有很多大佬给出了具体方法不过效果都不如win下,等后面有时间了解决~~ |
|  睡眠  |           |  正常  | 盒盖后睡眠正常(*偶尔可能重启情况不常见*),小红灯睡眠和唤醒时状态正常 |
|  USB   |           |  正常  | 目前还没发现有什么需要改进                                   |
|	雷电3  ||待验|理论可驱动,具体问题见下面|
| 以太网卡 ||正常|一般没什么问题|
| WiFi |94360cs2|正常|蓝牙与WiFi原装网卡无解,本人使用的**转接卡+mac网卡**方案无需驱动,其他网卡驱动请自行解决|
| 蓝牙 |同上|正常|同WiFi,**AirDop/handoff等功能不保证正常**(*原因见上*)|
| 快捷键 ||待完善|音量没问题,亮度无法使用,如有解决办法请联系(*亮度显示器内可调*)|
| 摄像头 ||||
| EM7455 ||待解决|走USB,设备内可见,如果有解决办法的还请联系我,谢谢!|
| 待补充 ||||

**其余诸如express card , SD卡读卡器,指纹,校色(我并没有)之类的洗洗睡吧**



> 2019.8.11

## 关于底座dock支持

这里需要感谢[@the3asic](https://t.me/@the3asic "telegram")提供的补丁SSDT-UIAC

> Basically basic: 对了我这里自己也买了一个P51用的Dock，里面的USB是HS04/SS04，也提交过给之前那位了：https://github.com/MirkoCovizzi/thinkpad-p51-hackintosh/issues/2

如果有需要的可以下载测试，已经放在EFI/CLOVER/ACPI/patched下，有关问题可以直接联系他

## 关于小红点和触控板

我是非常喜欢使用小红点，mac下的小红点驱动非常感人

目前加入的也是针对小红点优化的VoodooPS2Controller，触控板能实现三指

但小红点只能可接受的程度，而且触控板非常容易干扰打字时的光标

*可以使用PrtSc键（截图键）关闭触控板*



> 2019.8.4

## 关于升级

系统内可以从10.14.2升级到10.14.6，各项功能基本和原来一样
**系统升级前先更新clover版本到最新**
https://github.com/Dids/clover-builder/releases
更新后可能会出现电脑睡眠唤醒后无声的问题，可以通过更新alc及lilu组件解决
附上驱动更新地址，下载对应的releases版本替换
https://github.com/acidanthera/Lilu/releases
https://github.com/acidanthera/AppleALC/releases
https://github.com/acidanthera/WhateverGreen/releases

## 关于Thunderbolt3

我问过许多大佬,也见到成功案例,实际上确实可以驱动,你在EFI文件内也能看到相应的补丁,但没有雷电设备所以无法验证,而且在设备信息的雷电条目也不会显示.许多P52机主发出了自己驱动雷电3的证明,并实现了外接显卡的功能,这解决了*P5x系列黑果没法外接显示器*的问题,虽然解决办法代价极高,但有需要的可以尝试,**如果身边有相应设备可以验证的还请联系.**

**特别注意P5x系列的雷电3不支持热插拔,需要在关机状态下插上后开机识别**

## 关于三码洗白问题

因为EFI内已经移除了序列号相关信息，如有需要使用iMessage，FaceTime等功能，这边介绍一个教程可以洗白（**黑苹果使用apple id登陆存在ban账号的可能，请自行评估风险**）

洗白教程地址：https://forum.51nb.com/thread-1757464-1-1.html

## 关于P5X系列安装原生网卡

原先我使用的是94352z，那时候价格还没现在这么离谱（**鄙视那些炒高网卡价格的无良奸商**）
至于为什么换成原生网卡，主要因为不需要额外的驱动
还有原生mac的功能支持的非常好，
比如说aw解锁mac，94252z好像并不能实现
![](http://ww1.sinaimg.cn/large/006tNc79gy1g5nfu21935j30y60u04ct.jpg)

如果你有与apple设备的互动的需求，推荐使用原生网卡
安装方式目前我知道有两种：
1. 原位安装，需要剪掉转接板一部分，塞进去，[方案地址](https://forum.51nb.com/forum.php?mod=viewthread&tid=1899444&highlight=p52%2B%CD%F8%BF%A8)
2. 转接板和网卡分离，排线相连，转接卡在原网卡位，原生网卡放在wwan位

我使用的是方案二，两种方案所需材料可以某宝搞到，具体实现自行决定





如果你有需要我改进或者更好解决方法的可以通过Telegram联系我[@AsahiHuang](https://t.me/AsahiHuang)
这是极为快捷的途径,谢谢你的帮助!

本人旨在分享给各位希望能方便的解决基础问题从而去更好的优化,你可以使用而非商业用途
这一过程存在的问题和风险还请自行斟酌及承担



AsahiHuang







