---
title: Win主机IIS下配置WordPress伪静态【亲测成功】
author: Feng
type: post
published: 2012-11-16T13:56:04+00:00
url: /it/35.html
hera_post_view:
  - 4
categories:
  - IT网络

---
首先说一下，此方法仅适用于独立主机，或者你可以远程服务器均可（虚拟机就不用用试了，VPS当然是好用的）！  
第一步，在IIS站点配置加载一个WordPress URL Rewrite组件就行了。组件可以从这里下载：[<http://www.binaryfortress.com/wordpress-url-rewrite>][1]，下载此组件以后，把压缩包解压到任何地方，保持WordPressURLRewrite.ini和WordPressURLRewrite32.dll（32位版本，64位版本对应为64.dll）在同一文件夹下就可以了。一般都是32位，选择32位即可。  
第二步，在网站根目录放置httpd.ini文件！  
方法如下：  
首先得保证主机已经加载Rewrite组件，然后将下列代码保存为httpd.ini文件，上传到网站根目录即可！  
代码如下：  
[ISAPI_Rewrite]  
RewriteRule /post/tag/(._) /index.php?tag=$1  
RewriteRule /tag/(._) /index.php?tag=$1  
RewriteRule /(about|link|tags|sitemap) /index.php?pagename=$1  
RewriteRule /post/category/(._)/(feed|rdf|rss|rss2|atom)/?$ /wp-feed.php?category_name=$1&feed=$2  
RewriteRule /post/category/?(._) /index.php?category_name=$1  
RewriteRule /author/(._)/(feed|rdf|rss|rss2|atom)/?$ /wp-feed.php?author_name=$1&feed=$2  
RewriteRule /author/?(._) /index.php?author_name=$1  
RewriteRule /feed /index.php/?feed=rss2  
RewriteRule /rss.xml /index.php/?feed=rss2  
RewriteRule /comments/feed /index.php/?feed=comments-rss2  
RewriteRule /([0-9]+)/?([0-9]+)?/?$ /index.php?p=$1&page=$2  
RewriteRule /post/([0-9]+)/?([0-9]+)?/?$ /index.php?p=$1&page=$2  
RewriteRule /post/([0-9]+).html /index.php?p=$1 [I]  
RewriteRule /page/(._)/?s=(._) /index.php?s=$2&paged=$1  
RewriteRule /page/(.*) /index.php?paged=$1  
RewriteRule /post/date/([0-9]{4})([0-9]{1,2})([0-9]{1,2})/([^/]+)/?([0-9]+)?/?$ /index.php?year=$1&monthnum=$2&day=$3&name=$4&page=$5  
RewriteRule /post/date/([0-9]{4})/([0-9]{1,2})/([0-9]{1,2})/?$ /index.php?year=$1&monthnum=$2&day=$3&page=$4  
RewriteRule /post/date/([0-9]{4})/([0-9]{1,2})/?$ /index.php?year=$1&monthnum=$2&page=$3  
RewriteRule /post/([0-9]+).html/(feed|rdf|rss|rss2|atom) /index.php?feed=rss2&p=$1  
RewriteRule /post/([0-9]+).html/trackback /wp-trackback.php?p=$1

#  For file-based wordpress content (i.e. theme), admin, etc.

RewriteRule /wp-(.*) /wp-$1 [L]  
说明：止述伪静态规则实现的静态地址效果是：[<http://www.XXXX.com>**/post/4.html**][2]  
特别说明，网上有些规则，可已经太文章、TGS、归档、但是对wp的单页面步支持，  
这个规则中的第四行是针对单页面的伪静态  
RewriteRule /(**about**|link|tags|sitemap) /index.php?pagename=$1  
规则中的这部分(about|link|tags|sitemap)，如果你有需要可以增加，比如(about|link|tags|sitemap)可以增加(about|link|tags|sitemap|page|like|love)等等等等，结尾处不要|  
例如博客上面有“关于”，别名记得改成about，或你想要使用的，同时规则中也记得和别名一致。  
第三步，登录你的WordPress后台，在设置中的固定链接选择自定义为：**/post/%post_id%.html，**保存后就可以看到效果了，本站就是这么搞定的  
****  
&nbsp;

 [1]: http://www.binaryfortress.com/wordpress-url-rewrite
 [2]: http://www.XXXX.com/post/4.html