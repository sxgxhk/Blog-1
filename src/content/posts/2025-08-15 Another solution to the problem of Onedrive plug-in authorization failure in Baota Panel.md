---
title: 宝塔面板 Onedrive 插件授权失败的另解之法
published: 2025-08-15
updated: 2025-08-15
description: '自从上次把宝塔中的备份目的地改成Onedrive后，用了也有一段时间，相比其它收费的存储倒是省了一丢丢，不过好景不长，昨天收到备份失败的消息，查看了一下日志，似乎是密钥过期了，那就重新再授权一下吧，结果杯具了——授权失败，卸载掉重装也不行，后来查了，出现这种错误的还蛮多的，一般都说是宝塔给的密钥过期了'
image: ''
tags: [网站]
category: 'IT网络'
draft: false 
---

自从上次把宝塔中的备份目的地改成Onedrive后，用了也有一段时间，相比其它收费的存储倒是省了一丢丢，不过好景不长，昨天收到备份失败的消息，查看了一下日志，似乎是密钥过期了，那就重新再授权一下吧，结果杯具了——授权失败，卸载掉重装也不行，后来查了，出现这种错误的还蛮多的，一般都说是宝塔给的密钥过期了，好吧，本想跟着教程自己去注册个Microsoft Azure 创建应用程序的，结果试了好几回都以失败而结……

<img class="alignnone size-full wp-image-1589" src="https://image.uu126.cn/wp-content/uploads/2025/08/20250818150647261.png" alt="" width="747" height="301" />

后来想想，我的1Panel上不也是在用嘛，那个都能正常使用没报错，去拷个密钥来替换一下不就好了，马上走起&gt;&gt;&gt;&gt;，来到1Panel的备份账号里，添加一个Onedrive，马上就能看到我想要的东西：

<img class="alignnone size-full wp-image-1585" src="https://image.uu126.cn/wp-content/uploads/2025/08/20250818150634960.png" alt="" width="639" height="629" />

于是把客户端ID和客户端密钥Copy下来，再来到宝塔面板的文件中，找到Onedrive插件的目录：/www/server/panel/plugin/msonedrive/credentials.json，打开这个文件，在onedrive-international里修改相应的参数保存一下：

<img class="alignnone size-full wp-image-1588" src="https://image.uu126.cn/wp-content/uploads/2025/08/20250818150644125.png" alt="" width="1024" height="525" />

保存后再去应用商店中的Onedrive里重新按步骤授权一下即可：

&nbsp;

<img class="alignnone size-full wp-image-1587" src="https://image.uu126.cn/wp-content/uploads/2025/08/20250818150642261.png" alt="" width="1024" height="576" />

<img class="alignnone size-full wp-image-1586" src="https://image.uu126.cn/wp-content/uploads/2025/08/20250818150639737.png" alt="" width="687" height="603" />

这不就搞定了嘛，上宝塔面板的计划任务里，试着跟个任务试试，显示上传成功，搞定！

其实类似的网上教程很多，本也是宝塔官方未及时更新相关参数导致（这点还是1Panel好呀），自己注册应用（这招我试了不行，学艺不精……）解决不成功的，可以尝试这个办法，毕竟就算是搭个1Panel不也分分钟的事嘛，不管怎么样，我觉得只要能解决问题就好——懒人说词，哈哈。