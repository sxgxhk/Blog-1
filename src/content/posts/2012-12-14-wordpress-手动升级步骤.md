---
title: WordPress 手动升级步骤
author: Feng
type: post
published: 2012-12-14T09:48:04+00:00
url: /it/46.html
hera_post_view:
  - 4
categories:
  - IT网络

---
### WordPress 手动升级步骤：

第一步、建议备份程序文件和数据库（虽然一般情况下不会丢失，但丢失了就麻烦了）。  
第二步、手动升级 WordPress 之前最好先登录后台关闭所有插件，当然不关闭影响也不大，不过全部关闭要好点。  
第三步、到 WordPress 官方网站下载最新的 WordPress 版本程序。  
第四步、FTP登录后建议先在博客根目录下建一个文件夹（如名为：old），接着将网站根目录下所有文件除wp-content文件夹（里面放的是主题文件，插件文件等）、静态文件http.ini、wp-config.php（wp-config.php文件是wp配置文件，包括数据库连接设置等）外全部移动到刚才建立的old文件里，解压刚下载的程序安装包，把安装包除了刚才排除的那三个（wp-content文件夹、http.ini、wp-config.php）全部上传到空间里。  
第五步、上传完毕后，在地址栏里输入：“<http://你的博客地址/wp-admin/upgrade.php”，升级一下数据库，wordpress就算升级完成了>。