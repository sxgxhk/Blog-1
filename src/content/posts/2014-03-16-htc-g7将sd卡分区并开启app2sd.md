---
title: HTC G7将SD卡分区并开启APP2SD+
author: Feng
type: post
published: 2014-03-16T02:22:39+00:00
url: /it/91.html
hera_post_view:
  - 9
categories:
  - IT网络

---
在刷机过程中遇到无限多次重启的情况，可以先把手机关机。然后先按住音量-再按开机键。之后选择CLEAR STORAGE(音量键控制上下。开机键确定）再按音量+的那个键恢复出厂设置就好了。不过你原来手机里的东西就都没了。刷ROM准备：  
建议用Recovery_v5.0.2.3或更高版本的Recovery刷机（中文版Recovery下载，请点击：<a href="http://www.cr173.com/soft/36072.html" target="_blank" rel="noopener">下载地址</a>）。 刷机前请务必进行清空数据和缓存，本Recovery为中文版小房子为【向上按键】 MENU为【向下按键】 返回为【返回按键】 搜索为【确定按键】)  
刷入系统后，请等待2-3分钟，开机时间会比较长，请耐心等待。  
一定要进入系统后再进行APP2SD+否则容易造成开不了机。  
一定要确保有一张优质的SD卡，卡的好坏关系到系统速度。SD卡未分区进不了系统。  
APP2SD+教程：  
1.首先进入recovery对SD卡进行分区，在recovery里面选择 高级—>SD卡分区—>Ext大小选择512M或者1024M(看个人选择，你的应用都是装这里了，本人用1024M)—>swap选择0然后分区，分区会格式化清空你的SD卡，所以你一定要把SD卡里面的重要资料移出来备份，切记切记  
2.分区完毕后，你的SD卡应该是一片空白，把ROM和G7app2sd+补丁包放入SD卡里面。  
3.“从SD卡选择更新”先刷ROM包（此ROM包须支持APP2SD，一般在其下载说明里会提到），然后直接刷app2sd+补丁包。  
4.重启系统进入系统，重启可能会卡顿几次比较久，请耐心等待。  
5.下载超级终端adb.zip（点击<a href="http://dl.dbank.com/c0ipy7oqle" target="_blank" rel="noopener">下载地址</a>），把压缩包里面的3个文件直接放在C盘WINDOWSsystem32目录里  
6.手机的菜单里选择设置-应用程序-开发-USB调试打勾，连接PC端选择磁盘驱动器  
7.在PC桌面点击菜单→运行→输入“cmd”进入命令行界面  
8.输入以下指令，每次输入一个都要打回车，且输入一个结束后耐心等待  
adb shell 进入超级终端  
su  
a2sd check  
a2sd reinstall  
手机重启，  
adb shell  进入超级终端  
a2sd check  
a2sd cachesd等待手机重启，  
重启后继续进入“超级终端”。  
adb shell  
a2sd lowmem-optimum（让内存管理达到最佳状态）  
a2sd datasd   （ 移动/data/data下文件到sd卡）  
9.成功了!享受你的成果吧!<wbr />