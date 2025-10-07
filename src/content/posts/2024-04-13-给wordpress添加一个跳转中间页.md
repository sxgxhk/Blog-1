---
title: 给Wordpress添加一个跳转中间页
author: Feng
type: post
published: 2024-04-13T17:32:41+00:00
url: /it/1177.html
hera_post_view:
  - 9
categories:
  - IT网络
tags:
  - Wordpress

---
看到好多人的博客都有这么一个“神奇”的功能，作为一个备案过的网站我认为确实有需要，毕竟要小心对待嘛，但如果是部署是在那啥且也没有那啥的，个人感觉有或没有其实也没那么重要，管它跳转到哪里跟我又有何关系，不过既然人家有了，我没有，是不是感觉会缺少点啥（这个心理呀，真是要不得，不过倒是又给了自己一个折腾的理由）。

<!--more-->

本人作为一个资深的小老白，让我自己写完代码那是万万不可能的，但现在有ChatGpt呀，这玩意已经帮了我不知道多少次忙了，在此我非常正式的感谢一下[OpenAI公司][1]，你们太牛了！好了废话不多说这就开干吧。要实现所有链接（文章、评论）都要强制跳转到中间页（这里以go.php)，也不是很难，在主题的functions.php中加入相应的代码：

<pre class="wp-block-code"><code lang="php" class="language-php">/*链接跳转*/
function redirect_external_links($content) {
    $home_url = home_url(); // 获取WordPress站点的主URL
    // 使用正则表达式匹配所有链接
    return preg_replace_callback('#&lt;a\s+[^&gt;]*href=["\'](.*?)["\'][^&gt;]*&gt;#is', function($matches) use ($home_url) {
        $url = $matches[1]; // 提取URL
        // 检查是否为外部链接
        if (strpos($url, $home_url) === false && filter_var($url, FILTER_VALIDATE_URL)) {
            // 修改URL，通过go.php进行重定向
            $new_url = '/go.php?url=' . urlencode($url);
            return str_replace($matches[1], $new_url, $matches[0]);
        } else {
            // 内部链接不修改
            return $matches[0];
        }
    }, $content);
}
// 添加过滤器，处理文章内容中的链接
add_filter('the_content', 'redirect_external_links');
// 处理评论中的链接
add_filter('comment_text', 'redirect_external_links');
// 处理评论作者链接
function filter_comment_author_link($author_link) {
    $home_url = get_option('home');
    return redirect_external_links($author_link);
}
add_filter('get_comment_author_link', 'filter_comment_author_link');</code></pre>

然后在Wordpress根目录下创建一个go.php文件，具体参考代码如下：

<pre class="wp-block-code"><code lang="php" class="language-php">&lt;?php
// 加载WordPress环境和模板
require_once('wp-load.php');
// 安全检查，确保传递的URL是有效的，防止重定向攻击
$raw_url = isset($_GET['url']) ? $_GET['url'] : 'http://057000.xyz';
$url = filter_var($raw_url, FILTER_VALIDATE_URL) ? $raw_url : 'http://057000.xyz';
?&gt;
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
&lt;meta charset="UTF-8"&gt;
&lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
&lt;title&gt;页面跳转--Feng's Blog&lt;/title&gt;
&lt;style&gt;
    body {
        padding: 0;
        margin: 0;
        font-family: Arial, sans-serif;
        background: #f1f1f1;
        text-align: left;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }
    .container {
    background: #fff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    .url, .countdown {
        margin: 10px 0;
    }
    a.button {
    background: #3498db;
    color: white;
    padding: 10px 20px;
    text-decoration: none;
    border-radius: 5px;
    transition: background-color 0.3s;
    }
    a.button:hover {
    background: #2980b9;
   }
&lt;/style&gt;
&lt;script&gt;
    var countdown = 10; // Countdown in seconds
    var url = '';
    function redirectToUrl() {
        window.location.href = url;
    }
    function updateCountdown() {
        var countdownElement = document.getElementById('countdown');
        countdownElement.innerHTML = `将于 ${countdown} 秒后自动打开...`;
        if(countdown === 0) {
            redirectToUrl();
        } else {
            countdown--;
            setTimeout(updateCountdown, 2000);
        }
    }
    window.onload = function() {
        const params = new URLSearchParams(window.location.search);
        url = params.get('url') || 'http://057000.xyz'; // Default URL if none provided
        var urlElement = document.getElementById('url');
        urlElement.innerHTML = `&lt;strong&gt;即将访问：&lt;/strong&gt; ${url}`;
        setTimeout(updateCountdown, 2000); // Start countdown
    };
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;div class="container"&gt;
    &lt;h1&gt;即将离开Feng's Blog...&lt;/h1&gt;
    &lt;p class="url" id="url"&gt;&lt;/p&gt;
    &lt;p&gt;您即将进行页面跳转，请注意您的帐号和财产安全。&lt;/p&gt;
    &lt;p class="countdown" id="countdown"&gt;&lt;/p&gt;
     &lt;a href="#" onclick="redirectToUrl();" class="button"&gt;继续访问&lt;/a&gt;
&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

记得将上述代码中的057000.xyz改成自己的博客地址就可以了，大概的效果图如下：  
<img decoding="async" src="https://api.uu126.cn/wp-content/uploads/2024/04/wordprss-tiaozhuang.png" alt="" />  
好了，咱们自己的跳转页也就有了，哈哈。

 [1]: https://openai.com "OpenAI公司"