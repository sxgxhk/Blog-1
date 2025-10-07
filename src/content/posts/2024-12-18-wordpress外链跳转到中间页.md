---
title: Wordpress外链跳转到中间页
author: Feng
type: post
published: 2024-12-18T07:56:23+00:00
url: /it/1327.html
hera_post_view:
  - 21
categories:
  - IT网络
tags:
  - Wordpress

---
记得之前还在Wordpress的时候，曾经捣鼓了一个跳转页([原文章链接][1])，后来换成Typecho后，用的是姜先森的主题，也就直接用着他的跳转方式。回到Wordpress(后简称WP)后，就一直没弄，刚好中午闲逛，又让我看到了其它博主的跳转页，感觉不错，那就赶紧“作业抄起来”。<figure class="wp-block-image">

<img decoding="async" src="https://image.uu126.cn/wp-content/uploads/2024/12/20241218133045840.jpg!Tupian01" alt="" /> </figure> 



这个跳转页参照了[空白大佬][2]的，太多技术性的咱就不说了，都是抄作业，下面就细说一下步骤：

<ul class="wp-block-list">
  <li>
    在网站根目录下新建一个文件夹，例如<code> mygo </code>，再在里面新建几个文件如：<code> go.js </code>、 <code>go.html </code>、<code> go.css </code>，跳转页的图片自己抠一下吧。
  </li>
  <li>
    go.js文件内容：
  </li>
</ul>

<pre class="wp-block-code"><code lang="javascript" class="language-javascript">function checkParent(element, classNames) {
    while (element) {
        if (element.classList && classNames.some(cn =&gt; element.classList.contains(cn))) {
            return true;
        }
        element = element.parentElement;
    }
    return false;
}
var excludedClasses = ['card-link', 'friend-item', 'contact-item', 'footer-item']; // 排除的 a 标签类名
window.addEventListener('load', () =&gt; {
    document.body.addEventListener('click', function (e) {
        let target = e.target;

        // 确保点击的目标是 &lt;a&gt; 标签
        while (target && target.nodeName !== 'A') {
            target = target.parentNode;
        }

        // 如果是 &lt;a&gt; 标签并且满足以下条件才触发跳转逻辑
        if (target && target.nodeName === 'A' &&
            target.href && // 确保有 href 属性
            target.href !== '#' && // 排除返回顶部链接
            !checkParent(target, excludedClasses) && // 排除特定类名
            !target.href.startsWith('javascript:') && // 排除 javascript: 链接
            !target.href.includes('zfei.net') && // 排除特定域名
            !target.href.includes('057000.xyz') &&
            target.hostname !== window.location.hostname) { // 仅针对外部链接
            e.preventDefault();

            // Base64 编码目标链接
            let encodedUrl = btoa(target.href);
            let url = '/mygo/go.html?target=' + encodedUrl;

            // 在新窗口中打开跳转页面
            window.open(url, '_blank');
        }
    });
});
</code></pre>

<ul class="wp-block-list">
  <li>
    go.html文件内容：
  </li>
</ul>

<pre class="wp-block-code"><code lang="markup" class="language-markup">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
    &lt;link rel="stylesheet" href="go.css"&gt;
    &lt;title&gt;即将离开知非博客&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;div class="tiaozhuan-all"&gt;
    &lt;div class="tiaozhuan-nrong"&gt;
        &lt;div class="tiaozhuan-title"&gt;您即将离开 『 知非博客 』 ，跳转到以下外部链接&lt;/div&gt;
        &lt;div id="tiaozhuan-link"&gt;&lt;/div&gt;
        &lt;div class="tiaozhuan-info"&gt;请自行识别该链接是否安全，并保管好个人信息。&lt;/div&gt;
        &lt;div class="tiaozhuan-button"&gt;&lt;a href='' id='direct-link'&gt;继续访问&lt;/a&gt;&lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;
&lt;script&gt;
    const params = new URLSearchParams(window.location.search);
    const encodedTarget = params.get('target');
    const target = atob(encodedTarget); // 使用 atob 进行 Base64 解码
    if (target) {
        document.getElementById('direct-link').href = target;
        document.getElementById('tiaozhuan-link').textContent = '' + target; // 直接显示目标地址    
    } else {
        console.error('未指定重定向目标。');
    }
&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

<ul class="wp-block-list">
  <li>
    go.css文件内容：
  </li>
</ul>

<pre class="wp-block-code"><code lang="css" class="language-css">body {
    background: #ececec;
}
.tiaozhuan-all {
    position: relative;
    box-shadow: rgba(0, 0, 0, 0.25) 0px 25px 50px -10px;
    border-radius: 10px;
    background-image: url('go.png');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    color: #666;
    word-break: break-all;
    max-width: 700px;
    height: 350px;
    text-align: center;
    font-size: 0.85rem;
    overflow: hidden;
    margin: 100px auto 0;
    @include breakpoint('small') {
        aspect-ratio: 2 / 1;
        height: auto;
    }
}
.tiaozhuan-nrong {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 20px 20px 30px 20px;
}
.tiaozhuan-title {
    font-size: 1.3rem;
    color: #222;
    line-height: 1.4;
    margin-bottom: 4px;
}
.tiaozhuan-info {
    margin-top: 6px;
}
.tiaozhuan-button {
    margin-top: 20px;
}
.tiaozhuan-button a {
    color: #fc9151;
    border-radius: 4px;
    padding: 10px 30px;
    font-size: .85rem;
    border: 0.5px solid #fc9151;
    display: inline-block;
    text-decoration: none;
}</code></pre>

<ul class="wp-block-list">
  <li>
    最后在主题的<code> footer.php </code>中添加一段代码：<br /><pre><code class="language-php">&lt;script src="/mygo/go.js"&gt;&lt;/script&gt;</code></pre>
    
    <br /><p>
      其实，对于我们浏览体验来说，这样子操作等于多了一步跳转，体验上总归是不好，但为了愉快的玩耍博客，稳妥一点还是需要的。如果觉得跳转中间页很烦人，浏览器可以装个 Skip Redirect 插件，告别所有网站的中间页跳转，直接抵达目标地址。<br /><br />哈哈，跳转功能只运行了几个小时让我撤掉了，正如Jeffer.Z大佬说的：
    </p>
    
    <br /><blockquote>
      <p>
        有备案加是对的，如果不需要备案就无所谓了，我反正是不加，影响大家跳转流畅度感觉
      </p>
    </blockquote>
    
    <br />
  </li>
</ul>

所以说作为一个没有备案的网站，这种影响大家畅游网络的事宜，确实就不需要了，如果是备案网站的话，建议还是加一个跳转，虽然不太友好，但碍于现实也没什么好办法。

 [1]: https://zfei.net/post/1177.html "原文章链接"
 [2]: https://koobai.com/zhongjiantiaozhuan/ "空白大佬"