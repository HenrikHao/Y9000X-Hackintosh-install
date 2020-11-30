**Y9000X 2020黑苹果安装教程（非商业用途，仅用于自己记录学习研究）**

@[TOC](Y9000X Opencore 安装双硬盘双系统教程)
# 电脑配置
首先是我的电脑配置，于2019年购买的Y9000X，详细配置如下

 - 型号：Y9000X 2020 
 - 主板：HM370
 - CPU：I7-9750H
 - 显卡：UHD630
 - 硬盘：PM891a（已屏蔽） + SN750
 - 网卡：DW1820A（更换原AX200，AX200目前已有驱动，详情参考[OpenIntelWireless](https://github.com/OpenIntelWireless/itlwm)）
 - 分辨率：4K
# 前期准备
 - U盘 *1 （≥16G）
 - Catalina镜像（推荐[黑果小兵](https://blog.daliansky.net/WeChat-First-macOS-Catalina-10.15.6-19G73-official-version-Clover-5119-OC-WEPE-supports-both-INTEL-and-AMD-original-images.html)）
 - EFI文件（推荐[WangRicky](https://github.com/WangRicky/Y9000X-HACKINTOSH)，其余机型请参考[长期维护机型清单](https://blog.daliansky.net/Hackintosh-long-term-maintenance-model-checklist.html)）
 - WinMD5（用于校验镜像MD5值）
 - BalenaEtcher（用于写入镜像）
 - Opencore Configurator（生成三码）
 - F2进入BIOS关闭SecureBoot，切换硬盘模式为AHCI
 - 解锁CFG Lock（可选，谨慎操作！参考[CFG Lock解锁](https://github.com/OpenIntelWireless/itlwm)）
 
 [工具汇总](https://pan.baidu.com/s/1_9-wpNX9VfXEoMs7U9ZyLA) 提取码：Md52
# 安装流程
##  1. 写入U盘镜像
 使用BalenaEtcher即可，注意右键管理员身份运行![写入镜像](https://img-blog.csdnimg.cn/20201130174614517.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
## 2. 更换EFI文件
将Boot文件夹和OC文件夹整个替换即可，OC分区在Windows下可直接读取，无需使用DiskGenius更换EFI文件，若使用Clover引导。若使用Clover引导请使用DiskGenius更换
## 3. 磁盘分区
首先建立一个ESP分区，用于安装后建立OpenCore引导（200～300Mb即可）
![建立ESP分区](https://img-blog.csdnimg.cn/20201130175425395.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
然后建立一个HFS+分区，作为MacOS系统的安装盘，我这里分配了300G的空间
![建立HFS+分区](https://img-blog.csdnimg.cn/20201130175926218.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
剩下的区域我建立了一个NTFS分区并分配了盘符作为Windows，Ubuntu和MacOS的共享区域，Ubuntu和MacOS均可读写该NTFS分区
## 4. 系统安装
开机按F12选择Opencore引导，这里注意选择，如果和我写入的是同一镜像的话我的第一个是Clover引导第二个是OpenCore第三个是WEPE
![选择引导](https://img-blog.csdnimg.cn/20201130182143900.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
进入引导后选择磁盘工具进行分区
![选择磁盘工具](https://img-blog.csdnimg.cn/20201130182736638.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
点击显示所有设备后找到刚刚分出来的HFS+分区点击抹掉，格式选择APFS![显示所有设备](https://img-blog.csdnimg.cn/202011301829345.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
![选择APFS分区并抹掉](https://img-blog.csdnimg.cn/2020113018294821.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
之后关掉磁盘工具选择安装macOS并选择刚刚抹掉的磁盘![选择抹掉的磁盘](https://img-blog.csdnimg.cn/20201130183102473.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
之后会进入安装界面等待即可之后电脑会重启之后我们再次按F12选择到OpenCore，此时会多出来一个选项，选择macOS installer![重启后选择macOS installer](https://img-blog.csdnimg.cn/20201130183354503.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
然后会进入读条界面，读条完之后即可进入系统设置![读条](https://img-blog.csdnimg.cn/20201130183502944.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)

设置时记住不要登录AppleID，因为此时我们并没有注入三码，登录会有封appleid风险，选择稍后设置即可![AppleID登录界面](https://img-blog.csdnimg.cn/20201130183633126.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70)

设置完成后进入Catalina系统![Catalina](https://img-blog.csdnimg.cn/20201130183746217.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)

## 5. 将U盘中的EFI复制进硬盘
打开终端输入`diskutil list`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201130184501682.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
找到硬盘EFI分区也就是我们刚刚建立的ESP分区之后挂载，输入`sudo diskutil mount disk0s1`
之后打开finder，输入`open .`
此时我们可以看到Finder左侧已挂载硬盘EFI分区，将U盘中OC的EFI复制进去即可![复制EFI](https://img-blog.csdnimg.cn/20201130185204426.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
至此我们可以拔掉U盘重启F12即可选择Opencore引导
## 6. 注入三码
安装完后三码还未注入，此时我们用OpencoreConfigurator打开Config.plist文件后选择机型后生成保存即可![注入三码](https://img-blog.csdnimg.cn/20201130200123603.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)

# 使用情况

 - 4k显示，背光调节正常
 - 耳机，麦克风，摄像头
 - Wi-Fi 蓝牙 handoff airdrop
 - 触控板全手势支持，工作模式为GPIO中断
 - 电源管理，USB接口正常
 - 读卡器
 - type-c接口可以正常接U盘，接type-c扩展坞以太网卡、HDMI，DP工作正常外接显示器音频输出正常
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201130202309921.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201130202516371.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201130202530660.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201130202548771.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTc0OTc2OQ==,size_16,color_FFFFFF,t_70#pic_center)


