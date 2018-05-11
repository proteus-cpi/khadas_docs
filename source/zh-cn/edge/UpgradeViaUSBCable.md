title: 通过USB升级固件
---
## 通过Windows升级
### 准备
* 下载[USB驱动](http://www.mediafire.com/file/h2adcu2u9245y12/DriverAssitant_v4.6.zip)并解压。
* 运行`DriverInstall.exe`来安装USB驱动。
  * 先点击`驱动卸载`来卸载旧的驱动。
  ![DriverInstall uninstall](/images/edge/DriverInstall_uninstall_zh.png)
  * 在点击`驱动安装`来安装新的驱动。
  ![DriverInstall install](/images/edge/DriverInstall_install_zh.png)
* 下载[Android Tool](http://www.mediafire.com/file/tc40f47bxso8j9k/AndroidTool_Release_zh_v2.52.zip)并解压。
* `AndroidTool.exe`就是烧录工具，是免安装的，直接运行即可。

### 升级步骤
去报USB驱动已经安装，并按如下步骤进行升级。

#### 烧录安卓

1. 运行`AndroidTool.exe`, 点击`升级固件-->固件`来加载镜像文件。
![AndroidTool firmware select](/images/edge/AndroldTool_firmware_zh.png)
2. 通过USB-C数据线连接Edge和PC。
3. 使Edge[进入升级模式](/zh-cn/edge/HowtoBootIntoUpgradeMode.html)。
4. 执行上述操作后你会看到Edge升级模式设备。
* Loader模式如下：
![AndroidTool loader](/images/edge/AndroldTool_loader_zh.png)
* Maskrom模式如下：
![AndroidTool maskrom](/images/edge/AndroldTool_maskrom_zh.png)

现在执行`升级`就会开始升级：
![AndroidTool upgrade](/images/edge/AndroldTool_upgrade_zh.png)

## 在Ubuntu下升级固件
### 准备
```
$ sudo apt-get install libusb-dev git parted
```
### 获取烧录工具
镜像烧录工具在仓库[utils](https://github.com/khadas/utils)中。
```
$ git clone https://github.com/khadas/utils
```
如果以前克隆过仓库，只需更新即可：
```
$ cd /path/to/utils
$ git pull
```
### 安装烧录工具
需要安装USB规则文件以及创建链接文件。
```
$ cd /path/to/utils
$ ./INSTALL
```
如果成功你会看到如下打印信息：
```
Installing Amlogic flash-tool...

===============================================

Host PC: Ubuntu 16.04

===============================================

Installing USB rules...
[sudo] password for nick: 
Installing flash-tool...
Done!

Installing Rockchip flash-tool...

===============================================

Host PC: Ubuntu 16.04

===============================================

Installing USB rules...
Installing flash-tool...
Done!
Installing Khadas burn-tool...
Done!
```
**注意：** 安装需要`root`权限。

### 如何在Ubuntu下烧录镜像
```
$ burn-tool -v rk -i /path/to/image
```
如果执行成功你会看到如下打印信息：
```
Try to burn Rockchip image...
Rockchip Linux image with GPT found!
Try to burn Rockchip Linux image...
Burn to eMMC...
PARTITIONS OFFSET: 0 sectors.
Loading loader...
Support Type:RK330C	Loader ver:1.12	Loader Time:2018-04-26 10:24:40
Upgrade loader ok.
Write LBA from file (100%)
directlba=1,first4access=1,gpt=1
Write gpt...
Write gpt ok.
Reset Device OK.
Done!
```

### 如何卸载烧录工具
```
$ cd /path/to/utils
$ ./UNINSTALL
```

**注意：**烧录工具只在**Ubuntu 16.04**上验证过。

### 参考
* [如何进入升级模式](/zh-cn/edge/HowtoBootIntoUpgradeMode.html)
