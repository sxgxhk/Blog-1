---
title: '调用WordPress 文章标签[带文章数统计]'
author: Feng
type: post
published: 2016-10-30T04:53:00+00:00
url: /it/320.html
hera_post_view:
  - 3
categories:
  - IT网络
tags:
  - Wordpress

---
我们都知道 `the_tags` 和 `get_the_tags` 可以调用文章标签，但也无非就是调用标签，其实每个标签都包含了很多参数，只调用名字和链接有点太浪费了，所以我们在加上一个小小的文章数统计，瞬间变的高大上起来。

#### 实现方法

下面的代码加到 `functions.php` 中:

<pre><code class="language-php">function fa_get_the_term_list( $id, $taxonomy ) {
$terms = get_the_terms( $id, $taxonomy );
$term_links = "";
if ( is_wp_error( $terms ) )
return $terms;
if ( empty( $terms ) )
return false;
foreach ( $terms as $term ) {
$link = get_term_link( $term, $taxonomy );
if ( is_wp_error( $link ) )
return $link;
$term_links .= &#039;&lt;a href="&#039; . esc_url( $link ) . &#039;" class="js-loaded post--keyword" data-title="&#039; . $term-&gt;name . &#039;" data-type="&#039;. $taxonomy .&#039;" data-term-id="&#039; . $term-&gt;term_id . &#039;"&gt;&#039; . $term-&gt;name . &#039;&lt;sup&gt;[&#039;. $term-&gt;count .&#039;]&lt;/sup&gt;&lt;/a&gt;&#039;;
}
return $term_links;
}</code></pre>

调用方法:在loop中使用下面代码即可: