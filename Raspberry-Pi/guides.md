##Getting Started
下载镜像文件: http://www.raspberrypi.org/downloads  
我这里下载的是：`2013-05-25-wheezy-raspbian.zip`

###制作镜像
以下步骤适用于Mac OS X：

1. `2013-05-25-wheezy-raspbian.zip`解压后得到`2013-05-25-wheezy-raspbian.img`，打开终端，cd到这个目录  
![ls](https://raw.github.com/miclle/WALL-E/master/Raspberry-Pi/images/guides-dir-ls.png)

2. 插入你的SD卡，再运行`df –h` 会发现多了一个`/dev/disk1s1`的设备  
![df -h](https://raw.github.com/miclle/WALL-E/master/Raspberry-Pi/images/guides-df-h.png)

3. 卸载SD卡，输入`sudo diskutil unmount /dev/disk1s1`  
![diskutil unmount](https://raw.github.com/miclle/WALL-E/master/Raspberry-Pi/images/guides-diskutil-unmount.png)   
最后一行`Volume NO NAME on disk1s1 unmounted` disk1s1便是SD卡的名称

4. 写入镜像：  
将你的设备名（例如`/dev/disk1s1`）最后的s1去掉，然后在disk前面加上r，变成`/dev/rdisk1`，这样你就得到SD卡的原始设备名称了。
也就是说，`/dev/disk1s1` = `/dev/rdisk1`  
在终端中输入以下命令：`sudo dd bs=1m if=2013-05-25-wheezy-raspbian.img of=/dev/YOURDISKNAME`。将YOURDISKNAME改成你的原始设备名称，通常这个都是`/dev/rdisk1`  
![dd](https://raw.github.com/miclle/WALL-E/master/Raspberry-Pi/images/guides-dd.png)   

写入的过程需要一点时间。当`dd`完成了它的工作以后，将SD卡安全移除。

###初次启动Raspberry Pi
初次启动Raspberry Pi时，你会看到一个叫做raspi-config的配置工具。如果在日后使用过程中你需要更改这些设置，你可以通过在Pi的命令行中运行raspi-config来使用这个工具。在这里，你需要进行一些最基本的设置来继续使用你的Pi。  
PS.最新版本镜像raspi-config菜单与之前版本有点不同，合并了一些选项，增加了摄像头设置！

![setup-options](https://raw.github.com/miclle/WALL-E/master/Raspberry-Pi/images/guides-setup-options-1-select.png)   

首先，我们要选择`Expand Filesystem`。它的作用是将刚才写入到SD卡中的映像文件大小扩展到整张SD卡中。如果你使用的是一张较大的SD卡（例如 16GB），那么你肯定像充分利用上面的空间。因为原本的映像只有大约2GB的大小，进行该操作就能将它扩展到与你的SD卡同样的大小。
选中`Expand Filesystem`选项，然后按下回车。你会看到如下提示，只需要再按一下回车就可以回到raspi-config的主菜单中。  
![root-partition-has-been-resized](https://raw.github.com/miclle/WALL-E/master/Raspberry-Pi/images/guides-root-partition-has-been-resized.png)   

第二项 `Change User Password`  这里可以修改默认登录密码`raspberry`

第四项 `Internationalisation Options Set up language and regional settings to match your location` 这里可以更改区域、设置语言、时区及键盘
![internationalisation-options](https://raw.github.com/miclle/WALL-E/master/Raspberry-Pi/images/guides-internationalisation-options.png)   
Raspberry Pi没有实时时钟，靠网络同步时间

其过程类似于安装Ubuntu

第八项`Advanced Options`中，可以设置SSH Server，已默认开启。

在完成以上主要设置后，返回主菜单，选择`<Finish>` 系统会提示一些变更需要重启才能生效。重启以后，你会看到一个登录界面
默认帐户为：`Username: pi ` `Password: raspberry`

###startx 图形界面
命令行中输入`startx`来进入图形界面

###WIFI Config
*  在startx进入图形界面后，桌面有一个WIFI Config图标，如果你已经将USB无线网卡插入Raspberry Pi，应该能在设置中找到一个wlan0的设备，编辑这个网络，psk设置为你的无线密码，其它与你无线参数一一对应上即可，保存设置，最后点击`Connection`连接
*  另一种设置方法是通过命令行设置 过程详见 https://github.com/miclle/WALL-E/blob/master/Raspberry-Pi/setup-wifi-raspberry-pi.md