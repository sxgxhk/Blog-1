---
title: WordPress使用OSS详尽教程（使用OSS非下载图片）
author: Feng
type: post
published: 2015-12-21T13:28:00+00:00
url: /it/268.html
hera_post_view:
  - 5
categories:
  - IT网络
tags:
  - Wordpress

---
自己用的是阿里云的ECS，一直想用OSS存储图片，可惜碍于技术能力有限（最主要还是担心口袋里的银子），终于等到今天鼓起勇气使用OSS，先用一个月看看，贵咱就……言归正传，看了阿里云论坛上就关于Wordpress使用OSS有很多招，插件、第三方工具等等，还是用插件吧，具体的就看下面这篇文章吧，写的蛮详细的，直接转载了：

最近在阿里云申请了一个OSS，OSS是个开放存储器，闲话不多说，我们做项目的时候就是拿它当作专门存储图片的，可以看成一个云端的硬盘。  
WordPress其实是有插件可以直接使用OSS，但是由于OSS时常改进，所以该插件使用的时候会有点问题，反正我就遇到了很多问题，这里给大家详尽讲解一下如何使用oss4wp的全部过程。

首先，大家应该得明白，当我们把图片上传到OSS，使用OSS给的地址，浏览器会直接去下载图片，这个不是我们想要的，然而OSS为了安全起见，默认就是直接下载，据说老版本可以通过修改Http头，达到显示图片而不是下载图片的效果，然而我现在用的完全不行，只能通过绑定二级域名来达到这种效果。

这里拜一下大神，原本的插件下载地址：[oss4wp插件下载][1]  
知道我们需要二级域名，接下来我们就需要去绑定一个二级域名，我的域名是在万网上面买的。

### 打开域名解析

&nbsp;

2.点击添加解析

记住这里的记录类型一定要选择A，主机记录我写的为  img ，记录值为主机ip地址，解析完成后，我们就可以通过  img.coolecho.net 这个二级域名来访问我们的网站，解析过程中可能有网络缓冲，若打不开网页，你可以用ping来测试一下。

3.上传插件并启用

这个比较简单，按照插件的步骤一步一步来即可。

4.设置oss4wp

&nbsp;

Bucket这里我们选择新建，CName这里为img.coolecho.net。

5.OSS绑定域名

&nbsp;  
         这里我为了演示，就新建了一个img1.coolecho.net，这是错的，这里应该还是img.coolecho.net，然后下载文件上传至网站根目录，在验证绑定就行。  
6.修改解析域名

这个时候你发现可以去上传，但是上传成功根本就找不到图片正确的路径。

点击这里就可以上传文件至OSS，但是所有的图片是这个样子的。

7.这个时候我们需要修改解析

回到万网，修改之前加上去的解析，将A改为CName，记录值为OSS域名，这里我的为oss-cn-hangzhou.aliyuncs.com，不同地区的不同。

&nbsp;

不知道记录值的，可以现在OSS上传一张图片，然后打开地址。

比如：  
[<http://osscoolecho.oss-cn-hangzhou.aliyuncs.com/2015/04/liu.png>][2]  
红色字体就是我们要的记录值。

8.修改插件

当你以为着所有的一切都完了之后，发现上传为文件依旧是找不到的，经过比对后发现，你就发现了一些问题

&nbsp;

OSS： [<http://osscoolecho.oss-cn-hangzhou.aliyuncs.com/2015/04/liu.png>][2]

wordpreess：[<http://img.coolecho.net/osscoolecho/2015/04/liu.png>][3]

之所以打不开是因为  wordpress中的url多了一个osscoolecho，也就是Bucket的名字，这时候我们只好自己去修改了。

打开插件，找到class-plugin-public.php文件：

将   .$this->options[‘bucket’].”/”   去掉即可。

本文云转载自：www.coolecho.net，谢谢这位博主了。

 [1]: http://bbs.aliyun.com/read/119733.html?spm=0.0.0.0.Mxs2NM
 [2]: http://osscoolecho.oss-cn-hangzhou.aliyuncs.com/2015/04/liu.png
 [3]: http://img.coolecho.net/osscoolecho/2015/04/liu.png