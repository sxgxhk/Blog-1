---
title: Windows 7系统开启AHCI 提升硬盘性能（亲测，不用重装系统）
author: Feng
type: post
published: 2012-11-29T02:28:10+00:00
url: /my/39.html
hera_post_view:
  - 5
categories:
  - 生活随笔

---
如今的电脑系统中，硬盘的性能已经成为影响整机表现的最大瓶颈。而在对配件要求较高的Windows7系统中，硬盘自然成为了需要优化的对象，而通过开启硬盘的AHCI模式，可以在一定程度上提升硬盘的性能。  
　　在通常的情况下，硬盘在BIOS中默认为原生IDE模式，以获得最好的兼容性。如果在此模式下安装了Windows7，再在BIOS中更改硬盘为AHCI模式，就无法进入系统，需要重新安装系统才行。有没有办法不用重装系统，就打开硬盘的AHCI模式呢？当然有！  
　　小贴士:什么是硬盘的AHCI模式？  
　　AHCI是串行ATA高级主控接口的英文缩写，它是Intel所主导的一项技术，它允许存储驱动程序启用高级SATA功能，如本机命令队列（NCQ）和热插拔。开启AHCI之后可以发挥SATA硬盘的潜在的性能，理论上大约可增加30%的硬盘读写速度。  
　　STEP1：在点击开机菜单后，选择菜单中的“运行”栏目。在运行栏目的输入框内键入“regedit”，回车即可打开注册表编辑器。

<p align="center">
  <img decoding="async" src="http://img.win7china.com/NewsUploadFiles/20100805_105243_151_u.jpg" alt="" />
</p>

<p align="center">
  输入“regedit”
</p>

　　STEP2：打开注册表编辑器之后，进入“HKEY\_LOCAL\_MACHINESystemCurrentControlSetServicesMsahci”键值。在右边窗口中双击名称为“Start”的项目，会弹出一个对话框，将默认的参数由3更改为0。点击“确定”并且保存之后，重新启动电脑。

<p align="center">
  <img decoding="async" src="http://img.win7china.com/NewsUploadFiles/20100805_105307_339_u.jpg" alt="" />
</p>

<p align="center">
  更改“Start”默认参数
</p>

　　STEP3：重启电脑之后，进入BIOS，在“Integrated Peripherals”页面中，将“SATA RAID/AHCI Mode”更改为“AHCI”（不同BIOS选项名称会有细微差别）。

<p align="center">
  <img decoding="async" src="http://img.win7china.com/NewsUploadFiles/20100805_105327_932_u.jpg" alt="" />
</p>

<p align="center">
  将“SATA RAID/AHCI Mode”更改为“AHCI”
</p>

<p align="center">
  保存重启，进入系统后系统会自动安装AHCI的驱动程序。安装好后系统会要求再次重启，重启之后，硬盘的AHCI模式就打开了。
</p>

<p align="center">
  <img decoding="async" src="http://img.win7china.com/NewsUploadFiles/20100805_105343_620_u.jpg" alt="" />
</p>

<p align="center">
  硬盘评分提升到了6.5，性能提升约20%<br /> 　　写在最后：硬盘在更改为AHCI模式之后，系统启动的速度变化不大。不过在进行大文件拷贝时，速度由原来的60MB/S提升到了71MB/S，性能提升约20%。硬盘在Windwos7中的系统评分中，也由开始的5.9分提升到了6.5分。由此可见硬盘开启AHCI之后，效果是不错的。
</p>