---
title: Wordpress后台访问慢的解决办法
author: Feng
type: post
published: 2014-06-14T11:56:05+00:00
url: /my/141.html
hera_post_view:
  - 2
categories:
  - 生活随笔
tags:
  - word
  - 服务器

---
自从谷歌的服务器从香港搬走以后，加上一些“河蟹”之后，不仅谷歌搜索变得很鸡肋，就连一些网站的访问也慢的要死，本站用的是Wordpress搭建的，前台访问尚且OK，后台访问起来就很吃力了，通过开发者调试工具对网络加载进行检测，发现是由于后台使用了谷歌字体的API，因为谷歌api被墙的缘故，导致我们的浏览器会反复的请求谷歌服务器而无法正常加载页面，因此简单的解决方案就是禁用谷歌的字体api。  
解决方法是在当前主题的functions.php中加入下面的代码：

<pre lang="php" line="1" escaped="true">//禁用Open Sans
class Disable_Google_Fonts {
public function __construct() {
add_filter( 'gettext_with_context', array( $this, 'disable_open_sans' ), 888, 4 );
}
public function disable_open_sans( $translations, $text, $context, $domain ) {
if ( 'Open Sans font: on or off' == $context && 'on' == $text ) {
$translations = 'off';
}
return $translations;
}
}
$disable_google_fonts = new Disable_Google_Fonts;</pre>

&nbsp;  
记得点一下“更新”哦，要不然…………，这样操作过之后，再次重新登录可以发现比原先要稍快一点，当然这只是个临时解决方案，最好的办法还是把有关谷歌的相关调用进行替换或删除，想偷个懒就用这个办法吧。  
&nbsp;