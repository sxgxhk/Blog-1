---
title: 简易实现 WordPress 自动本地化文章中的外部图片
author: Feng
type: post
published: 2015-03-04T03:02:54+00:00
url: /it/208.html
hera_post_view:
  - 4
categories:
  - IT网络

---
我一直坚持可以不用插件实现的功能尽量不用插件，即使有些插件功能强大，定制很度高。因为很多功能自己更本很少用得上或者是更本用不到。越来越多插件反而让网站越来越复杂沉重，甚至会拖慢你的网站。  
写博客一段时间常常会用到一些网络上的资源，最经常的当然要数图片了，直接引用虽然很简单但是很不可控，因为大多数网站做维护开启了防盗链或者把图片删除了的话我这边的话会有好多404图片。所以我会把图片上传到自己的网站上，每次写文章需要引用的图片很多的话会比较很费力。于是我自己写了一段代码，在文章保存的时候自动将图片本地化，用了几天感觉不错。在这里分享出来，功能比较的简单，我会持续完善这个功能。

### 代码如下：

<pre class="lang:php decode:true " >/************自动下载外部图片开始**************/
function save_post_fix($content){
        global $wpdb;
    $post_id = get_the_ID();
    $upload_dir = wp_upload_dir();
    $path = $upload_dir[“url”];
    $realPath = $upload_dir[“path”];
    $pathbase = $upload_dir[“baseurl”].’/’;
    if(!is_dir($realPath)){
        mkdirs($realPath);
    }
    $pagelink=array();
    $pattern_page = ‘/&lt;img([sS]*?)src=\[“|’](.*?)\[“|’]([sS]*?)&gt;/i’;
    preg_match_all($pattern_page, $content, $pagelink[]);
    foreach ($pagelink[0][2] as $key =&gt; $value) {
        $pic_url = $value;
        $url_feter = parse_url($pic_url);
        if(stripos($url_feter[“host”],“zhnytech.com”)){   //此处修改成自己的网址
            continue;
        }else{
                 $ch = curl_init();
             curl_setopt($ch,CURLOPT_HEADER,1);
             curl_setopt($ch, CURLOPT_NOBODY, TRUE);
             curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);
             curl_setopt($ch,CURLOPT_URL,$pic_url);
             $hd = curl_exec($ch);
             if(!emptyempty($hd) && !(stripos($hd,’Content-Length: image/png’)||stripos($hd,’Content-Length: image/jpg’))){
                $fp =file_get_contents($pic_url);
                $pic_name =basename($url_feter[“path”]);
                $savePath = $realPath.’/’.$pic_name;
                $fullPath = $path.’/’.$pic_name;
                if(file_exists($savePath)){
                    $savePath = $realPath.’/’.str_replace(‘.’,’_’.date(“YmdHis”).‘.’ ,$pic_name);
                    $fullPath = $path.’/’.str_replace(‘.’,’_’.date(“YmdHis”).‘.’ ,$pic_name);
                }
                if(file_put_contents($savePath,$fp)){
                    $content = str_replace($pic_url, $fullPath, $content);
                    $pic_xiangdui = str_replace($pathbase,”,$fullPath);
                    $wpdb-&gt;query(“INSERT INTO zblo1Agd_postmeta (post_id, meta_key, meta_value)  VALUES (‘{$post_id}’, ‘_wp_attached_file’ ,'{$pic_xiangdui}’)”);  //此处需修改成自己的数据库前缀
                    $picSize = getimagesize(‘$fullPath‘);
                    $picInfo =array();
                    $picInfo[‘file’] = $pic_xiangdui;
                    $picInfo[‘width’] = $picSize[0];
                    $picInfo[‘height’] = $picSize[1];
                    $picInfo[‘sizes’] = array();
                    $picInfo[‘image_meta’] = array(
                          ‘aperture’ =&gt; ‘0’,
                          ‘credit’   =&gt; ”,
                          ‘camera’   =&gt;”,
                          ‘caption’  =&gt;”,
                          ‘created_timestamp’ =&gt;’0′,
                          ‘copyright’ =&gt;’0′,
                          ‘focal_length’ =&gt;’0′,
                          ‘iso’         =&gt;’0′,
                          ‘shutter_speed’  =&gt;’0′,
                          ‘title’   =&gt; ”
                        );
                    $picStr = serialize($picInfo);
                    $wpdb-&gt;query(“INSERT INTO zblo1Agd_postmeta (post_id, meta_key, meta_value)  VALUES (‘{$post_id}’, ‘_wp_attachment_metadata’ ,'{$picStr}’)”);  //此处需修改成自己的数据库前缀
                    $daytime= date(“Y-m-d H:i:s”);
                    $daytimegmt =date(“Y-m-d H:i:s”,strtotime(‘-8 hours’));
                    list($pictitle)=explode(‘.’,$pic_name);
                    $wpdb-&gt;query(“
                            INSERT INTO zblo1Agd_posts (post_author, post_date, post_date_gmt,post_content,post_title,post_excerpt,
                            post_status,comment_status,ping_status,post_password,post_name,to_ping,pinged,post_modified,post_modified_gmt,
                            post_content_filtered,post_parent,guid,menu_order,post_type,post_mime_type,comment_count)  VALUES (
                            ‘1’,'{$daytime}’,'{$daytimegmt}’,”,'{$pictitle}’,”,’inherit’,’open’,’open’,”,'{$pictitle}’,”,”,
                            ‘{$daytime}’,'{$daytimegmt}’,”,’0′,'{$fullPath}’,’0′,’attachment’,'”.$picSize[‘mime’].“‘,’0’)”);  //此处需修改成自己的数据库前缀
                }
            }
        }
    }
    return $content;
}
add_filter( ‘content_save_pre’, ‘save_post_fix’);
/************自动下载外部图片结束**************/</pre>