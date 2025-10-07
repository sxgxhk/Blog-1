---
title: 百度BAE3.0 安装WordPress图文教程
author: Feng
type: post
published: 2014-02-21T14:34:09+00:00
url: /it/70.html
hera_post_view:
  - 7
categories:
  - IT网络

---
百度开发者（简称：BAE3.0）开放已经有些日子了，之前一直没有抢到，今天终于抢了一个执行单元，抱着试试看的心情去安装WordPress，当然功课是必须做的，下面这些图文教程转自网上，但是本人都一一试过了，因为我就是这一步步配置起来的。本来是可以参照官方的帮助的，可无奈的是官方的帮助基本上都是BAE2.0的，所以关键时候还是得去找度娘呀^-^  
目前图片上传还没弄好，直接附上原教程链接吧：<a href="http://blog.gimhoy.com/archives/wordpress-on-bae3.html" target="_blank" rel="noopener"><a href="http://blog.gimhoy.com/archives/wordpress-on-bae3.html">http://blog.gimhoy.com/archives/wordpress-on-bae3.html</a></a>  
几个注意点跟大家说一下：<span style="color: #ff0000;">在本地用SVN（如果这个用不来的，稍后在本站中搜索，我会说明一下如何使用）将WordPress上传至BAE（说明一下，网上很多说要用Wordpress for BAE，那可是以前BAE2.0要这样，现在BAE3.0这里使用原版的WordPress（最新版本的，省得更新麻烦）即可，本人亲试真的不需要用修改版的）。</span>  
其实个人觉得BAE3.0用起来就像是一个VPS，没有太多的限制。但在使用过程中有些地方还是需要注意一下，比如上面提到的文件保存问题。  
另外告诉大家一个重要事情，就是BAE3.0从2月1号起正式收费了(2月1日开始计费，先使用后付费，即3月初支付2月账单)，官方给出的计费方式:<a href="http://developer.baidu.com/wiki/index.php?title=docs/cplat/bae/bill" target="_blank" rel="noopener"><a href="http://developer.baidu.com/wiki/index.php?title=docs/cplat/bae/bill">http://developer.baidu.com/wiki/index.php?title=docs/cplat/bae/bill</a></a>  
BAE3.0统一按使用的执行单元套餐计费，计费公式：  
**费用＝套餐单价*使用时长**

<table border="1" cellpadding="5">
  <caption>执行单元套餐</caption> <tr>
    <th>
      套餐名称
    </th>
    
    <th>
      内存(单位：MB)
    </th>
    
    <th>
      磁盘(单位：GB)
    </th>
    
    <th>
      单价(单位：元/天)
    </th>
  </tr>
  
  <tr>
    <td>
      套餐A
    </td>
    
    <td>
      64
    </td>
    
    <td>
      2
    </td>
    
    <td>
      0.1
    </td>
  </tr>
  
  <tr>
    <td>
      套餐B
    </td>
    
    <td>
      128
    </td>
    
    <td>
      2
    </td>
    
    <td>
      0.2
    </td>
  </tr>
  
  <tr>
    <td>
      套餐C
    </td>
    
    <td>
      256
    </td>
    
    <td>
      2
    </td>
    
    <td>
      0.4
    </td>
  </tr>
  
  <tr>
    <td>
      套餐D
    </td>
    
    <td>
      512
    </td>
    
    <td>
      2
    </td>
    
    <td>
      0.7
    </td>
  </tr>
  
  <tr>
    <td>
      套餐E
    </td>
    
    <td>
      1024
    </td>
    
    <td>
      2
    </td>
    
    <td>
      1.3
    </td>
  </tr>
</table>

**特别说明**：

  * 1.因BAE3.0在底层采用“轻量虚拟机技术”，为资源独享型PaaS。固计费指标为您当前占用的执行单元，不论流量大小。但有网络限制：流入5Mbytes/秒；流出5Mbytes/秒。
  * 2.不同配置的执行单元套餐能力评估可参考[256M执行单元压测数据][1]。可根据实际需求选择合适的套餐。

每位开发者都将获得 256M执行单元 720小时的免费使用权，作为开发者使用BAE3.0的试用期(可以跨月使用，直到用满为止；720小时仅针对256M的执行单元，不能折算为其它套餐使用。)

 [1]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/bae#.E6.89.A7.E8.A1.8C.E5.8D.95.E5.85.83.E5.8E.8B.E6.B5.8B "docs/cplat/bae"