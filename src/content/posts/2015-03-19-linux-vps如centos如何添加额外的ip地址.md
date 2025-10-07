---
title: Linux VPS(如CentOS)如何添加额外的IP地址
author: Feng
type: post
published: 2015-03-19T14:35:53+00:00
url: /it/217.html
hera_post_view:
  - 5
categories:
  - IT网络

---
很多同学在购买额外的IP地址后，跑来提交ticket，问为什么你这个IP不能访问啊，是不是IP被屏蔽了？遇到这种问题，我们常常会告知客户，IP是需要手动在Linux中绑定的。那么购买IP后如何在Linux VPS下绑定额外的IP地址呢？  
<span id="more-130"></span>  
1、进入主机服务商的后台查看，这里以国外主机商VPS2EZ为例，先会员中心，再点击服务管理-管理/添加IP地址，在IP地址列表中，点击IP，查看IP所对应的网关地址和子网掩码。  
[<img loading="lazy" decoding="async" class="alignnone wp-image-1615" src="http://uu126.cn/wp-content/uploads/2015/03/addip1.jpg" alt="addip1" width="470" height="304" />][1]  
&nbsp;  
2、使用putty等软件SSH登录VPS，输入命令：

<pre class="lang:sh decode:true " >cd /etc/sysconfig/network-scripts/</pre>

编辑文件，如果怕麻烦可以使用WinSCP，这里以使用命令方式：

<pre class="lang:sh decode:true " >vi ifcfg-eth0:<span class="number">1</span></pre>

复制以下代码到编辑框：

<pre class="lang:sh decode:true " >DEVICE=eth0:1
onboot=YES
BOOTPROTO=static
IPADDR=此处替换为额外的IP地址
NETMASK=此处替换为子网掩码
GATEWAY=此处替换为网关地址</pre>

重启网卡：

<pre class="lang:sh decode:true " >service network restart</pre>

3、测试新增加的IP地址是否可以访问。

 [1]: http://uu126.cn/wp-content/uploads/2015/03/addip1.jpg