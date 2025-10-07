---
title: Memcached缓存清空办法
author: Feng
type: post
published: 2015-01-11T06:58:38+00:00
url: /it/195.html
hera_post_view:
  - 3
categories:
  - IT网络

---
用了Wordpress也蛮长时间了，期间各种缓存插件也用过不少，因为不是高手，所以大部分都是在抄作业，结果时间一长也就忘了差不多了，就像这次服务器一换，结果又得重新去“翻书”，把Memcached又重新启用了（忘了之前为什么关闭了），结果麻烦来了，object-cache.php文件一上传，整个博客就出错，其实就是变成以前用的主题样子，没有了CSS文件那种难看的样子可想而知了。好吧，那么怎么把这个缓存给清空掉呢？显然清理IE浏览器的缓存是徒劳的，因为没上传这个文件之前都是OK的，所以只能去清理Memcached里的缓存，这个还是只能找我师傅的师娘——百度来搞定。方法如下：

<div class="alert alert-info">
  使用Putty连接服务器，登录后开始输入命令： telnet localhost 11211
</div>

[<img loading="lazy" decoding="async" class="alignnone size-full wp-image-1353" src="http://uu126.cn/wp-content/uploads/2015/01/memcached.jpg" alt="memcached" width="670" height="420" />][1]

<div class="alert alert-info">
  然后再输入：flush_all
</div>

<div class="alert alert-info">
  等显示“OK”后，再输入：quit
</div>

输完这些，直接刷新博客，哈哈，正常显示了！

 [1]: http://uu126.cn/wp-content/uploads/2015/01/memcached.jpg