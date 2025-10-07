---
title: 从WDCP迁徙到LNMPA
author: Feng
type: post
published: 2015-03-10T04:36:13+00:00
url: /it/211.html
hera_post_view:
  - 6
categories:
  - IT网络

---
开始玩站也蛮长时间了，期间经历过虚拟空间、合租主机、VPS到最后的阿里云（至于经历过多少个服务商都忘了），用过的系统有Win2003、Centos，Win2003就不说了（那个图形化的简单点），而CentOS则一直都使用的WDCP面板，这里不得不赞扬一下WDCP，非常适合新手使用（图形化界面的就是受欢迎呀），可时间一长觉得还是该使用无面板的，即使用LNMP或LNMPA这样，一来是WDCP毕竟会消耗一部分内存，对于俺这配置不高的“家”还是有一点压力的；二来WDCP多多少少会有一些漏洞，如果没更新及时的话，后果也是……（虽然是小站，可自从搬到阿里云后每天都能看到云盾提示，不知道是不是阿里云的云盾“太强”的缘故，以前用别的VPS都没发现或偶尔有攻击），所以最终决定弃WDCP改用LNMPA。  
要换成LNMPPA当然要选军哥的，网址：<a href="http://lnmp.org/" target="_blank" rel="noopener"><a href="http://lnmp.org/">http://lnmp.org/</a></a>，LNMPA相对于LNMP还是有很多优势的，具体的可以找度娘看看，这里就不在多说了，下面来说说俺的经历过程吧：  
第一次：先保存好资料（个人觉得数据库保存一下就好了），然后开始卸载WDCP（具体可以看这个<a href="http://www.nicky1605.net/121.html" target="_blank" rel="noopener">教程</a>），输入：

<pre class="lang:python decode:true " >wget http://down.wdlinux.cn/in/lanmp_wdcp_ins.sh
sh lanmp_wdcp_ins.sh uninstall</pre>

等看到下图，就表示卸载成功了  
[<img loading="lazy" decoding="async" class="alignnone size-full wp-image-1521" src="http://uu126.cn/wp-content/uploads/2015/03/wdcp-cp-install16_20150309043614.jpg" alt="wdcp-cp-install16" width="675" height="424" />][1]  
接着开始下载LNMP的安装包，这个按照的军哥的教程就可以了，<a href="http://lnmp.org/install.html" target="_blank" rel="noopener"><a href="http://lnmp.org/install.html">http://lnmp.org/install.html</a></a>，安装好之后接着配置站点这些（自己看教程，军哥写的还是蛮详细的），因为我的博客是启用了memcached，刚开始忘了安装了，导致了再配置好站点后出现访问500的错误，后来配置好memcached还是不行，原因是开始没有启用Apache，只是单纯使用Nginx，所以还一阵捣鼓的搞伪静态规则，还好最终网站可以正常访问了， 不过问题也来了，因为自己本身也是个半桶水，所以其它网站的伪静态规则搞不来，所以一直访问不了，后来又按装了Apache，这问题又来了（注意安装了Apache是不可逆的，三思！），网站彻底访问不了（包括之前弄好的博客），于是又开始忙活，删除之前搞的Nginx的伪静态规则，还是不行，心一狠干脆重新配置过吧（心想系统应该也蛮多垃圾的，顺便重装清理一下）。  
第二次：重装了系统，挂载好数据盘（仅挂载就可以了，不用格式化的，因为数据都在的），然后开始按军哥的教程先安装好LNMP，<span style="color: #ff0000;">接着直接安装Apache，<span style="color: #000000;">等一切就位后再开始配置虚拟主机并配置好memcached（这里啰嗦一下，像很多PHP加速军哥都做装备好了，都在解压后的目录下，直接执行安装就可以了），博客访问正常，其它网站也OK了，还是启用Apache好，因为这个伪静态规则一般都很好找到，开心一下！</span></span>  
至此，从WDCP迁徙到LNMPA就算是成功了，接下来就是时间的考验了，相信不会让我失望的！

 [1]: http://uu126.cn/wp-content/uploads/2015/03/wdcp-cp-install16_20150309043614.jpg