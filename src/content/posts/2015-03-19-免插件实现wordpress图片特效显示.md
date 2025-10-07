---
title: 免插件实现Wordpress图片特效显示
author: Feng
type: post
published: 2015-03-19T11:52:20+00:00
url: /it/216.html
hera_post_view:
  - 4
categories:
  - IT网络

---
自从用了这个简洁主题之后，以现很多功能都没了，于是又开始折腾旅程了，这不今天开始捣鼓图片特效了，Wordpress没装特效时点击图片会直接连接到图片地址，想继续看文章时就得使用“倒退”了，挺不方便的，所以得改改。话说到这里，其实很多插件都有这个功能，可又不想去安装，唉！还是把插件本地化吧，整合去。先去<a href="http://fancyapps.com/fancybox/" target="_blank" rel="noopener"><a href="http://fancyapps.com/fancybox/">http://fancyapps.com/fancybox/</a></a>下载这个盒子特效，下载后解压，提取source文件夹中如下几个基本文件：

<pre class="lang:default decode:true " >blank.gif
fancybox_loading.gif
fancybox_loading@2x.gif
fancybox_overlay.png
fancybox_sprite.png
fancybox_sprite@2x.png
jquery.fancybox.css
jquery.fancybox.pack.js</pre>

将这些文件保存到新建目录fancybox（可以自己定义名称，只要和后面一样就行），接着在function.php文件中加入代码：

<pre class="lang:php decode:true " >//自动添加暗箱标签属性
add_filter('the_content', 'pirobox_gall_replace');
function pirobox_gall_replace ($content)
{ global $post;
$pattern = "/&lt;a(.*?)href=('|")([^>]*).(bmp|gif|jpeg|jpg|png)('|")(.*?)>(.*?)&lt;/a>/i";
$replacement = '&lt;a$1href=$2$3.$4$5 rel="fancybox"$6>$7&lt;/a>';
$content = preg_replace($pattern, $replacement, $content);
return $content;
}</pre>

再在header.php或者footer.php文件中加入代码：

<pre class="lang:php decode:true " >&lt;link rel=“stylesheet” type=“text/css” href=“&lt;?php bloginfo(‘template_url’) ?&gt;/fancybox/jquery.fancybox.css” /&gt;
&lt;script src=“&lt;?php bloginfo(‘template_url’) ?&gt;/fancybox/jquery.fancybox.pack.js”&gt;&lt;/script&gt;
&lt;script type=“text/javascript”&gt;
$(function() {
jQuery(“.gallery a”).attr({rel: “fancybox”});
jQuery(“a[rel=fancybox]”).fancybox();
});
&lt;/script&gt;</pre>

这段里的fancybox就是刚才我新建的目录，所以如果你自己是其它名字的话，也在代码里改一下。  
好了，图片暗箱显示特效就大功告成了！