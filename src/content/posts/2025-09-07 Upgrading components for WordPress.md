---
title: 为Wordpress升级组件
published: 2025-09-07
updated: 2025-09-07
description: '自从偷懒不想手搓后，便用上BT面板，发现确实是省力不少，不管是配置或升级环境，还是整个计划任务或插件啥的，那简直就是点点点，木啥难度，这不听说Wordpress喜欢8以上版本（如PHP、Mysql等），想想要不咱也来一下，PHP倒是简单直接安装即可'
image: ''
tags: [网站]
category: 'IT网络'
draft: false 
---

自从偷懒不想手搓后，便用上BT面板，发现确实是省力不少，不管是配置或升级环境，还是整个计划任务或插件啥的，那简直就是点点点，木啥难度，这不听说Wordpress喜欢8以上版本（如PHP、Mysql等），想想要不咱也来一下，PHP倒是简单直接安装即可（相关的扩展也是要安装的，如opcache、memcached等），但是在版本切换里却傻了（BT版本不够高，不想升级），好在也有解决方案，可以自定义，然后在后面输入：unix:/tmp/php-cgi-84.sock

<img class="alignnone size-full wp-image-1596" src="https://image.uu126.cn/wp-content/uploads/2025/09/20250907000044522.webp" alt="" width="820" height="454" />

<img class="alignnone size-full wp-image-1597" src="https://image.uu126.cn/wp-content/uploads/2025/09/20250907000211656.webp" alt="" width="824" height="291" />

PHP搞好后，顺便把Mysql也从5.7升级到8.0吧，咱这6G的服务器不能浪费嘛，结果升级还得让我先把数据库删除了（这动手前还不得先备份一下），删完了还得卸载才能安装新版本，还真是折腾，早知道这么麻烦俺们就不折腾了，小破站本也没多少看客，但为了满足本站的终身VIP会员——本人那点小心思，还是折腾一下吧，一顿操作下来，现在就是8+8模式了，哈哈。

<img class="alignnone size-large wp-image-1598" src="https://image.uu126.cn/wp-content/uploads/2025/09/20250907000552323-1280x853.webp" alt="" width="1280" height="853" />

满足了，睡觉去，有空再捣鼓一下……