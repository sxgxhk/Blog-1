---
title: 如何让iphone进入DFU模式
author: Feng
type: post
published: 2015-02-09T13:39:53+00:00
url: /it/205.html
hera_post_view:
  - 5
categories:
  - IT网络

---
[<img loading="lazy" decoding="async" class="alignnone size-full wp-image-1405" src="http://uu126.cn/wp-content/uploads/2015/02/apple-dfu.png" alt="apple dfu" width="600" height="486" />][1]  
&nbsp;  
哈哈，看到这篇文章，估计很多人要吐槽了，这谁不会呀，也是哈，我以前都会的，这不好久没用iphone了，都生疏了，按哪几个键倒是记得，就是把一个顺序忘得…………，唉，老朽了^-^  
先来说明一下，FU的全称是Device Firmware Upgrade，实际意思就是iPhone固件的强制升降级模式。它一般是在iPhone无法开机，iTunes不能识别时或者降级越狱引导时，才会用得到。注意与恢复模式的区别：处于恢复模式的iOS设备的屏幕会显示iTunes +USB画面（不同系统版本设备可能图案略不同）；而DFU模式只能通过连接电脑，用软件来检测，屏幕上不会有任何显示<span style="color: #000000;">（黑屏）</span>。出现前者情况就是失败了。  
下面就来重点了：

<div class="para">
  方法一：开机状态下进入DFU模式
</div>

<ol class="custom_num para-list list-paddingleft-1">
  <li class="list-num-1-1 list-num-paddingleft-1">
    <div class="para">
      用USB线将设备连接上电脑，然后你将会听见电脑已连接成功的提示声音。
    </div>
  </li>
  
  <li class="list-num-1-2 list-num-paddingleft-1">
    <div class="para">
      请先将设备关机，然后你将会听见电脑未连接成功的提示声音。
    </div>
  </li>
  
  <li class="list-num-1-3 list-num-paddingleft-1">
    <div class="para">
      先按住开机键出现Apple Logo，同时按住开关机键和home键，持续直至logo消失，继续按住约4－5秒放开Power键，并继续保持按住home键直至iTunes检测到一台处于恢复模式的iPhone（成功的话iPhone应该处于黑屏状态），用Redsn0w检测的话会在界面下方显示设备型号处于DFU。
    </div>
  </li>
</ol>

<div class="para">
  方法二：任意状态下进入DFU（白苹果或无限重启情况下）
</div>

<ol class="custom_num para-list list-paddingleft-1">
  <li class="list-num-1-1 list-num-paddingleft-1">
    <div class="para">
      连接设备至电脑。
    </div>
  </li>
  
  <li class="list-num-1-2 list-num-paddingleft-1">
    <div class="para">
      直接按住开关机键和home键，持续直至logo消失，按以上步骤操作即可。
    </div>
  </li>
</ol>

<div class="para">
  方法三：不按键进入DFU（建议按键损坏的设备使用）
</div>

<ol class="custom_num para-list list-paddingleft-1">
  <li class="list-num-1-1 list-num-paddingleft-1">
    <div class="para">
      下载最新系统版本对应设备的固件（不能用Apple已经关闭验证的固件）。
    </div>
  </li>
  
  <li class="list-num-1-2 list-num-paddingleft-1">
    <div class="para">
      下载Redsn0w，依次进入Extra －Even More－DFU IPSW
    </div>
  </li>
  
  <li class="list-num-1-3 list-num-paddingleft-1">
    <div class="para">
      此时Redsn0w会提示你这是制作DFU固件的操作，不是正常恢复系统操作。选择是。
    </div>
  </li>
  
  <li class="list-num-1-4 list-num-paddingleft-1">
    <div class="para">
      选择官方最新固件后Redsn0w会开始制作DFU固件，等待完成。
    </div>
  </li>
  
  <li class="list-num-1-5 list-num-paddingleft-1">
    <div class="para">
      打开iTunes关闭Redsn0w，shift+恢复（Mac请用Option+恢复）选择刚制作完成DFU固件（前缀有ENTER_DFU字样），等待恢复过程中出现错误37即可。此时设备已经处于DFU模式。
    </div>
  </li>
</ol>

退出DFU模式也不难，长按Home键和开机键，等出现苹果的Logo就可以了。

 [1]: http://uu126.cn/wp-content/uploads/2015/02/apple-dfu.png