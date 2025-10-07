---
title: CentOS配置web服务器流程挂载、ftp、apache、mysql、二级域名
author: Feng
type: post
published: 2014-12-21T08:19:40+00:00
url: /it/183.html
hera_post_view:
  - 4
categories:
  - IT网络
tags:
  - CentOS
  - 阿里云

---
刚在阿里云论坛里看到了好东西，一定要把它“记”下来，方便自己、方便大伙哈！  
原文如下：  
<span style="font-size: large;"><span style="font-family: 微软雅黑;"><b>一．挂载系统盘</b></span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">1.执行 fdisk -l 命令，发现没有 /dev/xvdb1 标明您的<span id="rlt_7">云服务</span>无数据盘</span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">2.fdisk /dev/xvdb  命令，对数据盘进行分区</span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">3.依次输入“n”，“p”“1”，两次回车，“wq”（保存），分区就开始了</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">4.使用“fdisk -l”命令可以看到，新的分区xvdb1已经建立完成了。</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">5.mkfs.ext3 /dev/xvdb1 格式化新分区</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">6.通过vi编辑器修改写入新分区信息，vi /etc/fstab</span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">  修改的内容为：</span></span>

> [<img loading="lazy" decoding="async" class="alignnone size-full wp-image-1304" src="http://uu126.cn/wp-content/uploads/2014/12/Fid_207-207_1968974297916064_e2e06549617089c.png" alt="Fid_207-207_1968974297916064_e2e06549617089c" width="697" height="117" />][1]

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">  </span></span><span style="font-size: medium;"><span style="font-family: 微软雅黑;">  vi编辑器命令： i：启动键盘输入  Esc键：退出编辑模式  :wq 保存并退出</span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">7.然后使用  cat /etc/fstab 命令查看，出现 /dev/xvdb1  /mnt ext3 信息表示写入成功</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">8.使用  mount -a  命令挂载新分区</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">9.用  df -h  命令查看</span></span>

<span style="font-size: large;"><span style="font-family: 微软雅黑;"><b>二．在<span id="rlt_9">Linux</span>系统根目录下创建<span id="rlt_1">网站</span>目录</b></span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">[root@iZ235hqjjjlZ ~]# cd /              (返回系统根目录)</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">[root@iZ235hqjjjlZ /]# mkdir web</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">[root@iZ235hqjjjlZ /]# cd web</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">[root@iZ235hqjjjlZ web]# mkdir eoair</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">[root@iZ235hqjjjlZ web]# mkdir eoccc    </span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">目录结构：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">+ web</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">  &#8211; eoair</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">  &#8211; eoccc</span></span>

<span style="font-size: large;"><span style="font-family: 微软雅黑;"><b>三．安装vsftp，并<span id="rlt_4">配置</span>帐号依次分派到网站ftp目录中</b></span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">1.cd /   返回到系统根目录</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">2.ps -ef|grep vsftpd 判断是否暗转了vsftpd</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">  返回 root      1039   958  0 22:12 pts/0    00:00:00 grep vsftpd 表示未安装</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">2. yum install vsftpd -y  安装vsftpd</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">3. 编辑配置文件 vim /etc/vsftpd/vsftpd.conf </span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">  anonymous_enable=YES  改为  ON</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">4.chkconfig &#8211;level 35 vsftpd on  将ftp服务加入到系统<span id="rlt_3">自</span>启动</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">   vsftpd          0:off   1:off   2:off   3:on    4:off   5:on    6:off   35项为on表示完成</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">5. cd /web/   进入网站目录</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">6. useradd eoairftp -s /sbin/nologin -d /web/eoair/   将ftpeoair 用户权限加入到 web下eoair下</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">7. passwd eoairftp  设置ftpeoair用户的密码，输入两次</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">8. chown eoairftp eoair  将用户权限加入到文件中</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">  ls -lrst   查看是否成功</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">  drwxr-xr-x 2 eoairftp root 4096 Dec 18 22:11 eoair   表示添加成功</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">9.service vsftpd start    开启vsftp服务</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">好了 现在可以通过 eoairftp 用户名 <span id="rlt_6">上传</span>文件到  web/eoair</span></span>

<span style="font-size: large;"><span style="font-family: 微软雅黑;"><b>注：添加另一ftp帐号和对应目录 eoccc</b></span></span>**ftp** **-> /web/eoccc**

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">1.cd web  加入网站目录    mkdir eoccc   创建api目录</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">2.useradd eoapiftp -s /sbin/nologin -d /web/eoccc/   将eoapiftp 用户权限加入到 web 下eoccc下</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">3. passwd eoapiftp  设置eoairftp用户的密码，输入两次</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">4. chown eoapiftp eoccc  将用户权限加入到文件中</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">5. service vsftpd restart 重启vdftpd</span></span>

<span style="font-size: large;"><span style="font-family: 微软雅黑;"><b>四．安装apache 和 <span id="rlt_8">php</span></b></span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">1.yum install httpd -y  由于 CentOS 已经封装了 Apache，直接运行安装</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">2. chkconfig &#8211;levels 235 httpd on  配置系统让 Apache 随系统启动</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">3. chkconfig &#8211;list  确认 Apache 235为on</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">4. yum install php -y  安装 PHP</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">5. service httpd restart   重启apache服务器</span></span>

<span style="font-size: large;"><span style="font-family: 微软雅黑;"><b>五．设置网站子站点对应的目录</b></span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">www.eoair.com -> /web/eoair   ccc.eoair.com -> /web/eoccc</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">1.vim /etc/httpd/conf/httpd.conf  编辑配置：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">   #LoadModule rewrite_module modules/mod_rewrite.so”这行，去掉前面的“#”</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">   查找所有“AllowOverride None”，修改为“AllowOverride All”</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">   在文件最后输入以下语句：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">       RewriteEngine on</span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">　　RewriteMap lowercase int:tolower</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">　　RewriteMap vhost txt:/etc/httpd/<span style="text-decoration: underline;">vhost.map</span></span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">　　RewriteCond ${lowercase:%{SERVER_NAME}} ^(.+)$</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">　　RewriteCond ${vhost:%1} ^(/.*)$</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">　　RewriteRule ^/(.*)$ %1/$1</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">2.新建一个<span style="text-decoration: underline;">vhost.map</span>文件：vim /etc/httpd/vhost.map 写入二级<span id="rlt_2">域名</span>目录指向</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">eoair.com /web/eoair    </span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">www.eoair.com /web/eoair</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">ccc.eoair.com /web/eoccc</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">3.最后 重启Apache </span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">  service httpd restart</span></span>

<span style="font-size: large;"><span style="font-family: 微软雅黑;"><b>六．安装 mysql</b></span></span>

> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">首先来进行 MySQL 的安装。打开超级终端，输入：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">[root@localhost ~]# yum install mysql mysql-server</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">安装完毕，让 MySQL 能够随系统自动启动：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">[root@localhost ~]# chkconfig &#8211;levels 235 mysqld on</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">[root@localhost ~]# /etc/init.d/mysqld start</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">设置 MySQL 数据 root 账户的密码：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">[root@localhost ~]# mysql_secure_installation</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">当出现如下提示时候直接按回车：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">Enter current password for root</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">出现如下输入Y再次回车：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">Set root password? [Y/n]</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">出现如下提示输入你需要设置的密码，回车后在输入一次确认：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">New password:</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">接下来还会有四个Y确认，分别是：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">Remove anonymous users? [Y/n]Disallow root login remotely? [Y/n]Remove test database and access to it? [Y/n]Reload privilege tables now? [Y/n]</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">重启</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">[root@localhost ~]# /etc/init.d/mysqld restart</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">注：让mysql支持外网连接图形化界面</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">将 msql <span id="rlt_5">数据库</span>中的user表中的 Host 字段修改为 % </span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">1. 首先连接mysql数据库： mysql -p3306 -uroot -p123456  出现 mysql-> 表示连接成功</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">2. 选择mysql配置数据库 use mysql; 显示Database changed 表示成功</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">3.  update user set  Host=&#8217;%&#8217; where Host=&#8217;localhost&#8217;;   修改Host 为%</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">4.  select Host,User,Password from user;  查询修改后的结果：</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">      +&#8212;&#8212;&#8212;&#8211;+&#8212;&#8212;+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-+</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">      | Host      | User | Password                                  |</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">      +&#8212;&#8212;&#8212;&#8211;+&#8212;&#8212;+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-+</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">      | %         | root | *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 |</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">出现  %  表示成功</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">5.  重启mysql服务 ： service mysqld restart</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">5.  最后使用图形管理测试连接</span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">注：如果需要修改mysql用户名可以使用 </span></span>  
> <span style="font-size: medium;"><span style="font-family: 微软雅黑;">update user set  User=&#8217;eoaroot&#8217; where User=&#8217;root&#8217;;</span></span>

注：本文转载自阿里云论坛

 [1]: http://uu126.cn/wp-content/uploads/2014/12/Fid_207-207_1968974297916064_e2e06549617089c.png