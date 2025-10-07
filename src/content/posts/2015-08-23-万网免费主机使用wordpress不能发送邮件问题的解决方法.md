---
title: 万网免费主机使用WordPress不能发送邮件问题的解决方法
author: Feng
type: post
published: 2015-08-23T03:34:40+00:00
url: /it/253.html
hera_post_view:
  - 7
categories:
  - IT网络
tags:
  - Wordpress

---
<p style="font: 14px/1.8em 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; margin: 0px 0px 20px; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; box-sizing: border-box; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;">
  对于使用万网免费主机而又不想使用多说评论框的朋友，可能会发现即使安装了SMTP插件，评论回复也收不到邮件通知。之前在别人的博客中看到过相关的解决办法，测试有效，今天拿来给大家分享一下。
</p>

<p style="font: 14px/1.8em 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; margin: 0px 0px 20px; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; box-sizing: border-box; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;">
  <strong>1.</strong><span class="Apple-converted-space"> </span>进入万网免费<span id="3_nwp">主机</span>的<strong>管理控制台</strong>，然后点击左侧的“<strong>高级环境设置</strong>”–>“<strong>PHP.ini设置</strong>”，把“<strong>PHP函数fsockopen设置</strong>”设置为“<strong>启用</strong>”。
</p>

<p style="font: 14px/1.8em 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; margin: 0px 0px 20px; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; box-sizing: border-box; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;">
  <a href="http://uu126.cn/wp-content/uploads/2015/08/Wordpress-post.png"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-1820" src="http://uu126.cn/wp-content/uploads/2015/08/Wordpress-post.png" alt="Wordpress post" width="700" height="400" /></a>
</p>

<p style="font: 14px/1.8em 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; margin: 0px 0px 20px; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; box-sizing: border-box; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;">
  <strong><span style="font-family: 微软雅黑;">2.</span></strong><span style="font: 14px/25.2px 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;"> 打开</span><strong style="font: bold 14px/25.2px 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; box-sizing: border-box; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;">wp-includes/class-smtp.php</strong><span style="font: 14px/25.2px 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;">文件，找到下面的代码：</span>
</p>

<div class="dp-highlighter">
  <div class="bar">
  </div>
  
  <ol class="dp-c" start="0">
    <li class="alt">
      <span class="vars">$this</span>->smtp_conn = @stream_socket_client(
    </li>
    <li>
          <span class="vars">$host</span> . <span class="string">&#8220;:&#8221;</span> . <span class="vars">$port</span>,
    </li>
    <li class="alt">
          <span class="vars">$errno</span>,
    </li>
    <li>
          <span class="vars">$errstr</span>,
    </li>
    <li class="alt">
          <span class="vars">$timeout</span>,
    </li>
    <li>
          STREAM_CLIENT_CONNECT,
    </li>
    <li class="alt">
          <span class="vars">$socket_context</span>
    </li>
    <li>
      );
    </li>
  </ol>
</div>

<span style="font: 14px/25.2px 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; float: none; display: inline !important; white-space: normal; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;">把这段代码注释掉，然后在该代码的下面添加代码：</span>

<div class="dp-highlighter">
  <div class="bar">
  </div>
  
  <ol class="dp-c" start="0">
    <li class="alt">
      <span class="vars">$this</span>->smtp_conn = <span class="func">fsockopen</span>(<span class="vars">$host</span>, <span class="vars">$port</span>, <span class="vars">$errno</span>, <span class="vars">$errstr</span>);
    </li>
  </ol>
</div>

<p style="font: 14px/1.8em 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; margin: 0px 0px 20px; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; box-sizing: border-box; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;">
  保存后上传到<span id="2_nwp">服务器</span>，覆盖原来的文件。
</p>

<p style="font: 14px/1.8em 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; margin: 0px 0px 20px; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; box-sizing: border-box; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;">
  <strong>3. </strong>到WordPress后台安装一个SMTP插件，本人使用的是“Configure SMTP”，填写正确相关的配置。保存后可以点击下面的“Send test<span class="Apple-converted-space"> </span><span id="0_nwp">e-mail</span>”，测试是否可以成功发出<span id="1_nwp">邮件</span>，如果可以，说明已经配置成功，否则检查下配置是否正确。
</p>

<p style="font: 14px/1.8em 微软雅黑, 'WenQuanYi Micro Hei', STHeiti, SimSun, sans-serif; margin: 0px 0px 20px; color: #333333; text-transform: none; text-indent: 0px; letter-spacing: normal; word-spacing: 0px; white-space: normal; box-sizing: border-box; font-size-adjust: none; font-stretch: normal; background-color: #ffffff; -webkit-text-stroke-width: 0px;">
  本文转载自9IPHP博客。
</p>