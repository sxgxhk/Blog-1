---
title: Wordpress头像不显示的处理方法
author: Feng
type: post
published: 2015-03-11T02:06:54+00:00
url: /my/212.html
hera_post_view:
  - 3
categories:
  - 生活随笔

---
Wordpress头像不显示的问题，之前也碰到过，不过一般主题都解决了（感谢这些作者们的辛勤制作），但今天还是让我碰到了，因为之前主题出了一点问题，所以就换了个主题（人懒没办法），就是现在在用的主题，也不知道是不是我哪里没弄好，反正就是主题安装好之后，评论头像就不显示了，没办法只好自己解决了，请了度娘来指教，终于解决了，方法如下：  
1、在Wordpress根目录里打开<span style="color: #ff0000;">wp-includes</span>目录，然后打开<span style="color: #ff0000;">pluggable.php</span>，找到下面这段代码：

<pre class="lang:php decode:true " >if ( is_ssl() ) {
        $host = ‘https://secure.gravatar.com’;
    } else {
        if ( !emptyempty($email) )
            $host = sprintf( “http://%d.gravatar.com”, ( hexdec( $email_hash[0] ) % 2 ) );
        else
            $host = ‘http://0.gravatar.com’;
    }</pre>

找到之后将其替换成如下代码：

<pre class="lang:php decode:true " >if ( is_ssl() ) {
    $host = ‘https://secure.gravatar.com’;
    } else {
    $host = ‘http://cn.gravatar.com’;
    }</pre>

然后上传替换，再刷新看看，是不是出来了。