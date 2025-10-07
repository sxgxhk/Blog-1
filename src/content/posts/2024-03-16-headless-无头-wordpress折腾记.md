---
title: Headless（无头）WordPress折腾记
author: Feng
type: post
published: 2024-03-16T18:10:37+00:00
url: /it/835.html
hera_post_view:
  - 13
categories:
  - IT网络
tags:
  - Wordpress

---
什么是Headless WordPress？  
无头WordPress是一个术语，指的是任何使用WordPress作为后端软件来管理数据和内容，但使用单独的技术在前端显示数据的网站。后端是用于网站管理区域的术语。您可以在此处创建帖子和页面等内容、安装插件、管理评论等。

<!--more-->

<img decoding="async" src="https://api.uu126.cn/wp-content/uploads/2024/03/headless-wordpress-explained-og.png" alt="" /> 

很早以前在“我爱水煮鱼”网站看到无头Wordpress里（[链接][1]），感觉这玩意挺好玩的，但一直都没去折腾，据说他这个是纯PHP+Memcached来实现的，最近也不知道咋的，也在看Hugo和这个无头Wordpress,前者还没搞定，按空白大佬的那套俺们还没整会，记得以前整Hugo或Hexo时，都是要在本地搭环境，然后写文章再生成再PUSH到站点（Github或VPS等等），但现在直接可以把源文件MD直接扔给Github Action后由其生成并PUSH到站点（也有可能是我理解错了，反正我没整好）。扯远了，既然Hugo没整好那就整无头Wordpress吧，等有思路了再去整Hugo，这次整无头Wordperss都是在ChatGpt4的帮助下搞的，几乎全程代码都是由它写，我嘛就直接抄抄改改，谁叫我是老白呀（我对老白的定义就是：比小白强那么一点点，但也不精通等），用过Html和PHP都能成功调取，其中Html版分布（页码或上下页都正常），但Html不能用Memcached来缓存（至少那个ChatGpt是这么说的，因为Html本身就是静态文件嘛），用PHP来整的话，加上Memcached后，分页功能一直都没整好还得再研究。

<img decoding="async" src="https://api.uu126.cn/wp-content/uploads/2024/03/headless-wordpress-explained-og-2.png" alt="" /> 

不过不管是Html还是PHP,目前调用都是没问题，首页或文章页都能正常显示（美化嘛就算了，只是弄了自适应加一点点CSS修饰），如果后续有时间的话再折腾折腾，也有可能就此终止，谁让我爱折腾呢，这不我除了折腾这个，还早早的又在折腾xLog了，号称书写在 区块链 上的 开源 创作社区（[介绍在此][2]），当然还有我的区块链博客地址：[blog.057000.xyz][3]，都是搬运过去的，有兴趣的可以去注册一个。

 [1]: https://blog.wpjam.com/article/headless-wordpress/ "链接"
 [2]: https://xlog.app/about "介绍在此"
 [3]: https://blog.057000.xyz/ "blog.057000.xyz"