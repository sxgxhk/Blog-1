---
title: WP-syntax(Wordpress代码高亮插件）的使用及简单美化
author: Feng
type: post
published: 2014-06-14T12:39:00+00:00
url: /my/142.html
hera_post_view:
  - 6
categories:
  - 生活随笔
tags:
  - word
  - Wordpress

---
在Wordpress里发表一些代码，估计是各位大大们经常碰到的事，相关的插件也很多，这里就简单说一下本站在用的WP-syntax插件吧，安装很简单，相信会玩Wordpress的都知道哈（插件&#8211;搜索&#8211;安装&#8211;启用），下面来说说简单的使用办法吧。担心代码冲突，所以下面“（”和“）”在使用时换成“<“和”>“ <span style="background-color: #f7f7f7; color: #222222; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 15px; line-height: 21px;">即可。</span>

<pre class="lang:php decode:true " >&lt;pre lang="html" line="1" escaped="true"&gt;
//这里添加代码……
&lt;/pre&gt;</pre>

<span style="color: #3366ff;">注释：lang="html"表示代码语言为html，请根据自己需要修改； line="1" 表示显示行号，如果不需要，去掉即可；escaped="true" 是为了防止代码转义，如果不需要，去掉即可。</span> <span style="color: #3366ff;">注意：在wordpress后台使用 WP-Syntax 等代码高亮插件，需要在html模式下添加代码，不要随意切换到可视化模式，否则代码就容易转义！！</span> 由于插件本身的CSS不是很美观，建议修改一下，本站用的CSS代码如下（覆盖该插件的 wp-syntax/wp-syntax.css 的代码）：

<pre class="lang:css decode:true " >.wp_syntax {
color:#100;
background-color:#f9f9f9;
border:1px solid #EBEBEB;
margin:0 0 1.5em 0;
overflow:auto;
}
.wp_syntax {
overflow-x:auto;
overflow-y:hidden;
padding-bottom:expression(this.scrollWidth &gt; this.offsetWidth ? 15:0);
width:99%;
}
.wp_syntax table {
border:none;
border-collapse:collapse;
margin:0;
padding:0;
width:100% !important
}
.wp_syntax caption {
padding:2px;
width:100%;
background-color:#def;
text-align:left;
font-family:Monaco;
font-size:13px;
line-height:20px;
}
.wp_syntax caption a {
color:#1982d1;
text-align:left;
font-family:Monaco;
font-size:13px;
line-height:20px;
text-decoration:none;
}
.wp_syntax caption a:hover {
color:#1982d1;
text-decoration:underline;
}
.wp_syntax div,.wp_syntax td {
border:none;
text-align:left;
padding:0;
vertical-align:top;
}
.wp_syntax td.code {
background:none;
line-height:normal;
white-space:normal;
padding-left:10px;
}
.wp_syntax pre {
background:transparent;
margin:0;
padding:0;
width:auto;
float:none;
clear:none;
overflow:visible;
font-family:Monaco;
font-size:13px;
line-height:20px;
white-space:pre;
}
.wp_syntax td.line_numbers pre {
border-right:3px solid #6CE26C;
background-color:#E7E5DC;
color:gray;
width:20px;
padding:0 5px;
text-align:right;
}</pre>

写的简单了点，有空再来补充一下哈，各位看官多多见谅哈。