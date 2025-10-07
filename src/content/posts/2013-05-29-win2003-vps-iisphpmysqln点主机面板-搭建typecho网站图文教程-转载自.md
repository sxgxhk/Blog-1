---
title: Win2003 VPS IIS+PHP+MYSQL+N点主机面板 搭建Typecho网站图文教程！（转载自味道网）
author: Feng
type: post
published: 2013-05-29T03:26:26+00:00
url: /it/64.html
hera_post_view:
  - 4
categories:
  - IT网络

---
Win2003 VPS IIS+PHP+MYSQL+N点主机面板 搭建Typecho网站图文教程(新手必看)！  
有不少朋友买了WIN VPS后不知道怎么弄网站，今天我就来详细图文解说下 Win2003 VPS 利用 IIS+PHP+MYSQL+N点主机面板来搭建Typecho网站图文教程：

<!--more-->

**一、准备工作：**  
1，从VPS服务商那里获得 IP(购买后服务商分配给你) 、administrator密码(VPS管理面板里提供) ,确保你的VPS系统为 Windows 2003 ，其他系统请绕行。如果不是请进入VPS管理面板重新做系统。  
2，利用远程桌面连接到你的WIN主机中，进入后，VPS主机商一般都会把IIS安装好的，并且会在桌面直接显示 tool 文件夹，里面有需要的软件，如果没有请自行下载，或者和你的VPS主机商索要。  
需要准备的软件：

> 3389x.rar # 用于修改远程端口  
> zkeysphp.rar #用于直接在IIS下安装PHP+MYSQL+PHPMYADMIN（前提：IIS先装好。）  
> ServU6.4.rar #FTP软件  
> ISAPI\_Rewrite\_Full.rar #IIS环境下支持的httpd.ini伪静态插件  
> SQL2000+sp4.rar #支持asp.net的mssql数据库和SP4补丁  
> N196.msi #N点主机管理面板软件

> 以上软件打包下载：<a href="http://weidao.net/iis.html" target="_blank" rel="noopener">http://weidao.net/iis.html</a>

3，远程进入桌面后，首先要修改VPS密码，点击 “我的电脑” 右键 “管理” &#8211; “系统工具” &#8211; “本地用户和组” &#8211; “用户” 第一个就是 administrator ，你可以点击右键进行修改密码。  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11013.jpg" />  
4，刚拿到的VPS只有系统C分区，这个时候要扩展你额外的磁盘分区：继续 点击 “储存” &#8211; “磁盘管理” &#8211; 右键 未指派的 空间（图中是19.99G）- “新建磁盘分区” 。  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11014.jpg" />  
直接下一步，直到下图所示，选择 “执行快速格式话” 打勾，下一步，完成即可。  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11015.jpg" />  
OK，完成后，如图所示：  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11016.jpg" />  
在我的电脑里面也出现了D盘分区：  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11017.jpg" />  
**二、安装环境：（绝大多数VPS服务商都会安装好IIS的，如果没有自行解决。）**  
1，打开桌面 tool 文件夹，所有文件解压如图所示：  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11018.jpg" />  
2，打开 3389x.rar ，自行修改远程端口，记得开启远程桌面打勾，主机重启后记得加上你修改的端口即可。  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11019.jpg" />  
3，打开 zkeysphp.rar ，安装 IIS 下 PHP+MYSQL+PHPMYADMIN 一键安装包，直接下一步知道完成。  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11020.jpg" />  
安装完成后，立刻在自己的电脑中输入网址 http://IP:999/index.php 进入 PHPMYADMIN 修改 MYSQL root 密码 （默认密码为：zkeys），你可以进入IIS管理中心，看到下图所示：  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11021.jpg" />  
4，打开 ServU6.4.rar 安装 FTP 软件，先安装 英文原版，然后安装 汉化包 。记得要先开个FTP账户，不然N点主机管理面板用不起来。  
4-1，确保FTP软件安装在非系统分区里，我这里是D盘：（N点主机配置需要用的）  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11022.jpg" />  
4-2，汉化包安装后，根据提示一步一步进行安装，全部安装完成后，运行 keygen.exe 注册机，注册过后就是无限用户了。  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11023.jpg" />  
5，安装 ISAPI\_Rewrite\_Full.rar 全功能版伪静态组件，安装后需要注册，序列号压缩包中含有。  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11024.jpg" />  
6，安装 SQL2000+sp4.rar ，详细安装步骤：<a href="http://www.weidao.net/1495.html" target="_blank" rel="noopener">http://www.weidao.net/1495.html</a>  
7，重启WIN VPS后，确认右下角FTP、MSSQL 任务栏小图标已经开启，没有红叉叉。  
到这里为止，IIS+PHP+MYSQL+PHPMYADMIN+FTP+IIS全功能伪静态(httpd.ini) 已经安装完成。下面就来安装 N点主机管理面板，将上面的所有东东全部绑定到面板里面，这样可以方便我们操作。  
**三、安装面板：**  
1，运行 N点主机管理面板软件 ，记得把软件安装到非系统盘（一般都是D盘），直接点击安装完成即可。  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11025.jpg" />  
2，双击桌面 “N点主机配置工具”，如图所示，输入加密字符，点击 “设置” ，完成后会提示你后台地址和密码。  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11026.jpg" />  
3，打开你电脑的浏览器，输入地址登陆配置，如果无法访问，进入VPS打开IIS管理中心 &#8211; “Web 服务扩展” &#8211; 右侧 “Active Server Pages” &#8211; “允许”如图所示：  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11027.jpg" />  
4，登陆N点主机管理后台，左侧 “总管理员设置”迅速修改密码。  
5，面板左侧，“空间存放路径设置” 如图：  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11028.jpg" />  
6，面板左侧，“主机系统参数设置”，这个是关键：

> 6.1，服务器IP地址：填写你的VPS IP地址；  
> 6.2，FTP服务软件：Serv-U 6.4  
> 6.3，默认文档：添加个 default.asp  
> 6.4，Serv-U/G6 安装路径：D:Serv-U（就是刚才你安装时候的路径）  
> 6.5，MSSQL 管理员密码：就是你自己设置的sa密码  
> 6.6，MYSQL 数据存放路径：D:ZkeysSoftMySqlMySQL Server 5.1data （zkeys你安装的是D盘吗）  
> 6.7，MYSQL 管理员密码：就是你自己设置的root数据库密码

点击 “修改配置”，OK，搞定。  
**四，开设网站：**  
1，进入N点管理面板左侧，点击 “站点虚拟主机开设”如图：  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11029.jpg" />  
浏览你开通的域名，恭喜你的虚拟主机已经开通了。  
2，接着开通MSSQL和MYSQL，这个比较简单。  
3，直接输入IP，你会看到主机登陆页面，在这里你可以自由的管理你刚才开通的主机空间和数据库了。  
4，下载TYPECHO博客程序(官方地址：<a href="http://typecho.org/" target="_blank" rel="noopener">typecho.org</a>)，解压后打包成 typecho.rar 上传到你的FTP空间 web 文件夹中。  
5，进入主机面板，点击“在线解压文件”如图所示：  
<img decoding="async" alt="" src="http://www.weidao.net/images/2012/11030.jpg" />  
6，输入你绑定的域名，现在开始安装TYPECHO吧！