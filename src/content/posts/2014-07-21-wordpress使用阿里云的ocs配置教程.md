---
title: Wordpress使用阿里云的OCS配置教程（已更新）
author: Feng
type: post
published: 2014-07-21T14:28:00+00:00
url: /it/149.html
hera_post_view:
  - 7
categories:
  - IT网络
tags:
  - OCS
  - Wordpress
  - 阿里云

---
更新一下，使用现在的OCS免密码访问功能，可以方便的实现Wordpress使用OCS，使用方法如下：  
先申请后开启无密码访问，然后把你ECS 内网IP放入白名单之中，让只有你的内网IP才可以访问，接着在wp-config.php中加入如下代码：

global $memcached_servers;  
$memcached_servers = array(‘default‘ => array(‘你的内网地址:11211’));

之后访问几个页面，可以看到对象已经成功到OCS了。  
最近阿里云有点火呀，先是推出6个月的免费ECS试用，接着RDS也紧随其后，这不OCS都推出了128M免费版了，只要你是阿里云ECS的用户且经通过了实名认证，就可以申领一个免费的128MOCS（当然这好东西只能领一个哦），OCS之前我也没接触过，原先是价格高加上就俺们这个小站几乎没有什么收入来源，建站也只是自己的个人爱好而已，但现在有了免费的自然要来享受一下，这好丰富的免费午餐岂能放过。本站的博客就是运行在ECS+RDS+OCS之上，下面来说一下OCS的配置教程（转自阿里云论坛的，本人也是亲自测试过），教程如下：

首先到阿里云 OCS   购买OCS服务，购买成功你到控制台进入OCS获取内网地址，端口一般都是memcached默认的11211，实例ID也就相当于账号，还有密码。这些信息会应用在下面的配置中。

下面提供需要的文件。  OCS.zip (12 K) ，解压文件把advanced-cache.php，MemcacheSASL.php，object-cache.php上传到你的站点/wp-content/目录 把batcache.php上传你的/wp-content/plugins/插件目录 这里需要配置的文件是object-cache.php按如图配置。  

原教程地址：[<https://bbs.aliyun.com/read/156942.html>][1]

原教程上还列出了其它插件的使用，因为本人博客站点也没有使用memcached，帮就直接按上面的方法进行相应的修改和上传，已经运行了几天，感觉上是比以前要快一点，不知道是不是心理作用（小站访问流量小，作用起来不是很明显），如果站点流量比较大的话，那OCS的作用会比较明显，就如同RDS一样，当然了我还会持续观察下去，各位朋友也可以就自己的访问速度留个言提点意见。

&nbsp;

 [1]: https://bbs.aliyun.com/read/156942.html