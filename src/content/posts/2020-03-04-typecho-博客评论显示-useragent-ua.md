---
title: Typecho 博客评论显示 UserAgent (UA)
author: Feng
type: post
published: 2020-03-04T04:50:08+00:00
url: /it/565.html
hera_post_view:
  - 3
categories:
  - IT网络
tags:
  - typecho

---
本篇文章纯搬运 [左岸大佬][1] 的教程，之所以搬运也是为了记录下过程，也便于以后时间长了还能再参考着折腾（没办法，文章写不出来多少，折腾这些东西无用的却是十分的来劲）废话不多说，赶紧码字+拷贝记录下来。

<!--more-->

由于目前我用的是Mirages主题，所以接下来也按这个主题来：

<ol class="wp-block-list">
  <li>
    将下面的样式表外链加入到<code>/usr/themes/Mirages/component/header.php</code>的<code>head</code>部分，当然也可通过主题设置界面添加，这里建议大伙把css中的图片下载到本地，以便将来…………。
  </li>
</ol>

<pre class="wp-block-code"><code lang="php" class="language-php">&lt;link rel="stylesheet" href="//cdn.zrahh.com/css/comment-ua.css"&gt;
</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://cdn.lancn.cn/wp-content/uploads/2020/03/1583672377-4209146948.png" alt="typecho_ua.png" /> </figure> 



<ol start="2" class="wp-block-list">
  <li>
    将以下代码加入到<code>/usr/themes/Mirages/function.php</code>末尾
  </li>
</ol>

<pre class="wp-block-code"><code lang="php" class="language-php">// 获取浏览器信息
function getBrowser($agent)
{
    if (preg_match('/MSIE\s([^\s|;]+)/i', $agent, $regs)) {
        $outputer = '&lt;i class="ua-icon icon-ie"&gt;&lt;/i&gt;&nbsp;&nbsp;Internet Explore';
    } else if (preg_match('/FireFox\/([^\s]+)/i', $agent, $regs)) {
      $str1 = explode('Firefox/', $regs[0]);
$FireFox_vern = explode('.', $str1[1]);
        $outputer = '&lt;i class="ua-icon icon-firefox"&gt;&lt;/i&gt;&nbsp;&nbsp;FireFox';
    } else if (preg_match('/Maxthon([\d]*)\/([^\s]+)/i', $agent, $regs)) {
      $str1 = explode('Maxthon/', $agent);
$Maxthon_vern = explode('.', $str1[1]);
        $outputer = '&lt;i class="ua-icon icon-edge"&gt;&lt;/i&gt;&nbsp;&nbsp;MicroSoft Edge';
    } else if (preg_match('#360([a-zA-Z0-9.]+)#i', $agent, $regs)) {
$outputer = '&lt;i class="ua-icon icon-360"&gt;&lt;/i&gt;&nbsp;&nbsp;360极速浏览器';
    } else if (preg_match('/Edge([\d]*)\/([^\s]+)/i', $agent, $regs)) {
        $str1 = explode('Edge/', $regs[0]);
$Edge_vern = explode('.', $str1[1]);
        $outputer = '&lt;i class="ua-icon icon-edge"&gt;&lt;/i&gt;&nbsp;&nbsp;MicroSoft Edge';
    } else if (preg_match('/UC/i', $agent)) {
              $str1 = explode('rowser/',  $agent);
$UCBrowser_vern = explode('.', $str1[1]);
        $outputer = '&lt;i class="ua-icon icon-uc"&gt;&lt;/i&gt;&nbsp;&nbsp;UC浏览器';
    }  else if (preg_match('/QQ/i', $agent, $regs)||preg_match('/QQBrowser\/([^\s]+)/i', $agent, $regs)) {
                  $str1 = explode('rowser/',  $agent);
$QQ_vern = explode('.', $str1[1]);
        $outputer = '&lt;i class= "ua-icon icon-qq"&gt;&lt;/i&gt;&nbsp;&nbsp;QQ浏览器';
    } else if (preg_match('/UBrowser/i', $agent, $regs)) {
              $str1 = explode('rowser/',  $agent);
$UCBrowser_vern = explode('.', $str1[1]);
        $outputer = '&lt;i class="ua-icon icon-uc"&gt;&lt;/i&gt;&nbsp;&nbsp;UC浏览器';
    }  else if (preg_match('/Opera[\s|\/]([^\s]+)/i', $agent, $regs)) {
        $outputer = '&lt;i class= "ua-icon icon-opera"&gt;&lt;/i&gt;&nbsp;&nbsp;Opera';
    } else if (preg_match('/Chrome([\d]*)\/([^\s]+)/i', $agent, $regs)) {
$str1 = explode('Chrome/', $agent);
$chrome_vern = explode('.', $str1[1]);
        $outputer = '&lt;i class="ua-icon icon-chrome"&gt;&lt;/i&gt;&nbsp;&nbsp;Google Chrome';
    } else if (preg_match('/safari\/([^\s]+)/i', $agent, $regs)) {
         $str1 = explode('Version/',  $agent);
$safari_vern = explode('.', $str1[1]);
        $outputer = '&lt;i class="ua-icon icon-safari"&gt;&lt;/i&gt;&nbsp;&nbsp;Safari';
    } else{
        $outputer = '&lt;i class="ua-icon icon-chrome"&gt;&lt;/i&gt;&nbsp;&nbsp;Google Chrome';
    }
    echo $outputer;
}
// 获取操作系统信息
function getOs($agent)
{
    $os = false;

    if (preg_match('/win/i', $agent)) {
        if (preg_match('/nt 6.0/i', $agent)) {
            $os = '&nbsp;&nbsp;&lt;i class= "ua-icon icon-win1"&gt;&lt;/i&gt;&nbsp;&nbsp;Windows Vista&nbsp;/&nbsp;';
        } else if (preg_match('/nt 6.1/i', $agent)) {
            $os = '&nbsp;&nbsp;&lt;i class= "ua-icon icon-win1"&gt;&lt;/i&gt;&nbsp;&nbsp;Windows 7&nbsp;/&nbsp;';
        } else if (preg_match('/nt 6.2/i', $agent)) {
            $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-win2"&gt;&lt;/i&gt;&nbsp;&nbsp;Windows 8&nbsp;/&nbsp;';
        } else if(preg_match('/nt 6.3/i', $agent)) {
            $os = '&nbsp;&nbsp;&lt;i class= "ua-icon icon-win2"&gt;&lt;/i&gt;&nbsp;&nbsp;Windows 8.1&nbsp;/&nbsp;';
        } else if(preg_match('/nt 5.1/i', $agent)) {
            $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-win1"&gt;&lt;/i&gt;&nbsp;&nbsp;Windows XP&nbsp;/&nbsp;';
        } else if (preg_match('/nt 10.0/i', $agent)) {
            $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-win2"&gt;&lt;/i&gt;&nbsp;&nbsp;Windows 10&nbsp;/&nbsp;';
        } else{
            $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-win2"&gt;&lt;/i&gt;&nbsp;&nbsp;Windows X64&nbsp;/&nbsp;';
        }
    } else if (preg_match('/android/i', $agent)) {
    if (preg_match('/android 9/i', $agent)) {
            $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-android"&gt;&lt;/i&gt;&nbsp;&nbsp;Android Pie&nbsp;/&nbsp;';
        }
    else if (preg_match('/android 8/i', $agent)) {
            $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-android"&gt;&lt;/i&gt;&nbsp;&nbsp;Android Oreo&nbsp;/&nbsp;';
        }
    else{
            $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-android"&gt;&lt;/i&gt;&nbsp;&nbsp;Android&nbsp;/&nbsp;';
    }
    }
    else if (preg_match('/ubuntu/i', $agent)) {
        $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-ubuntu"&gt;&lt;/i&gt;&nbsp;&nbsp;Ubuntu&nbsp;/&nbsp;';
    } else if (preg_match('/linux/i', $agent)) {
        $os = '&nbsp;&nbsp;&lt;i class= "ua-icon icon-linux"&gt;&lt;/i&gt;&nbsp;&nbsp;Linux&nbsp;/&nbsp;';
    } else if (preg_match('/iPhone/i', $agent)) {
        $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-apple"&gt;&lt;/i&gt;&nbsp;&nbsp;iPhone&nbsp;/&nbsp;';
    } else if (preg_match('/mac/i', $agent)) {
        $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-mac"&gt;&lt;/i&gt;&nbsp;&nbsp;MacOS&nbsp;/&nbsp;';
    }else if (preg_match('/fusion/i', $agent)) {
        $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-android"&gt;&lt;/i&gt;&nbsp;&nbsp;Android&nbsp;/&nbsp;';
    } else {
        $os = '&nbsp;&nbsp;&lt;i class="ua-icon icon-linux"&gt;&lt;/i&gt;&nbsp;&nbsp;Linux&nbsp;/&nbsp;';
    }
    echo $os;
}
</code></pre>

<ol start="3" class="wp-block-list">
  <li>
    将以下代码添加到<code>/usr/themes/Mirages/lib/comments.php</code>中<code>122</code>行所在的<code>div</code>中
  </li>
</ol>

<pre class="wp-block-code"><code lang="php" class="language-php">&lt;span class="comment-ua"&gt;
    &lt;?php getOs($this-&gt;agent); ?&gt;
    &lt;?php getBrowser($this-&gt;agent); ?&gt;
&lt;/span&gt;
</code></pre>

本文部分内容转载自 [LOGI][2] ，如果你有缘看到这篇文章，也去踩踩他的博客吧。

 [1]: https://www.zrahh.com/archives/298.html
 [2]: https://logi.im/blog/user-agent-in-typecho-comment.html