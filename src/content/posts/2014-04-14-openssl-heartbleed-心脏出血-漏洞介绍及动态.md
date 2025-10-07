---
title: OpenSSL Heartbleed（心脏出血）漏洞介绍及动态
author: Feng
type: post
published: 2014-04-14T13:31:39+00:00
url: /my/113.html
hera_post_view:
  - 11
categories:
  - 生活随笔
tags:
  - 服务器
  - 淘宝

---
## OpenSSL漏洞介绍

### 漏洞简介：

2014年4月7日OpenSSL发布了安全公告，在OpenSSL1.0.1版本的心跳包模块存在严重漏洞（CVE-2014-0160）。攻击者可以通过构造特殊的数据包，直接远程读取存在漏洞的OpenSSL服务器内存中多达64KB的数据，极有可能导致网站用户帐号密码等敏感数据被非法获取。漏洞发现者甚至声称可以直接获取到证书私钥和重要的商业文档。

### 漏洞影响：

国内大量使用HTTPS协议的网站相当一部分都存在此漏洞，其中不乏知名电子商务网站及提供关键服务（邮箱、社交等网站），此次曝光的漏洞非常严重，安全威胁不容小觑。

### OpenSSL受影响和不受影响版本：

OpenSSL 1.0.1f（受影响）  
OpenSSL 1.0.1g （不受影响）  
OpenSSL 1.0.0 branch （不受影响）  
OpenSSL 0.9.8 branch （不受影响）

### 什么是SSL？

SSL是一种流行的加密技术，可以保护用户通过互联网传输的隐私信息。当用户访问Gmail.com等安全网站时，就会在URL地址旁看到一个“锁”，表明你在该网站上的通讯信息都被加密。  
这个“锁”表明，第三方无法读取你与该网站之间的任何通讯信息。在后台，通过SSL加密的数据只有接收者才能解密。很多大型网络服务都已经默认利用这项技术加密数据。如今，谷歌、雅虎和Facebook都在使用SSL默认对其网站和网络服务进行加密。

### 什么是“心脏出血”漏洞？

多数SSL加密的网站都使用名为OpenSSL的开源软件包。本周一，研究人员宣布这款软件存在严重漏洞，可能导致用户的通讯信息暴露给攻击者。OpenSSL大约两年前就已经存在这一缺陷。

<div>
  <h3>
    OpenSSL漏洞工作原理：
  </h3>
  
  <p>
    SSL标准包含一个心跳选项，允许SSL连接一端的电脑发出一条简短的信息，确认另一端的电脑仍然在线，并获取反馈。研究人员发现，可以通过巧妙的手段发出恶意心跳信息，欺骗另一端的电脑泄露机密信息。受影响的电脑可能会因此而被骗，并发送服务器内存中的信息。
  </p>
  
  <h3>
    该漏洞的影响大不大？
  </h3>
  
  <p>
    很大，因为有很多隐私信息都存储在服务器内存中。使用这项技术的攻击者可以通过模式匹配对信息进行分类整理，从而找出密钥、密码，以及信用卡号等个人信息。<br /> 丢失了信用卡号和密码的危害有多大，相信已经不言而喻。但密钥被盗的后果可能更加严重：这是信息服务器用于整理加密信息的一组代码。如果攻击者获取了服务器的私钥，便可读取其收到的任何信息，甚至能够利用密钥假冒服务器，欺骗用户泄露密码和其他敏感信息。
  </p>
  
  <h3>
    网站怎么办？
  </h3>
  
  <p>
    网站管理员应尽快升级OpenSSL到1.0.1g。
  </p>
  
  <h3>
    网民怎么办？
  </h3>
  
  <p>
    1.注意观察相关事件进展，目前尚无法准确评估黑客利用OpenSSL漏洞获得了多少数据。<br /> 2.对重要服务，尽可能开通手机验证或动态密码，比如支付宝、邮箱等，登录重要服务，不仅仅需要验证用户名密码，最好绑定手机，加手机验证码登录。这样就算黑客拿到帐户密码，登录还有另一道门槛。<br /> 3.随着事件进展，一些知名网站已修复安全漏洞，此时用户可以修改重要服务的登录密码。专家建议：一个密码的使用时间不宜过长，超过3个月就该更换了。
  </p>
</div>

<div>
</div>

<!-- footer -->

<div>
  <h2>
    相关动态
  </h2>
  
  <h3>
    已修复漏洞的知名网站
  </h3>
  
  <dl>
    <dt>
      银行
    </dt>
    
    <dd>
      中国工商银行   www.icbc.com.cn
    </dd>
    
    <dd>
      招商银行   www.cmbchina.com
    </dd>
    
    <dd>
      中国农业银行   www.abchina.com
    </dd>
    
    <dd>
      广东发展银行   ebank.gdb.com.cn
    </dd>
    
    <dd>
      中国银行   www.boc.cn
    </dd>
    
    <dd>
      深圳发展银行   bank.pingan.com
    </dd>
    
    <dd>
      中国建设银行   www.ccb.cn
    </dd>
    
    <dd>
      兴业银行   www.cib.com.cn
    </dd>
    
    <dd>
      交通银行   www.bankcomm.com
    </dd>
    
    <dd>
      上海浦东发展银行   www.spdb.com.cn
    </dd>
    
    <dd>
      中信实业银行   www.ecitic.com
    </dd>
    
    <dd>
      上海银行   www.bankofshanghai.com.cn
    </dd>
    
    <dd>
      中国光大银行   www.cebbank.com
    </dd>
    
    <dd>
      宁波市商业银行   www.nbcb.com.cn
    </dd>
    
    <dd>
      中国民生银行   www.cmbc.com.cn
    </dd>
  </dl>
  
  <dl>
    <dt>
      电商
    </dt>
    
    <dd>
      淘宝   www.taobao.com
    </dd>
    
    <dd>
      支付宝   www.alipay.com
    </dd>
    
    <dd>
      京东   www.jd.com
    </dd>
    
    <dd>
      卓越   www.amazon.cn
    </dd>
    
    <dd>
      易迅   www.yixun.com
    </dd>
    
    <dd>
      新蛋   www.newegg.cn
    </dd>
  </dl>
  
  <dl>
    <dt>
      门户
    </dt>
    
    <dd>
      新浪   www.sina.com.cn
    </dd>
    
    <dd>
      网易   www.163.com
    </dd>
    
    <dd>
      雅虎   www.yahoo.com
    </dd>
    
    <dd>
      腾讯   www.qq.com
    </dd>
  </dl>
  
  <h3>
    未修复漏洞的网站
  </h3>
  
  <ul>
    <!--
    

<li>www.273.cn</li>


--></p> 
    
    <li>
      aoyama-platinum.com
    </li>
    <li>
      bookstores.umn.edu
    </li>
    <li>
      www3.startsupport.com
    </li>
    <li>
      cvvshop.lv
    </li>
    <li>
      gdx.gestamp.com
    </li>
    <li>
      555wang.com
    </li>
    <li>
      c.108198.com
    </li>
    <li>
      210.237.109.229
    </li>
    <li>
      jc3.guiguyun.cn
    </li>
    <li>
      snowsummit.tv
    </li>
    <li>
      websterandsons.filecamp.com
    </li>
    <li>
      220.248.244.12
    </li>
    <li>
      oa1.zrjt.com.cn
    </li>
    <li>
      catwebedi.com
    </li>
    <li>
      esupplier.amat.com
    </li>
    <li>
      trac.syous.co.jp
    </li>
    <li>
      218.106.152.82
    </li>
    <li>
      liji-ccms.fenxibao.com
    </li>
    <li>
      elearning2.danahertm.com
    </li>
    <li>
      sellerpartner.dxmallcloud.com
    </li>
  </ul>
  
  <h3>
    新闻动态
  </h3>
  
  <p>
    OpenSSL安全漏洞威胁升级 电脑手机均可能被窃取隐私<br /> 4月11日消息，互联网严重安全漏洞OpenSSL“心脏出血”的威胁仍在发酵。金山毒霸安全中心研究发现，不仅网民访问https攻击网站会泄露个人隐私信息，而且使用包含OpenSSL代码库的一些电脑软件，甚至安卓APP、浏览器，都有可能面临隐私被窃取的风险。<br /> 金山毒霸安全专家指出，国外已有黑客将针对个人电脑、手机、平板设备的攻击代码公开，可能已在黑客圈大面积传播。黑客利用OpenSSL“心脏出血”漏洞构造特殊网页，诱骗网民点击访问。<br /> 当用户电脑或移动电子设备使用了OpenSSL的软件，访问到上述攻击网页时，黑客就通过服务器发送恶意“心跳包”（定时发送的通讯包）给客户端，利用漏洞多次远程读取用户系统内存数据，盗取用户数字证书，帐号，密码，上网记录等重要信息。<br /> OpenSSL Heartbleed（“心脏出血”）漏洞被业内称为2014年度最重大的安全漏洞之一，它不久前由安全公司Codenomicon和谷歌的工程师发现，漏洞编号CVE-2014-0160。<br /> 由于OpenSSL协议广泛应用于网银、在线支付、电子邮件、电商等重要网站，所以利用此漏洞的黑客只需坐在电脑前，即可实时获取约30%以https开头网址的用户登录账号密码。<br /> 据最新消息，该漏洞不仅影响了大量网站服务器，也存在于思科和Juniper的网络设备中。思科已经列出了10余款被确认存在漏洞的产品，而另60余款产品可能受到影响，但调查仍在进行中。<br /> 除网络设备之外，一些手机系统也存在“心脏出血”漏洞。谷歌近日发布公告证实安卓手机用户同样受到此漏洞的威胁。谷歌称安卓系统的4.1.1版采用了有漏洞版本的OpenSSL协议库，用户同样面临隐私遭窃取的风险。<br /> 据安全圈人士透露，由于OpenSSL漏洞的出现，在近日的地下交易市场中，各种兜售非法数据的交易显得异常火爆。<br /> 目前，国内外众多网站和网络服务商正积极应对此次重大安全事件。金山毒霸安全中心分析，截止目前，包括工行、建行、农行、交行、招行等较大的银行网站，支付宝、淘宝、京东、卓越等电商及支付网站，新浪、腾讯、网易等门户网站，国内网民经常使用的知名网站服务已修复该漏洞。但是，国内仍有部分网站仍未修复，尚存风险。
  </p>
</div>