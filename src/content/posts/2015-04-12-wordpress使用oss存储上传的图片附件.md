---
title: Wordpress使用OSS存储上传的图片附件
author: Feng
type: post
published: 2015-04-12T13:50:59+00:00
url: /it/231.html
hera_post_view:
  - 8
categories:
  - IT网络
tags:
  - OCS
  - 服务器
  - 阿里云

---
<span style="font-family: Arial;">使用<span id="rlt_2">阿里</span>云<span id="rlt_3">ECS</span>有一段时间了，一直想使用一下OSS，但是每次一想到使用OSS需要用Java/Python等编程语言，刚涌上来的热情就冷却一半了。最近在论坛里面看到有人说可以把OSS变成ECS的硬盘来用，抱着试试的想法，私信联系了一下，<span id="rlt_9">安装</span>到ECS上，真的可以把OSS变成ECS的盘，好东西不敢藏私，刚好又是<span id="rlt_1">阿里云</span>分享月，赶紧写出来给大家共享。</span>  
<span style="font-family: Arial;">首先下载软件，登陆www.cloudtalkers.com，进入下载页面，里面有软件安装包和指导书，现在官方只提供了Ubuntu和CentOS的版本，我的ECS是Ubuntu 14.04，刚好有对应的版本：</span>  
[<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-1687" src="http://uu126.cn/wp-content/uploads/2015/04/Fid_211-211_1415218023534054_d7902f5b82f7343.png" alt="Fid_211-211_1415218023534054_d7902f5b82f7343" width="747" height="256" />][1]  
<span style="font-family: Arial;">然后按照<span id="rlt_5">操作</span>指导书安装软件，软件安装很快，只要解压缩就可以了，<span id="rlt_4">配置</span>文件稍微麻烦一些，还好官方的指导书还比较详细，同时在官方群里面咨询了一下，也顺利的安装好了。</span>  
<span style="font-family: Arial;">配置完成后，启动运行，测试拷贝几个文件过去，又到OSS控制台上一看，真的可以哦。</span>  
**<span id="rlt_6">Linux</span>下目录<span id="rlt_7">信息</span>：**  
[<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-1688" src="http://uu126.cn/wp-content/uploads/2015/04/Fid_211-211_1415218023534054_0ee9eceef2e983c.png" alt="Fid_211-211_1415218023534054_0ee9eceef2e983c" width="577" height="99" />][2]**OSS控制台：**  
[<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-1689" src="http://uu126.cn/wp-content/uploads/2015/04/thumb-Fid_211-211_1415218023534054_4e9793d7591cb57.png" alt="thumb-Fid_211-211_1415218023534054_4e9793d7591cb57" width="990" height="202" />][3]<span style="font-family: Arial;">这下可以把OSS当成一个超级大硬盘来使用了。</span>  
<span style="font-family: Arial;">在官方的群里面跟软件作者也Q聊了一下，他们软件的原理是利用Linux的FUSE框架，把OSS存储虚拟成Linux的本地盘。另外了解到他们的软件正在申请进入阿里云<span id="rlt_10">工具</span>市场，进入市场后可能会收费。不过现在使用的用户全部<span id="rlt_8">免费</span>，真心要赞一个。就当给他们做个广告吧，有需要的同学们赶紧去下哦。</span>  
一切就绪后，开始Wordpress了，<span style="font-family: 宋体;">将wordpress上传目录设置为cloudfs的挂载目录，我的目录是/home/wordpress/wp-content/uploads，登陆WORDPRESS，給媒体库增加几个图片：</span>  
[<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-1690" src="http://uu126.cn/wp-content/uploads/2015/04/Fid_211-211_1415218023534054_2b43ef74e4e2b1c.png" alt="Fid_211-211_1415218023534054_2b43ef74e4e2b1c" width="757" height="228" />][4]  
到OSS对应的BUCKET看下结果，<span id="rlt_3">上传</span>的文件全部都在OSS里面了：  
[<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-1691" src="http://uu126.cn/wp-content/uploads/2015/04/thumb-Fid_211-211_1415218023534054_c24713de10407ff.png" alt="thumb-Fid_211-211_1415218023534054_c24713de10407ff" width="990" height="585" />][5]  
我又看了一下我的ECS磁盘，的确本地磁盘没有增加使用，这个东东看起来不错，向大家推荐一下，更重要的是现在<span id="rlt_6">免费</span>，<span id="rlt_7">安装</span>使用有问题还有人支持。  
&nbsp;  
<span style="color: #ff0000;">注：文章转载自阿里云论坛，原文链接：<a href="http://bbs.aliyun.com/read/236273.html?spm=5176.7189909.0.0.c5QktS">http://bbs.aliyun.com/read/236273.html?spm=5176.7189909.0.0.c5QktS</a></span>

 [1]: http://uu126.cn/wp-content/uploads/2015/04/Fid_211-211_1415218023534054_d7902f5b82f7343.png
 [2]: http://uu126.cn/wp-content/uploads/2015/04/Fid_211-211_1415218023534054_0ee9eceef2e983c.png
 [3]: http://uu126.cn/wp-content/uploads/2015/04/thumb-Fid_211-211_1415218023534054_4e9793d7591cb57.png
 [4]: http://uu126.cn/wp-content/uploads/2015/04/Fid_211-211_1415218023534054_2b43ef74e4e2b1c.png
 [5]: http://uu126.cn/wp-content/uploads/2015/04/thumb-Fid_211-211_1415218023534054_c24713de10407ff.png