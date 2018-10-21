---
title: raspberry系统安装手册
date: 2018-10-21 10:27:21
tags: 
    - 树莓派  
categories:
    - 笔记  

---

本手册不需要显示器及键盘连树莓派操作, 使用windows系统来为tf卡安装系统, mac和linux我这里没用过, 这些写在上面, 下面不说这些了

### 事先准备
硬件: 
* 树莓派 x1
* tf卡 x1 (这边我就叫tf卡了, 不要纠结就是sd卡)
* 读卡器 x1
* 正常可用的PC x1

软件/镜像: 
* [树莓派官方系统下载](https://www.raspberrypi.org/downloads/ "") 这里面两种我选择的 `RASPBIAN` 点进去我选择的是 `Raspbian Stretch with desktop` 这里注意下载不了种子你就多试几次, 或者用梯子
* [SD Memory Card formatter](https://www.sdcard.org/chs/index.html "") 进去点下载再点 `... for Windows Download` 拖到最底下点 `Accept` (注意: 这个东西不一定会用上新TF卡可以直接用windows直接操作格式化就好了)
* [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/ "") 这个直接点进去下载装上
* [PuTTY](https://www.putty.org/ ""), [advanced-ip-scanner](http://www.advanced-ip-scanner.com/ "") 这两个自己点进去下载安装, 这两个不用也无所谓


### 安装系统
我这边只讲重点, 其他的问题网上都有

1. 把tf卡插上格式化, 注意只能是 `FAT16` 和 `FAT32` 这边给出[官网解释](https://www.raspberrypi.org/documentation/installation/sd-cards.md ""), 不理解的继续看接下来的解决办法, 用 `Win32DiskImager` 把镜像的 `.img` 往里写入, 别选错盘, 注意: 如果有任何其他关于格式化等等的报错全部点取消退出, 只要是提示了写入成功那就行, 一律点取消退出, 如果弹出来句柄错误啥的, 卡住不动啥的, 看下面的解决办法
    
2. 写入完成在tf卡的根目录下添加一个没有后缀的文件 `SSH` 这个就空文件, 电脑上不显示后缀的, 请把后缀调出来, 另外添加一个文件 `wpa_supplicant.conf` 里面的内容就下面的, `ssid, psk, key_mgmt` 自己改下自己的无线名称, 密码和加密方式

    


```bash
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=CN
    
network={
    ssid="WiFi-A"
    psk="12345678"
    key_mgmt=WPA-PSK
}
```

    
3. 好了这就ok了, tf卡插树莓派连上电源直接启动
4. 等待, 多等等
5. 查下你无线网络内的ip `advanced-ip-scanner` 可以查, 找到你的树莓派, 它上面就写的叫 `Raspberry Pi` 在路由里看就比较不方便了, 你看多出来的就是了 
6. 用 `PuTTY` SSH远程 用户名:pi 密码:raspberry, 连上了就OK, 直接终端命令用`ssh pi@192.168.xxx.xxx`

### 异常解决办法
上面的都是正常情况, 肯定不会顺风顺水啊, 这里着重讲我遇到的这个问题:

#### tf卡的格式化问题

之前无法将tf卡格式化为 `FAT32` 和 `FAT16` 的看条, 如果你看过官网的解释你的问题应该解决了, 那么这里我给没看懂官网解释的复述一下, 简单来说就是你的tf卡太大了

> The standard formatting tools built into Windows are limited, as they only allow partitions up to 32GB to be formatted as FAT32, so to format a 64GB partition as FAT32 you need to use a third-party formatting tool. 

这里给出[官网推荐第三方格式化工具](http://www.ridgecrop.demon.co.uk/guiformat.htm ""), 用这个工具去格才能顺利将大于32G的tf卡格成 `FAT32` , 链接不稳定的自己搜 `FAT32 Format` 或者 `guiformat`
    

#### tf卡无法格式化, 写入据句柄报错

* 先拿出 `SD Memory Card formatter` 格式化, 不要用 `overwrite` 太慢了
* 然后用管理员打开cmd 用 `diskpart` 来格式化 输入 `diskpart` 进入工具后先用 `list disk` 查下所有的磁盘 `select disk 2` 这个是根据显示 `###` 号来的 选几就操作几, 别选错, 然后无脑 `clean`, `create partition primary`, `active`, `format fs=fat32 quick` 然后一直等, 显示 `100 百分比已完成 diskpart成功格式化该卷` 这就ok了, 出错就重复之前的所有步骤包括 `SD Memory Card formatter` 
* 之后继续写入, 如果还报错, 继续重复以上所有步骤, 直到成功

