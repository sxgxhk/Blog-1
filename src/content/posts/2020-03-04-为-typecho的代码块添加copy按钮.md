---
title: 为 Typecho的代码块添加Copy按钮
author: Feng
type: post
published: 2020-03-04T05:01:21+00:00
url: /it/567.html
hera_post_view:
  - 4
categories:
  - IT网络
tags:
  - typecho

---
由于目前我用的是`Mirages`主题，所以接下来的步骤也按这个主题来，当然主题不同，也只是改的地方不一样而已，相信这都不是事，要是真有事了欢迎留言哈。

  * 先将以下代码添加到主题`header.php`中的`</head>`标签前，或前往`控制台`&#8211;`设置外观`&#8211;`主题自定义扩展`（考虑到以后更新主题能够更加偷懒，建议还是放到自定义扩展中，将它添加到`自定义 HTML 元素拓展`&#8211;`标签: head 头部 (meta 元素后)`。

<pre><code class="language-js">&lt;script&gt;
    // 在代码块右上角添加复制按钮
    document.addEventListener(&#039;DOMContentLoaded&#039;, initCodeCopyButton);
    function initCodeCopyButton() {
        function initCSS(callback) {
            const css = `
                .btn-code-copy {
                    position: absolute;
                    line-height: .6em;
                    top: .2em;
                    right: .2em;
                    color: rgb(87, 87, 87);
                }
                .btn-code-copy:hover {
                    color: rgb(145, 145, 145);
                    cursor: pointer;
                }
                `;
            const styleId = btoa(&#039;btn-code-copy&#039;).replace(/[=+\/]/g, &#039;&#039;);
            const head = document.getElementsByTagName(&#039;head&#039;)[0];
            if (!head.querySelector(&#039;#&#039; + styleId)) {
                const style = document.createElement(&#039;style&#039;);
                style.id = styleId;
                if (style.styleSheet) {
                    style.styleSheet.cssText = css;
                } else {
                    style.appendChild(document.createTextNode(css));
                }
                head.appendChild(style);
            }
            callback();
        };
        function copyTextContent(source) {
            let result = false;
            const target = document.createElement(&#039;pre&#039;);
            target.style.opacity = &#039;0&#039;;
            target.textContent = source.textContent;
            document.body.appendChild(target);
            try {
                const range = document.createRange();
                range.selectNode(target);
                window.getSelection().removeAllRanges();
                window.getSelection().addRange(range);
                document.execCommand(&#039;copy&#039;);
                window.getSelection().removeAllRanges();
                result = true;
            } catch (e) { console.log(&#039;copy failed.&#039;); }
            document.body.removeChild(target);
            return result;
        };
        function initButton(pre) {
            const code = pre.querySelector(&#039;code&#039;);
            if (code) {
                const preParent = pre.parentElement;
                const newPreParent = document.createElement(&#039;div&#039;);
                newPreParent.style = &#039;position: relative&#039;;
                preParent.insertBefore(newPreParent, pre);
                const copyBtn = document.createElement(&#039;div&#039;);
                copyBtn.innerHTML = &#039;copy&#039;;
                copyBtn.className = &#039;btn-code-copy&#039;;
                copyBtn.addEventListener(&#039;click&#039;, () =&gt; {
                    copyBtn.innerHTML = copyTextContent(code) ? &#039;success&#039; : &#039;failure&#039;;
                    setTimeout(() =&gt; copyBtn.innerHTML = &#039;copy&#039;, 250);
                });
                newPreParent.appendChild(copyBtn);
                newPreParent.appendChild(pre);
            }
        };
        const pres = document.querySelectorAll(&#039;pre&#039;);
        if (pres.length !== 0) {
            initCSS(() =&gt; pres.forEach(pre =&gt; initButton(pre)));
        }
    };
&lt;/script&gt;
</code></pre>

  * 如果像我一样用的是`Mirages`主题，那么还要交前面的代码部分修改，要不然会出现提示拷贝成功，粘贴里却是啥也没有的尴尬情况，具体为：将上述代码第35行的`const target = document.createElement(&#039;pre&#039;);`改成`const target = document.createElement(&#039;textarea&#039;);`

如果你开启了`PJAX`，则需单独加入回调函数。对于本主题，依次进入`控制台 - 外观 - 设置外观 - PJAX(BETA) - PJAX RELOAD`，将`initCodeCopyButton();`添加进入即可。

本文部分内容转载自 [LOGI][1] ，如果你有缘看到这篇文章，也去踩踩他的博客吧。

 [1]: https://logi.im/blog/adding-copy-btn-to-typecho-code-block.html