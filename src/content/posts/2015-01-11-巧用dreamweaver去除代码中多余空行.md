---
title: 巧用Dreamweaver去除代码中多余空行
author: Feng
type: post
published: 2015-01-11T02:19:00+00:00
url: /it/194.html
hera_post_view:
  - 8
categories:
  - IT网络

---
本人对代码之类的不是很精通，但迫于修改，所以还是经常会碰到一些小问题，这不今天就碰到一个PHP文件，可能是作者书写的很规范吧，空行特别多（几百行还是有的吧），手动删了几行，看看那右边的滚动条，实在没有动力再删下去了，这不只好请出我师傅的师娘——百度来，当然结果很让人满意，一切搞定，来分享一下吧：

原来的代码是这样的：

<img decoding="async" src="https://cdn.uu126.cn/wp-content/uploads/2015/01/Dreamweaver1.jpg" alt="请输入图片描述" title="请输入图片描述" />  
使用DW自带的搜索功能，  
利用正则表达式查找 `rns<em>n` ，替换成 `n`  
<img decoding="async" src="https://cdn.uu126.cn/wp-content/uploads/2015/01/Dreamweaver2.jpg" alt="请输入图片描述" title="请输入图片描述" /> 

#### 这里需要注意的，一般默认都是”忽略空白“的，下面这个”使用正则表达式“是没有打勾的

改后效果  
<img decoding="async" src="https://cdn.uu126.cn/wp-content/uploads/2015/01/Dreamweaver3.jpg" alt="请输入图片描述" title="请输入图片描述" />  
使用正则表达式搜索： `s</em>` 即可搜到代码中的空行，再用回车符 替换即可消除代码中的多余空行。