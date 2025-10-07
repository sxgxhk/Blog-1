---
title: Typecho CommentToMail邮件样式分享
author: Feng
type: post
published: 2018-04-09T03:18:05+00:00
url: /it/441.html
hera_post_view:
  - 3
categories:
  - IT网络
tags:
  - typecho

---
刚在逛博客圈，发现有个Typecho的CommentToMail的邮件样式挺美的，虽然我现在已经入了Ghost门，但本着一种折腾不息的心理（万一哪天心情不顺又杀回Typecho呢，哈哈），于是就顺手摘录到我家宝典了，具体如下：

#### Guest样式

怎么样？挺美的吧，感觉比我在用Typecho时的样式美多了，喜欢就赶紧把下面的代码Down走吧：

#### Guest样式源码

<pre><code class="language-php">&lt;pre class="wp-block-code"&gt;```
&lt;table style=width: 99.8%;height:99.8% &gt;&lt;tbody&gt;&lt;tr&gt;&lt;td style=background:#fafafa url(https://a.photo/images/2018/03/24/2017113018325846288465.png)&gt;
    &lt;div style=border-radius: 10px 10px 10px 10px;font-size:13px;    color: #555555;width: 666px;font-family:&#039;Century Gothic&#039;,&#039;Trebuchet MS&#039;,&#039;Hiragino Sans GB&#039;,微软雅黑,&#039;Microsoft Yahei&#039;,Tahoma,Helvetica,Arial,&#039;SimSun&#039;,sans-serif;margin:50px auto;border:1px solid #eee;max-width:100%;background: #ffffff repeating-linear-gradient(-45deg,#fff,#fff 1.125rem,transparent 1.125rem,transparent 2.25rem);box-shadow: 0 1px 5px rgba(0, 0, 0, 0.15);&gt;
        &lt;div style=width:100%;background:#49BDAD;color:#ffffff;border-radius: 10px 10px 0 0;background-image: -moz-linear-gradient(0deg, rgb(67, 198, 184), rgb(255, 209, 244));background-image: -webkit-linear-gradient(0deg, rgb(67, 198, 184), rgb(255, 209, 244));height: 66px;&gt;
            &lt;p style=font-size:15px;word-break:break-all;padding: 23px 32px;margin:0;background-color: hsla(0,0%,100%,.4);border-radius: 10px 10px 0 0;&gt;您在&lt;a style=text-decoration:none;color: #ffffff; href=https://www.liuguogy.com&gt; {siteTitle} &lt;/a&gt;上的留言有新回复啦！
            &lt;/p&gt;
        &lt;/div&gt;
        &lt;div style=margin:40px auto;width:90%&gt;
            &lt;p&gt;{author_p} 同学，您曾在文章《{title}》上发表评论:&lt;/p&gt;
            &lt;p style=background: #fafafa repeating-linear-gradient(-45deg,#fff,#fff 1.125rem,transparent 1.125rem,transparent 2.25rem);box-shadow: 0 2px 5px rgba(0, 0, 0, 0.15);margin:20px 0px;padding:15px;border-radius:5px;font-size:14px;color:#555555;&gt;{text_p}&lt;/p&gt;
            &lt;p&gt;{author} 给您的回复如下：&lt;/p&gt;
            &lt;p style=background: #fafafa repeating-linear-gradient(-45deg,#fff,#fff 1.125rem,transparent 1.125rem,transparent 2.25rem);box-shadow: 0 2px 5px rgba(0, 0, 0, 0.15);margin:20px 0px;padding:15px;border-radius:5px;font-size:14px;color:#555555;&gt;{text}&lt;/p&gt;
              &lt;p&gt;您可以点击 &lt;a style=text-decoration:none; color:#12addb href={permalink}&gt;查看回复的完整內容 &lt;/a&gt;，欢迎再次光临 &lt;a style=text-decoration:none; color:#12addb href=https://www.liuguogy.com&gt; {siteTitle} &lt;/a&gt;。&lt;/p&gt;
            &lt;style type=text/css&gt;a:link{text-decoration:none}a:visited{text-decoration:none}a:hover{text-decoration:none}a:active{text-decoration:none}&lt;/style&gt;
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/td&gt;&lt;/tr&gt;&lt;/tbody&gt;&lt;/table&gt;</code></pre>

#### Owners样式源码

<pre><code class="language-php">&lt;pre class="wp-block-code"&gt;```
&lt;style&gt;
    .wrap span {
        display: inline-block;
    }
    .w260{ width: 260px;}
    .w20{ width: 20px;}
    .wauto{ width: auto;}
&lt;/style&gt;
&lt;table style=width: 99.8%;height:99.8% &gt;&lt;tbody&gt;&lt;tr&gt;&lt;td style=background:#fafafa url(https://a.photo/images/2018/03/24/2017113018325846288465.png)&gt;
    &lt;div style=border-radius: 10px 10px 10px 10px;font-size:13px;    color: #555555;width: 666px;font-family:&#039;Century Gothic&#039;,&#039;Trebuchet MS&#039;,&#039;Hiragino Sans GB&#039;,微软雅黑,&#039;Microsoft Yahei&#039;,Tahoma,Helvetica,Arial,&#039;SimSun&#039;,sans-serif;margin:50px auto;border:1px solid #eee;max-width:100%;background: #ffffff repeating-linear-gradient(-45deg,#fff,#fff 1.125rem,transparent 1.125rem,transparent 2.25rem);box-shadow: 0 1px 5px rgba(0, 0, 0, 0.15);&gt;
        &lt;div style=width:100%;background:#49BDAD;color:#ffffff;border-radius: 10px 10px 0 0;background-image: -moz-linear-gradient(0deg, rgb(67, 198, 184), rgb(255, 209, 244));background-image: -webkit-linear-gradient(0deg, rgb(67, 198, 184), rgb(255, 209, 244));height: 66px;&gt;
            &lt;p style=font-size:15px;word-break:break-all;padding: 23px 32px;margin:0;background-color: hsla(0,0%,100%,.4);border-radius: 10px 10px 0 0;&gt;您的&lt;a style=text-decoration:none;color: #ffffff; href=https://www.liuguogy.com&gt; {siteTitle} &lt;/a&gt;上有新的评论啦！
            &lt;/p&gt;
        &lt;/div&gt;
        &lt;div style=margin:40px auto;width:90%&gt;
            &lt;p&gt;{author} 在您文章《{title}》上发表评论:&lt;/p&gt;
            &lt;p style=background: #fafafa repeating-linear-gradient(-45deg,#fff,#fff 1.125rem,transparent 1.125rem,transparent 2.25rem);box-shadow: 0 2px 5px rgba(0, 0, 0, 0.15);margin:20px 0px;padding:15px;border-radius:5px;font-size:14px;color:#555555;&gt;{text}&lt;/p&gt;

            &lt;p class=wrap style=text-decoration:none&gt;&lt;span class=w260&gt;时间：{time}&lt;/span&gt;&lt;span class=w20&gt; &lt;/span&gt;&lt;span class=wauto&gt;IP：{ip}&lt;/span&gt;&lt;/p&gt;
            &lt;p class=wrap style=text-decoration:none&gt;&lt;span class=w260&gt;邮箱：{mail}&lt;/span&gt;&lt;span class=w20&gt; &lt;/span&gt;&lt;span class=wauto&gt;状态：{status}&lt;/span&gt;&lt;/p&gt;
            &lt;p&gt;&lt;a style="text-decoration:none;" href="{permalink}" target=&#039;_blank&#039; rel="noopener"&gt;[查看评论]&lt;/a&gt; | &lt;a style="text-decoration:none;" href="{manage}" target=&#039;_blank&#039; rel="noopener"&gt;[管理评论] &lt;/a&gt;&lt;/p&gt;
            &lt;style type=text/css&gt;a:link{text-decoration:none}a:visited{text-decoration:none}a:hover{text-decoration:none}a:active{text-decoration:none}&lt;/style&gt;
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/td&gt;&lt;/tr&gt;&lt;/tbody&gt;&lt;/table&gt;</code></pre>

摘录完毕，感谢[@Linger][1]的分享，等我转战回Typecho时也可以使用这么美美的邮件提醒样式了。

 [1]: https://www.liuguogy.com/