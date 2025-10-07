---
title: Docker Ghost修改默认首页地址localhost:2368
author: Feng
type: post
published: 2021-04-18T20:43:00+00:00
url: /it/606.html
hera_post_view:
  - 6
categories:
  - IT网络
tags:
  - Ghost

---
兜兜转转，晃一晃俺们又从 Typecho 转回 Ghost 了，倒不是 Typecho 不好，只是还是挺喜欢 Ghost 的风格，要是 Ghost 出个中文版的就好了（英文水平太 Low 了，没办法）。现在部署 Ghost 也比较简单，想省力可以直接 Docker 一下，分分钟就可以把 Ghost 搭建好，不过方便是方便，就是要修改 Ghost 配置、添加个啥的有点麻烦（我也还是个 Docker 新手，还有太多的不会），下面就来说说修改默认首页地址。

<!--more-->

这里以群晖 Docer 来演示，不会的时候也折腾了我许久，不把默认首页地址（也就是：localhost:2368）修改的话，很多链接调用就会出错，比如上传的图片等。群晖的 Docker 修改比较简单，直接在环境变量口中添加即可，如图：

<img decoding="async" src="https://blog.uu126.cn/usr/uploads/2021/04/3293710249.png#vwid=927&#038;vhei=535" alt="Ghost_docker.png" /> 

添加好之后记得重启一下容器，登陆后台随便上传个图片看看，就可以看到图片可以正常显示了。