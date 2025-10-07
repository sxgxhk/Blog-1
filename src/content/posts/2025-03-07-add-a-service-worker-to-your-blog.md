---
title: 给博客加一个Service Worker耍耍
author: Feng
type: post
published: 2025-03-07T14:31:37+00:00
url: /it/1376.html
praise:
  - 1
hera_post_view:
  - 11
categories:
  - IT网络
tags:
  - Wordpress

---
先说个题外话，上次抄了沉沦大佬的作业《[适配评论头像本地缓存功能][1]》，实现了头像下载并缓存到主机上，加快了头像的加载速度，不过在我的博客上却碰了一些问题：一些没有头像或头像链接失效的，就拖慢了页面有显示，最终交由DeepSeek修正了下，完美解决了我的这个问题，涉及的部分代码如下：

<pre class="wp-block-code"><code lang="php" class="language-php">// 定义头像缓存目录
define('AVATAR_CACHE_DIR', WP_CONTENT_DIR . '/avatars');
// 定义头像缓存URL
define('AVATAR_CACHE_URL', WP_CONTENT_URL . '/avatars');
// 定义头像缓存有效期，默认7天
define('AVATAR_CACHE_LIFETIME', apply_filters('avatar_cache_lifetime', 7 * DAY_IN_SECONDS));
// 定义头像最大存储时间，默认30天
define('AVATAR_CLEANUP_AGE', apply_filters('avatar_max_age', 30 * DAY_IN_SECONDS));
// 定义默认头像URL
define('DEFAULT_AVATAR_URL', '/wp-content/uploads/2025/03/default.webp');

/**
 * 缓存用户头像到本地
 *
 * @param string $email 用户邮箱
 * @param array $args 头像参数
 * @return string 头像URL
 */
function cache_avatar_locally($email, $args = array()) {
    // 检查WP_Filesystem函数是否存在，若不存在则加载文件操作类
    if (!function_exists('WP_Filesystem')) {
        require_once ABSPATH . 'wp-admin/includes/file.php';
    }
    WP_Filesystem();
    global $wp_filesystem;
    // 默认头像参数
    $default_args = array(
        'default' =&gt; DEFAULT_AVATAR_URL,
        'size'    =&gt; 96,
        'rating'  =&gt; 'g',
        'scheme'  =&gt; null
    );
    $args = wp_parse_args($args, $default_args);
    $args = apply_filters('avatar_cache_params', $args, $email);
    // 对参数进行排序，以确保生成一致的hash值
    $sorted_args = ksort_deep($args);
    $param_string = http_build_query($sorted_args);
    // 根据用户邮箱和参数生成唯一的hash值
    $hash = md5(strtolower(trim($email)) . '|' . $param_string);
    $base_path = AVATAR_CACHE_DIR . '/' . $hash;
    // 查找是否已有缓存的头像文件
    $avatar_file = find_existing_avatar($base_path);
    if ($avatar_file) {
        // 如果头像文件存在且需要刷新，则安排刷新操作
        if (should_refresh_avatar($avatar_file)) {
            schedule_avatar_refresh($email, $args);
        }
        // 返回头像的URL
        return str_replace(AVATAR_CACHE_DIR, AVATAR_CACHE_URL, $avatar_file);
    }
    // 获取Gravatar头像URL
    $gravatar_url = get_avatar_url($email, $args);
    // 获取头像内容
    $response = wp_remote_get($gravatar_url, array('timeout' =&gt; 10));
    // 如果请求失败，则返回默认头像URL
    if (is_wp_error($response) || 200 !== wp_remote_retrieve_response_code($response)) {
        return $args['default'];
    }
    // 获取图片类型
    $content_type = wp_remote_retrieve_header($response, 'content-type');
    // 获取文件扩展名
    $ext = get_extension_from_mime($content_type);
    // 设置缓存头像的路径
    $avatar_path = "{$base_path}.{$ext}";
    $avatar_dir = dirname($avatar_path);
    // 如果缓存目录不存在，则创建目录
    if (!file_exists($avatar_dir)) {
        wp_mkdir_p($avatar_dir);
    }
    // 将头像内容保存到本地
    if ($wp_filesystem-&gt;put_contents($avatar_path, wp_remote_retrieve_body($response), 0644)) {
        return AVATAR_CACHE_URL . "/{$hash}.{$ext}";
    }
    // 如果保存失败，则返回默认头像URL
    return $args['default'];
}

/**
 * 深度排序数组
 *
 * @param array $array 输入数组
 * @return array 排序后的数组
 */
function ksort_deep($array) {
    if (is_array($array)) {
        ksort($array);
        foreach ($array as $key =&gt; $value) {
            $array[$key] = ksort_deep($value);
        }
    }
    return $array;
}

/**
 * 查找已存在的头像文件
 *
 * @param string $base_path 头像缓存基础路径
 * @return string|null 头像文件路径，若没有则返回null
 */
function find_existing_avatar($base_path) {
    $files = glob("{$base_path}.*");
    foreach ($files as $file) {
        if (is_file($file) && in_array(pathinfo($file, PATHINFO_EXTENSION), ['jpg', 'jpeg', 'png', 'webp'])) {
            return $file;
        }
    }
    return null;
}</code></pre>

<img decoding="async" src="https://image.uu126.cn/wp-content/uploads/2025/03/20250307221718523.webp!Tupian01" alt="" />  
好了，言归正传，开始今天的唠叨话题吧——给博客加个Service Workers，网上类似的代码有很多，有些甚至还要收费（小小鄙视一下），好在现在各种AI工具加持，终于有了适合自己的代码，大概的步骤如下：

<ul class="wp-block-list">
  <li>
    在网站根目录下创建sw.js文件，这个在移动终端上也适应了（之前出现了电脑端访问时头像显示正常，在移动端时无法显示），大致的内容如下：
  </li>
</ul>

<pre class="wp-block-code"><code lang="javascript" class="language-javascript">// 配置中心
const CACHE_NAME = 'wp-sw-desktop-v2';
const OFFLINE_URL = '/offline.html';
const VALID_SCHEMES = ['http:', 'https:'];
const STATIC_EXTS = ['css', 'js', 'png', 'jpg', 'webp', 'svg'];
const UPLOAD_PATHS = ['/wp-content/uploads/', '/wp-content/avatars/'];
// 预缓存清单（桌面端专用）
const PRECACHE_RESOURCES = [
  '/',
  '/index.php',
  '/wp-content/themes/主题/style.css',
  '/wp-content/themes/主题/static/helper.js',
  '/wp-content/themes/主题/static/lang.js',
  '/wp-content/themes/主题/static/script.js',
  '/wp-content/themes/主题/static/modules.js',
  '/wp-content/themes/主题/static/package.js',
  '/favicon.ico',
  OFFLINE_URL
];
// 安装阶段：增强型预缓存
self.addEventListener('install', (event) =&gt; {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache =&gt; {
        return Promise.all(
          PRECACHE_RESOURCES.map(url =&gt; 
            cache.add(url).catch(err =&gt; 
              console.error(`预缓存失败: ${url}`, err)
            )
          )
        );
      })
      .then(() =&gt; self.skipWaiting())
      .catch(err =&gt; {
        console.error('安装失败:', err);
        self.skipWaiting();
      })
  );
});
// 激活阶段：清理旧缓存
self.addEventListener('activate', (event) =&gt; {
  event.waitUntil(
    caches.keys().then(keys =&gt; 
      Promise.all(keys.map(key =&gt; 
        key !== CACHE_NAME && caches.delete(key)
      ))
    ).then(() =&gt; self.clients.claim())
  );
});
// 请求处理：智能缓存策略
self.addEventListener('fetch', event =&gt; {
  const { request } = event;
  const url = new URL(request.url);
  // 安全过滤
  if (!VALID_SCHEMES.includes(url.protocol)) return;
  // 缓存策略路由
  event.respondWith(
    cacheFirstWithUpdate(request)
  );
});
// 核心缓存策略
async function cacheFirstWithUpdate(request) {
  try {
    // 优先返回缓存
    const cached = await caches.match(request);
    if (cached) return cached;
    // 网络请求
    const netRes = await fetch(request);
    // 动态缓存
    if (shouldCache(request, netRes)) {
      cachePut(request, netRes.clone());
    }
    return netRes;
  } catch (err) {
    // 离线回退
    return handleOffline(request);
  }
}
// 缓存条件判断
function shouldCache(req, res) {
  const url = new URL(req.url);
  return res.status === 200 &&
    (STATIC_EXTS.some(ext =&gt; url.pathname.endsWith(`.${ext}`)) ||
     UPLOAD_PATHS.some(path =&gt; url.pathname.startsWith(path)));
}
// 安全存储
async function cachePut(req, res) {
  try {
    const cache = await caches.open(CACHE_NAME);
    await cache.put(req, res);
  } catch (err) {
    console.error('缓存存储失败:', req.url, err);
  }
}
// 离线处理
async function handleOffline(req) {
  if (req.destination === 'document') {
    return (await caches.match(OFFLINE_URL)) || Response.redirect(OFFLINE_URL);
  }
  return new Response('', { 
    status: 503,
    headers: { 'Content-Type': 'text/html' } 
  });
}</code></pre>

<ul class="wp-block-list">
  <li>
    在网站根目录下创建 offline.html，具体的代码如下：
  </li>
</ul>

<pre class="wp-block-code"><code lang="markup" class="language-markup">&lt;!-- 创建/offline.html --&gt;
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;离线模式&lt;/title&gt;
  &lt;meta charset="utf-8"&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;h1&gt;您处于离线状态，部分内容可能无法显示&lt;/h1&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>

<ul class="wp-block-list">
  <li>
    在主题的header.php文件加入以下代码：
  </li>
</ul>

<pre class="wp-block-code"><code lang="javascript" class="language-javascript">&lt;script&gt;
// 移动端检测函数（综合 UA 和屏幕尺寸）
function isMobile() {
  const ua = navigator.userAgent;
  const isMobileUA = /Android|iPhone|iPad|iPod|Windows Phone/i.test(ua);
  const isMobileScreen = window.matchMedia('(max-width: 768px)').matches;
  return isMobileUA || isMobileScreen;
}
// Service Worker 注册控制
if ('serviceWorker' in navigator && !isMobile()) {
  navigator.serviceWorker.register('/sw.js')
    .then(reg =&gt; console.log('SW 已注册:', reg))
    .catch(err =&gt; console.error('SW 注册失败:', err));
} else if (isMobile()) {
  // 强制注销移动端可能存在的旧 SW
  navigator.serviceWorker.getRegistrations().then(registrations =&gt; {
    registrations.forEach(reg =&gt; reg.unregister());
    console.log('已禁用移动端 Service Worker');
  });
}
&lt;/script&gt;</code></pre>

一切添加完毕后，打开首页（建议清除一下缓存），按F12键&#8211;Application&#8211;Service Workers，如果没有报错，Status显示小绿圆的话，说明就OK了，当然以上代码我在目前用的主题是可以的，不代表其它主题就没有问题，另外加了Service Worekers能不能明显提升加载速度，这个还得再使用一段时间看看，个人感觉不是很明显（这个主题用起来本身也不是很慢，VPS线路好的话更加没的说），所以是骡子是马，还得拉出来溜溜不是嘛。

 [1]: https://kkn.me/3933.html "适配评论头像本地缓存功能"