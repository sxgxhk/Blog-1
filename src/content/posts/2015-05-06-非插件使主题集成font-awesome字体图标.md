---
title: 非插件使主题集成Font Awesome字体图标
author: Feng
type: post
published: 2015-05-06T06:58:11+00:00
url: /it/243.html
hera_post_view:
  - 5
categories:
  - IT网络
tags:
  - Wordpress

---
[<img loading="lazy" decoding="async" class="aligncenter size-full wp-image-1757" src="http://uu126.cn/wp-content/uploads/2015/05/20150505150126.jpg" alt="20150505150126" width="700" height="305" />][1]  
Font Awesome是一种矢量图标，或者叫图标字体，矢量的好处是无限缩放不会失真，可以适应各种尺寸的屏幕，省掉了做很多图片的麻烦。如果你想在自己的WordPress主题中使用Font Awesome，下面介绍了方法。

  1. 下载<a class="external" href="http://www.bootcss.com/p/font-awesome" target="_blank" rel="noopener">Font Awesome</a>，将font-asesome文件夹直接解压到你主题的根目录下
  2. 打开主题的functions.php，添加如下代码： <pre class="lang:php decode:true " >add_action( ‘wp_enqueue_scripts’, ‘load_fontawesome_styles’ );
function load_fontawesome_styles(){
global $wp_styles;
wp_enqueue_style( ‘font-awesome’, get_template_directory_uri() . ‘/font-awesome/css/font-awesome.min.css’ );
wp_enqueue_style( ‘font-awesome-ie7’, get_template_directory_uri() . ‘/font-awesome/css/font-awesome-ie7.min.css’ );
$wp_styles-&gt;add_data( ‘font-awesome-ie7’, ‘conditional’, ‘lte IE 7’ );
}</pre>
    
    这段代码会引入font awesome主要的css文件，还会条件化加载修复ie7的css样式。

  3. 大功告成，下面就是使用了，使用的方式很多，官方推荐的方法是用i标签加class来添加，例如： <pre class="lang:php decode:true " >&lt;i class=“icon-camera-retro”&gt;&lt;/i&gt;</pre>
    
    当然，也可以将class应用到其它标签，就像使用字体一样，可以设定字号、颜色、阴影等属性。具体使用方法可以看官方文档。
    
    ## 其它说明
    
    需要注意的是font-awesome的css文件和字体文件要保持对应关系，如果你更改了字体目录名称或者位置，不要忘记修改css文件。  
    具体说是修改font-awesome.css这个没压缩的文件，打开文件看开头的几行样式：
    
    <pre class="lang:php decode:true " >@font-face {
font-family: ‘FontAwesome’;
src: url(‘../font/fontawesome-webfont.eot?v=3.1.0′);
src: url(‘../font/fontawesome-webfont.eot?#iefix&v=3.1.0′) format(’embedded-opentype’), url(‘../font/fontawesome-webfont.woff?v=3.1.0′) format(‘woff’), url(‘../font/fontawesome-webfont.ttf?v=3.1.0′) format(‘truetype’), url(‘../font/fontawesome-webfont.svg#fontawesomeregular?v=3.1.0′) format(‘svg’);
font-weight: normal;
font-style: normal;
}</pre>
    
    url里写的就是字体文件路径，根据自己的实际情况修改之。之后将其压缩，就可以用了。  
    另外插件的方式就不说了，直接搜索就可以找到，安装一下就行了，本着能少用则不用的精神，俺还是喜欢代码集成好一点，看个人喜好吧。

 [1]: http://uu126.cn/wp-content/uploads/2015/05/20150505150126.jpg