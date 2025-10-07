---
title: Windows 2008一键安装包配置环境：Windows+IIS+Php+Mysql
author: Feng
type: post
published: 2012-03-14T02:00:35+00:00
url: /it/20.html
hera_post_view:
  - 5
categories:
  - IT网络
tags:
  - word

---
<span style="font-weight: inherit; font-style: inherit;"><strong style="font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">集成包：</span></strong></span>  
IIS7组件、FTP7、php 5.5.7、mysql 5.6.15、phpMyAdmin 4.1.8、phpwind 9.0、ISAPI_Rewrite  
<span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><strong style="font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">安装包：</span></span></strong>  
32位和64位  
下载地址：<a href="http://oss.aliyuncs.com/aliyunecs/windows.zip?spm=5176.7150518.1996836753.5.6VfyUA&file=windows.zip" target="_blank" rel="noopener">一键安装包下载</a>  
安装包启动

<p style="color: #222222;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> <img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1QFBPFCdmXXcivD6F-503-3581.jpg" alt="" /></span></span>
</p>

<p style="color: #222222;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>点击“下一步”后，指定安装目录，默认使用C:websoft，然后点击“安装”。
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T14fR7FChhXXcivD6F-503-3581.jpg" alt="" />
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>开始将所需文件安装到指定目录。
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1g40QFuabXXcivD6F-503-3581.jpg" alt="" /></span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>安装IIS组件
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">弹出命令行窗口，开始安装iis组件（不包括FTP组件），大概需要5分钟。完成后按任意键继续。</span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span> <img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1l9SbFDdfXXbSpS2g-668-4311.jpg" alt="" />
</p>

<p style="color: #222222;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>安装PHP环境
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">配置php-cgi运行环境，并指定站点默认页为index.php。完成后按任意键继续。</span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> <img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1xWmbFEXcXXbSpS2g-668-4311.jpg" alt="" /></span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><strong style="font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">安装重定向Rewrite</span></span></strong>
</p>

<p style="color: #666666;">
  <strong style="font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span></strong>安装完后按任意键继续。
</p>

<h3 style="font-weight: inherit; color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> <img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1.wNWFwRnXXbSpS2g-668-4311.jpg" alt="" /></span></span>
</h3>

<p style="color: #666666;">
  安装mysql服务
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">服务会先执行stop执行，因为之前没有安装，所以stop会报错，不用理会。启动成功</span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">后继续安装所需的VC环境。</span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1UXeaFydlXXbSpS2g-668-4311.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>接着、将执行mysql初始化操作，并设置文件夹权限。
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1al5hFtpdXXbSpS2g-668-4311.jpg" alt="" />
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>然后，将在iis开始创建phpwind站点
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1dj0TFxtCXXbSpS2g-668-4311.jpg" alt="" />
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><span style="font-weight: inherit; font-style: inherit;">创建完成后，会打开浏览器，地址为</span><a style="font-weight: inherit; font-style: inherit; color: #666666;" href="http://localhost/index.php"><span style="font-weight: inherit; font-style: inherit; color: #0000ff;"><span style="font-weight: inherit; font-style: inherit;">http://localhost/index.php</span></span></a><span style="font-weight: inherit; font-style: inherit;">，开始安装phpwind。</span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1eWGfFrpdXXbSpS2g-668-4311.jpg" alt="" />
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>mysql的帐号和密码请查看安装目录下的account.log文件。
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1Ui48Fv8vXXbqMvs7-800-6001.jpg" alt="" />
</p>

<p style="color: #666666;">
   account.log文件将包含mysql和ftp的帐号信息。（这时因为ftp还没有安装完成，所以FTP帐号的密码还未生成，为默认值ftp_password，不必理会。）
</p>

<h3 style="font-weight: inherit; color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> <img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1cROkFsldXXcJdtsv-960-5611.jpg" alt="" /></span></span>
</h3>

<p style="color: #666666;">
  安装phpwind
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">浏览器中将打开phpwind安装向导，点击“接受”进入下一步。</span></span><span style="font-weight: inherit; font-style: inherit;"> </span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T10G9hFC4cXXaArzPn-781-6391.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>检测通过后，点击“下一步”。
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T15cuhFyBdXXbBI16x-785-7911.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>将安装目录下的account.log中的mysql密码复制粘贴到相应的“数据库密码”项中，并填写数据库名称，phpwind管理员admin的登录密码，然后点击“创建数据”按钮进入下一个环节。
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1A7mbFv4eXXapcPTn-778-6451.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>Phpwind安装程序开始自动在mysql中创建库、创建数据表。
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T104SeFxpdXXcEBNbs-783-6801.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>完成后直接进入phpwind登录页。至此，phpwind安装完毕。按任意键继续。
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T13DiaFCldXXbRwB.A-1107-5521.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>安装ftp服务
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1MS5uFwNfXXbSpS2g-668-4311.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">命令行将启动安装包，界面如下，点击“next”进行下一步操作。</span></span><span style="font-weight: inherit; font-style: inherit;"> </span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1UYxRFv8xXXXs6p3q-499-3851.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">将“I accept the ……”前的复选框勾选上，然后点击“next”。</span></span><span style="font-weight: inherit; font-style: inherit;"> </span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T17.J5FwBsXXXs6p3q-499-3851.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">不必修改安装项目，继续点击“next”。</span></span><span style="font-weight: inherit; font-style: inherit;"> </span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1gEJWFwlnXXXs6p3q-499-3851.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">设置完成后，点击“install”开始安装，直到安装结束。</span></span><span style="font-weight: inherit; font-style: inherit;"> </span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1z_JPFBNlXXXs6p3q-499-3851.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span><span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">ftp模块安装完成后，安装窗口自动关闭，命令行自动往下执行。开始配置ftp站点。</span></span><span style="font-weight: inherit; font-style: inherit;"> </span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1OdB4FqdpXXbSpS2g-668-4311.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>创建ftp用户，并将ftp站点的路径设置到phpwind的根目录，方便用户对站点进行更新维护。
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1AAabFtBgXXbSpS2g-668-4311.jpg" alt="" /></span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>设置ftp密码后并写入安装目录下的“account.log”文件中。按任意键继续。
</p>

<h3 style="font-weight: inherit; color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> <img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1eWuaFE4gXXcJdtsv-960-5611.jpg" alt="" /></span></span>
</h3>

<p style="color: #666666;">
  安装phpMyAdmin
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">phpMyAdmin的默认访问为8080，并在iis中创建站点和连接池。</span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1K9V5Fz0VXXbSpS2g-668-4311.jpg" alt="" /></span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>完成后按任意键将启动浏览器，打开phpMyAdmin站点，输入安装目录下account.log文件中的mysql帐号信息进行登录。
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1POB4FyFgXXb8E6QN-649-5581.jpg" alt="" /></span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>正确登录后，就能看到所有mysql中的数据库了。（包括之前命名的phpwind的数据库。）
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1KXB7FrhkXXXF_0_N-1258-6611.jpg" alt="" /> </span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> </span></span>至此，全部安装完毕。按任意键窗口自动关闭。
</p>

<h3 style="font-weight: inherit; color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"> <img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1QW48FDpiXXbSpS2g-668-4311.jpg" alt="" /></span></span>
</h3>

<p style="color: #666666;">
  安装完成
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;">打开IIS，查看所有部署的服务和站点内容。</span></span>
</p>

<p style="color: #666666;">
  <span style="font-weight: inherit; font-style: inherit;"><span style="font-weight: inherit; font-style: inherit;"><img decoding="async" style="font-weight: inherit; font-style: inherit;" src="http://uu126.cn/wp-content/uploads/2014/07/T1QZhTFyRkXXaW.U_5-835-7301.jpg" alt="" /></span></span>
</p>