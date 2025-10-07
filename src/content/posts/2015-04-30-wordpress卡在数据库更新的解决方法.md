---
title: Wordpress卡在数据库更新的解决方法
author: Feng
type: post
published: 2015-04-30T13:26:34+00:00
url: /it/240.html
hera_post_view:
  - 5
categories:
  - IT网络
tags:
  - Wordpress

---
本人玩Wordpress以来每次更新都是自己手动上传的（都没在线升级成功过），这次奇怪了竟然能在线更新到4.2了，不知道不是停用了一些插件的缘故，还是阿里云又把XXX改运过了（应该不是，我在阿里云论坛有看到过可以在线升级成功过的，不过我比较悲催而已），不过程序倒是在线更新成功了，可第二天却发现了个问题，就是登陆后台后始终卡在更新数据库界面：  
[<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-1743" src="http://uu126.cn/wp-content/uploads/2015/04/wordpress05130100_2345.jpg" alt="wordpress05130100_2345" width="838" height="402" />][1]  
每次点完继续就跳转到首页，接着点仪表台又跳这个，再点又跳首页，如此反复循环着。本站目前是使用阿里的ECS+OCS+RDS，本机当然也启用了Memcached，在度娘里寻了寻，有说更改缓存文件名啥的，但我觉得这个不太靠谱，毕竟我还是要用的呀，看来还是得采纳清空缓存的方法（这里说明一下，那些改文件权限的，我没去试过，出于安全考虑，不敢给予太高的777权限），先清空了Memcached缓存（具体方法看我之前的博文：<a href="http://uu126.cn/post/1352.html" target="_blank" rel="noopener"><a href="http://uu126.cn/post/1352.html">http://uu126.cn/post/1352.html</a></a>），清空掉之后还是不行，看来还有个地方也需要清理一下，那就是阿里云的OCS，这个简单登录后台直接点击右上方的“清空实例缓存”，再刷新一下网页看看，是不是可以正常进入仪表盘了，哈哈，又可以写文章了！

 [1]: http://uu126.cn/wp-content/uploads/2015/04/wordpress05130100_2345.jpg