---
title: linux nginx 网站访问提示502 Bad Gateway
author: Feng
type: post
published: 2014-02-24T13:18:38+00:00
url: /it/72.html
hera_post_view:
  - 6
categories:
  - IT网络

---
从日志报错分析，是php线程打开文件句柄受限导致的，解决办法：  
1、提升服务器的文件句柄打开打开  
vi /etc/security/limits.conf 底部加上

  * soft nofile 51200
  * hard nofile 51200  
    vi /etc/sysctl.conf  底部添加  
    fs.file-max=51200  
    2、提升nginx的进程文件打开数  
    vi /www/wdlinux/nginx/conf/nginx.conf  
    worker\_rlimit\_nofile 5120; 改成worker\_rlimit\_nofile 51200;  
    3、修改php-fpm.conf文件，主要需要修改2处。  
    vi /www/wdlinux/etc/php-fpm.conf  
    改成下面的值  
    <value name="max_requests">10240</value>  
    <value name="rlimit_files">51200</value>  
    4.设置php-fpm自动启动  
    vi /etc/rc.local 最后增加  
    /etc/init.d/php-fpm start  
    完成之后reboot重启下服务器  
    ulimit -n 查看