---
title: 使用LNMP1.2架设的Wordpress使用OCS问题解决
author: Feng
type: post
published: 2015-12-20T01:40:44+00:00
url: /it/266.html
hera_post_view:
  - 6
categories:
  - IT网络
tags:
  - Wordpress

---
建站从以前的Windows平台到后来的Centos，再又从WDC面板到军哥的LNMP，算是用的比较晚了，LNMP1.1版本的，一路顺风，诸如各项缓存：eAccelerator，Memcached等都运行OK，而且也用上了阿里云的OCS（现在应该是叫“云数据库Memcache版”），运行了差不多一年了吧，从来没关过机或重启过，阿里云的东西还是真心不错的，稳定！这不快续费了，现在用的主机还是去年双十一半价抢来的，可惜今年没有这活动了，所以只能降配续费吧，一下子就降到了基本型了，连数据云盘都不要了，1核512M带宽也是1M，应该不能再降了吧，既然降了，系统索性重装吧，刚好现在军哥LNMP也有新版本了，目前最新的是1.3属于测试阶段，所以就选择了1.2稳定版的，一路默认到最后，接着创建网站，并用WinSCP上传（这是好东西，连FTP都用不着了），等到全部弄完后，打开我的小博客，杯具了，白屏跳500错误，果断删除wp-content目录下的object-cache.php，网站立马就可以访问了，基本判定是缓存Memcached的问题了，要不换个版本的memcached吧，原来军哥给的默认是;  
<a href="http://uu126.cn/wp-content/uploads/2015/12/3448493554.png" rel="attachment wp-att-1914"><img loading="lazy" decoding="async" class="aligncenter size-full wp-image-1914" src="http://uu126.cn/wp-content/uploads/2015/12/3448493554.png" alt="3448493554" width="520" height="175" /></a>  
默认安装的是2，那就先卸载吧，输入命令:

<pre class="lang:default decode:true " >./addons.sh uninstall memcached</pre>

然后再重新安装，输入命令：

<pre class="lang:default decode:true " >./addons.sh install memcached
</pre>

安装好之后，重启一下LNMP，LNMP1.2的命令跟1.1的版本不一样了，是：

<pre class="lang:default decode:true " >lnmp restart
</pre>

当然这些命令还是要在进入lnmp1.2-full目录下才能用的，重启后之后再上传object-cache.php至wp-content目录，刷新一下网站，这回OK了，首页和后台都可以访问了。