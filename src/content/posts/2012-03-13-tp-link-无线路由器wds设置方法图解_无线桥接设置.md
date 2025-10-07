---
title: TP-link 无线路由器WDS设置方法图解_无线桥接设置
author: Feng
type: post
published: 2012-03-13T08:02:02+00:00
url: /my/17.html
hera_post_view:
  - 5
categories:
  - 生活随笔

---
TP-link 无线路由器WDS设置方法图解_无线桥接设置  
详细出处参考：<a href="http://www.jb51.net/softjc/39394.html" target="_blank" rel="noopener"><a href="http://www.jb51.net/softjc/39394.html">http://www.jb51.net/softjc/39394.html</a></a>  
随着无线网络的发展，现在越来越多的公司及企业都已经开始布局无线局域网，今天我们主要介绍下适合中小企业的无线路由器桥接或WDS功能。文章以TP-link WR841N无线路由器设置为例，其它路由器参考设置思路进行设置。

<img decoding="async" id="aimg_142073" title="11.jpg" src="http://sky123.org/data/attachment/forum/201202/25/171243x0zr9roogbxovn92.jpg" alt="11.jpg" width="422" /> 

<div id="aimg_142073_menu">
  　　上图所示为一小型企业无线网络，A、B、C三个部门如果只使用1个无线路由器，可能会出现一些计算机搜到信号很弱或者搜索不到信号，导致无法连接无线网络。解决方法是：A、B、C三个部门各自连接一台无线路由器，三个无线路由器通过WDS连接就可以实现整个区域的完美覆盖、消除盲点。
</div>

配置思想：无线路由器B作为中心无线路由器，无线路由器A、C与无线路由器B建立WDS连接。  
步骤如下：

<table cellspacing="0" cellpadding="0">
  <tr>
    <td id="postmessage_3244743">
      <div>
        无线路由器的基本设置请参考：tp link无线路由器设置<br /> 一、中心无线路由器B设置<br /> 登陆无线路由器设置B管理界面，在无线设置-基本设置中设置“SSID号”、“信道”，如图：<br /> <img decoding="async" id="aimg_142061" title="1.jpg" src="http://sky123.org/data/attachment/forum/201202/25/170944h5dd4j4ha52zt5j7.jpg" alt="1.jpg" width="508" /></p> 
        
        <div id="aimg_142061_menu">
        </div>
        
        <p>
          在“无线设置”——“无线安全设置”中设置无线信号加密信息<br /> <img decoding="async" id="aimg_142062" title="2.jpg" src="http://sky123.org/data/attachment/forum/201202/25/170944snyo7daj7itwi042.jpg" alt="2.jpg" width="470" />
        </p>
        
        <div id="aimg_142062_menu">
        </div>
        
        <p>
          记录无线路由器B设置后的SSID、信道和加密设置信息，在后续无线路由器A、C的配置中需要应用。<br /> 二、无线路由器A设置。<br /> 1.修改LAN口IP地址。在网络参数-LAN口设置中，修改IP地址和B路由器不同（防止IP地址冲突），如192.168.1.2，保存，路由器会自动重启。<br /> <img decoding="async" id="aimg_142063" title="3.jpg" src="http://sky123.org/data/attachment/forum/201202/25/170944599hhhy5hbvjkhe4.jpg" alt="3.jpg" width="504" />
        </p>
        
        <div id="aimg_142063_menu">
        </div>
        
        <p>
          2.启用WDS功能。重启完毕后，用更改后的LAN口IP地址重新登陆无线路由器A，在无线设置-基本设置中勾选“开启WDS”。大家注意这里的SSID跟B路由器的是不一样的，当然也可以设置成相同的，这样你在这三个路由器覆盖范围内可以漫游，也就是说只要你在这个范围内随意一点连上了网，到这个范围内的另一点也能上网,不用重新连接,重新输入SSID很方便形象的说就是三个路由器组成了一个相同的大网。<br /> <img decoding="async" id="aimg_142064" title="4.jpg" src="http://sky123.org/data/attachment/forum/201202/25/170944z8o1u1pag7tgvkqs.jpg" alt="4.jpg" width="507" />
        </p>
        
        <div id="aimg_142064_menu">
        </div>
        
        <p>
          3.WDS设置。点击“扫描”，搜索周围无线信号。<br /> <img decoding="async" id="aimg_142065" title="5.jpg" src="http://sky123.org/data/attachment/forum/201202/25/170945esnndduejcfiduj3.jpg" alt="5.jpg" width="507" />
        </p>
        
        <div id="aimg_142065_menu">
        </div>
        
        <p>
          在扫描到的信号列表中选择B路由器SSID号，如下图中TP-LINK_841_B,点击“连接”。<br /> <img decoding="async" id="aimg_142066" title="6.jpg" src="http://sky123.org/data/attachment/forum/201202/25/170945wfu2hh8unlnnhl8l.jpg" alt="6.jpg" width="499" />
        </p>
        
        <div id="aimg_142066_menu">
        </div>
        
        <p>
          将信道设置成与B路由器信道相同。<br /> <img decoding="async" id="aimg_142067" title="7.jpg" src="http://sky123.org/data/attachment/forum/201202/25/170945cnk2brc2cn67nnzk.jpg" alt="7.jpg" width="505" />
        </p>
        
        <div id="aimg_142067_menu">
        </div>
        
        <p>
          设置加密信息和B路由器相同，“保存”。<br /> <img decoding="async" id="aimg_142068" title="8.jpg" src="http://sky123.org/data/attachment/forum/201202/25/170945wti1avs232s3wssa.jpg" alt="8.jpg" width="505" />
        </p>
        
        <div id="aimg_142068_menu">
        </div>
        
        <p>
          4.关闭DHCP服务器。在DHCP服务器中，选择“不启用”，“保存”，重启路由器。<br /> <img decoding="async" id="aimg_142069" title="9.jpg" src="http://sky123.org/data/attachment/forum/201202/25/1709452xi1c2npnpsf2xhz.jpg" alt="9.jpg" width="499" />
        </p>
        
        <div id="aimg_142069_menu">
        </div>
        
        <p>
          无线路由器A配置完成。此时无线路由器A与无线路由器B已成功建立WDS。<br /> 三、无线路由器C设置。设置的方法跟路由器A配置相同（IP地址必须与路由器A、B以及网络中的其它计算机不能相同，否则会造成IP冲突计算机无法上网）。<br /> 详细出处参考：<a href="http://www.jb51.net/softjc/39394.html" target="_blank" rel="noopener">http://www.jb51.net/softjc/39394.html</a></div> </td> </tr> </tbody> </table>