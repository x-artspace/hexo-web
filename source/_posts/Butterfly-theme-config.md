---
title: Butterfly 主题配置及美化
top: true
cover: /img/blog-butterfly.jpg
categories: Web
tag: Hexo
abbrlink: b9872036
---
### 安装butterfly主题

```shell
$ npm i hexo-theme-butterfly
# 通过 npm 安装并不会在 themes 里生成主题文件夹，而是在 node_modules 里生成
# git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

#### 升级检查

```shell
$ npm update hexo-theme-butterfly
```

#### 应用主题

修改`Hexo`根目录下`_config.yml`,把主题改为`butterfly`

![image-20221110094830555](C:\Users\ericr\AppData\Roaming\Typora\typora-user-images\image-20221110094830555.png)

#### 修改配置文件

为了减少升级主题后带来的不便，在 `hexo` 的根目录创建一个文件` _config.butterfly.yml`，并把主题目录的 `_config.yml `内容复制到 `_config.butterfly.yml` 去。( **注意: 复制的是主题的` _config.yml` ,而不是 `hexo` 的` _config.yml`**)

```shell
$ cd node_modules/hexo-theme-butterfly/
$ cp _config.yml ../../_config.butterfly.yml
```

![image-20221110100416162](C:\Users\ericr\AppData\Roaming\Typora\typora-user-images\image-20221110100416162.png)

**注意： 不要把主题目录的 `_config.yml `删掉**

**注意： 以后只需要在` _config.butterfly.yml`进行配置就行。
如果使用了 `_config.butterfly.yml`， 配置主题的`_config.yml `将不会有效果。**

Hexo会自动合并主题中的`_config.yml`和` _config.butterfly.yml`里的配置，如果存在同名配置，会使用`_config.butterfly.yml`的配置，其优先度较高。

#### 安装插件

安装pug以及stylus的渲染器

```shell
$ npm install hexo-renderer-pug hexo-renderer-stylus --save
```

### 设置网站个人资料

#### 网站标题设置

修改站点配置文件`_config.yml`

```shell
# Site
title: X-artSpace #网站名称
subtitle: ''
description: '人生是一场盛大的烟火' # 个性签名
keywords:
author: Eric Ray # 作者
language: zh-CN #语言
timezone: 'Asia/Shanghai' # 时区
```

#### 网站URL

此处url涉及到版权信息跳转URL

```yaml
# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: http://x-artspace.github.io
```

#### 部署站点设置

1. 安装hexo-deployer-git

   ```shell
   $ npm install hexo-deployer-git --save
   ```

2. 修改站点配置文件

   ```yaml
   # Deployment
   ## Docs: https://hexo.io/docs/one-command-deployment
   deploy:
     type: git
     repo: https://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@github.com/x-artspace/x-artspace.github.io.git # 注意github使用令牌
     branch: main
   ```

3. 部署命令

   ```shell
   $ hexo clean && hexo deploy
   ```

#### 生成文章唯一链接

Hexo 的默认文章链接格式是年，月，日，标题这种格式来生成的。如果你的标题是中文的话，那你的 URL 链接就会包含中文。

安装插件

```yaml
# 在hexo站点目录下安装
npm install hexo-abbrlink --save
```

在配置文件`_config.yml`

```yaml
# permalink: :year/:month/:day/:title/
permalink: post/:abbrlink.html # post为自定义前缀
abbrlink:
	  alg: crc32   #算法： crc16(default) and crc32
	  rep: hex     #进制： dec(default) and hex
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks
```

### 主题设置

#### 修改主题配置文件

在主题配置文件`_config.butterfly.yml`进行如下设置

```yaml
menu:
    主页: / || fas fa-home
    文章 || fas fa-book:
      分类: /categories/ || fa fa-archive
      标签: /tags/ || fa fa-tags
      归档: /archives/ || fa fa-folder-open
    娱乐 || fas fa-list:
      相册: /photos/ || fa fa-camera-retro
      音乐: /music/ || fa fa-music
      影视: /movies/ || fas fa-video
    友链: /links/ || fa fa-link
    留言板: /comment/ || fa fa-paper-plane

```

#### 标签页

1. 在hexo博客的根目录，输入`hexo new page tags`

2. 找到`source/tags/index.md`这个文件

3. 修改文件如下：

   ```shell
   ---
   title: 标签
   date: 2022-11-10 13:12:21
   type: "tags"
   ---
   
   ```

   **记得添加`type: "tags"`**

#### 分类页

1. 同样在hexo博客根目录输入`hexo new page categories`

2. 修改`source/categories/index.md`

   ```shell
   ---
   title: 分类
   date: 2022-11-10 13:12:41
   type: "categories"
   ---
   
   ```

#### 其他页面

根据自己主页面设置，分别添加对应页。我的设置如下

```shell
# 归档
$ hexo new page archives
# 相册
$ hexo new page photos
# 音乐
$ hexo new page music
# 影视
$ hexo new page movies
# 友链
$ hexo new page links
# 留言板
$ hexo new page comment
# 关于我们
$ hexo new page about
```

#### 添加友情链接

在Hexo博客目录中的`source/_data`（如果没有 _data 文件夹，请自行创建）中创建一个`link.yml`。

```yaml
- class_name: 友情链接
  class_desc: 那些人，那些事
  link_list:
    - name: Hexo
      link: https://hexo.io/zh-tw/
      avatar: https://d33wubrfki0l68.cloudfront.net/6657ba50e702d84afb32fe846bed54fba1a77add/827ae/logo.svg
      descr: 快速、简单且强大的网志框架

- class_name: 网站
  class_desc: 值得推荐的网站
  link_list:
    - name: Youtube
      link: https://www.youtube.com/
      avatar: https://i.loli.net/2020/05/14/9ZkGg8v3azHJfM1.png
      descr: 视频网站
    - name: Weibo
      link: https://www.weibo.com/
      avatar: https://i.loli.net/2020/05/14/TLJBum386vcnI1P.png
      descr: 中国最大社交分享平台
    - name: Twitter
      link: https://twitter.com/
      avatar: https://i.loli.net/2020/05/14/5VyHPQqR6LWF39a.png
      descr: 社交分享平台
```

#### 添加社交图标

Butterfly支持` font-awesome v6`图标.

书写格式 `图标名：url || 描述性文字`

修改**主题配置文件**

```yaml
# social settings (社交圖標設置)
# formal:
#   icon: link || the description
social:
  fab fa-github: https://github.com/x-artspace || Github
  fas fa-envelope: mailto:ericray.tech@outlook.com || Email
```

#### 版权设置

修改主题配置文件：

```yaml
post_copyright:
  enable: true
  decode: true
  author_href: mailto:ericray.tech@outlook.com # https://x-artspace.github.io 点击作者名字发邮件
  license: CC BY-NC-SA 4.0
  license_url: https://creativecommons.org/licenses/by-nc-sa/4.0/
```

#### 去掉底部Hexo标志

方法一：修改文件：`node_modules/hexo-theme-butterfly/layout/includes/footer.pug:`

```yaml
#footer-wrap
  if theme.footer.owner.enable
    - var now = new Date()
    - var nowYear = now.getFullYear()
    if theme.footer.owner.since && theme.footer.owner.since != nowYear
      .copyright!= `&copy;${theme.footer.owner.since} - ${nowYear} By ${config.author}`
    else
      .copyright!= `&copy;${nowYear} By ${config.author}`
  if theme.footer.copyright
    .framework-info
      //-span= _p('footer.framework') + ' '
      //-a(href='https://hexo.io')= 'Hexo'
      //-span.footer-separator |
      //-span= _p('footer.theme') + ' '
      //-a(href='https://github.com/jerryc127/hexo-theme-butterfly')= 'Butterfly'
      span= 'Power By' + ' '
      a(href='https://x-artspace.github.io')= 'X-artSpace'
      span.footer-separator |
      span= 'Author' + ' '
      // a(href='https://blog.csdn.net/ericleiy')= 'X-Ray'
      a(href='mailto:ericray.tech@outlook.com')= 'X-Ray'
  if theme.footer.custom_text
    .footer_custom_text!=`${theme.footer.custom_text}`

```

方法二：修改主题配置文件

```yaml
footer:
  owner:
    enable: true
    since: 2020
  custom_text: Welcome to my blog!
  copyright: false  # Copyright of theme and framework
```



### 图片设置

图片可以用云图片链接或者放在本地文件夹位置：`node_modules/hexo-theme-butterfly/source/img`

均在主题配置文件中做修改。

#### 网站图标

```yaml
# Favicon
favicon: /img/favicon.png
```

#### 头像

```yaml
avatar:
  img: /img/avatar.jpg #图片路径
  effect: false #头像会一直转圈  
```

#### 主页封面图片

```yaml
# The banner image of home page
index_img: /img/background.jpg
```

#### 文章详情页的顶部图片

当没有在`front-matter`设置`top_img`和`cover`的情况下会显示该图
修改主题配置文件`_config.butterfly.yml`：

```yaml
# If the banner of page not setting, it will show the top_img
default_top_img: /img/default_top_img.jpg
```

#### 归档页顶部图片

```yaml
# The banner image of archive page
archive_img: /img/archive.jpg
```

#### tag页顶部图

```yaml
#tag页（标签页）
# If the banner of tag page not setting, it will show the top_img
# note: tag page, not tags page (子標籤頁面的 top_img)
tag_img: /img/tag_img.jpg
```

#### category页顶部图

```yaml
#category页
# If the banner of category page not setting, it will show the top_img
# note: category page, not categories page (子分類頁面的 top_img)
category_img: /img/category_img.jpg
```

#### 文章封面图

每篇文章都可以设置一张封面，可以为每篇文章设置默认封面

也可以修改每个md文件的front-matter的cover属性，会覆盖上面的默认封面。修改主题配置文件`_config.butterfly.yml：`

```yaml
cover:
  index_enable: true #  是否展示文章封面
  aside_enable: true
  archives_enable: true
  position: both # 封面展示的位置 left/right/both
  # 当没有设置cover时，默认展示的文章封面
  default_cover:
    # 当配置多张图片时，会随机选择一张作为 cover. 此时写法为
    - https:
    - http:
    - http:
    - http:
    - http:
    - http:
```

#### 错误页面

```yaml
# Replace Broken Images (替換無法顯示的圖片)
error_img:
  flink: /img/friend_404.gif
  post_page: /img/404.jpg
```

#### 图片懒加载

新增`hexo-lazyload-image`模块

```shell
# 在hexo网站目录下执行安装
npm install hexo-lazyload --save
```

在**主目录配置文件**`_config.yml`增加配置

```yaml
lazyload:
  enable: true
  loadingImg: /img/loading.gif
```

#### 图片大图查看

修改主题配置文件`_config.butterfly.yml`

```yaml
# Lightbox (圖片大圖查看模式)
# --------------------------------------
# You can only choose one, or neither (只能選擇一個 或者 兩個都不選)

# medium-zoom
# https://github.com/francoischalifour/medium-zoom
medium_zoom: false
 
# fancybox
# http://fancyapps.com/fancybox/3/
fancybox: true
```



### 文章设置

#### 代码块设置

1. 代码高亮设置

   `butterfly`支持6中代码高亮样式：`dark,pale night,light,ocean,mac,mac light`

   修改**主题配置文件**

   ```yaml
   highlight_theme: light
   ```

2. 代码复制

   修改**主题配置文件**

   ```yaml
   highlight_copy: true
   ```

3. 代码框展开/关闭

   在默认情况下，代码框自动展开，可设置是否所有代码框都关闭状态，点击>可展开代码。

   - true 全部代码框不展开，需点击>打开
   - false 代码框展开，有>点击按钮
   - none 不显示>按钮

   修改**主题配置文件**

   ```yaml
   highlight_shrink: true #代码框不展开，需点击 '>' 打开
   ```

4. 代码换行

   在默认情况下，Hexo 在编译的时候不会实现代码自动换行。如果你不希望在代码块的区域里有横向滚动条的话，那么你可以考虑开启这个功能。

   修改**主题配置文件**

   ```yaml
   code_word_wrap: true
   ```

5. 代码高度

   可配置代码高度限制，超出的部分会隐藏，并显示展开按钮。

   ```yaml
   highlight_height_limit: 200 # unit: px
   ```

   **注意：**

   - 单位是 px，直接添加数字，如 200
   - 实际限制高度为` highlight_height_limit + 30 px` ，多增加` 30px` 限制，目的是避免代码高度只超出`highlight_height_limit` 一点时，出现展开按钮，展开没内容。
   - 不适用于隐藏后的代码块（ css 设置 display: none）

#### 主页文章节选

在butterfly里，有四种可供选择：

1. description： 只显示description
2. both： 优先选择description，如果没有配置description，则显示自动节选的内容
3. auto_excerpt：只显示自动节选
4. false： 不显示文章内容

修改**主题配置文件**

```yaml
index_post_content:
  method: 2
  length: 500 # if you set method to 2 or 3, the length need to config
```

#### 文章置顶

1. 可以直接在文章的`front-matter`区域里添加`sticky: 1`属性来把这篇文章置顶。数值越大，置顶的优先级越大。

   ```shell
   $ npm hexo-generator-index-pin-top
   ```

   

2. 在文章的 front-matter 区域里添加 top: true 属性来把这篇文章置顶

   ```shell
   $ npm install hexo-generator-index-pin-top --save
   ```

   

#### 文章单独设置版权

从3.0.0开始，支持对单独文章设置版权信息，可以在文章Front-matter单独设置

```markdown
copyright_author: xxxx
copyright_author_href: https://xxxxxx.com
copyright_url: https://xxxxxx.com
copyright_info: 此文章版权归xxxxx所有，如有转载，请注明来自原作者
```

#### 文章打赏功能

修改`主题配置文件`

```yaml
reward:
  enable: true
  QR_code:
    - img: /img/wechat.jpg
      link:
      text: 微信
    - img: /img/alipay.jpg
      link:
      text: 支付宝
```

#### 文章分页设置

可设置分页的逻辑，也可以关闭分页显示

```yaml
# post_pagination (分页)
# value: 1 || 2 || false
# 1: The 'next post' will link to old post
# 2: The 'next post' will link to new post
# false: disable pagination
post_pagination: false
```

#### 复制添加版权信息

```yaml
# copy settings
# copyright: Add the copyright information after copied content (复制的内容后面加上版权信息)
copy:
  enable: true
  copyright:
    enable: true
    limit_count: 50
```

### 留言板

#### 修改主题配置文件

```yaml
comments:
  # Up to two comments system, the first will be shown as default
  # Choose: Disqus/Disqusjs/Livere/Gitalk/Valine/Waline/Utterances/Facebook Comments/Twikoo/Giscus/Remark42/Artalk
  use: 
    - Valine # Valine,Disqus
  text: true # Display the comment name next to the button
  # lazyload: The comment system will be load when comment element enters the browser's viewport.
  # If you set it to true, the comment count will be invalid
  lazyload: false
  count: true # Display comment count in post's top_img
  card_post_count: false # Display comment count in Home Page
```

#### 注册valine

登录网站https://www.leancloud.cn/，注册并生成id和key

#### 修改valine

```yaml
# valine 
# 注册 https://www.leancloud.cn/
# https://valine.js.org
valine:
  appId: # leancloud application app id
  appKey: # leancloud application app key
  avatar: monsterid # gravatar style https://valine.js.org/#/avatar
  serverURLs: https://qxdd0wpk.lc-cn-n1-shared.com # leancloud REST API Server URL ，显示最新评论用
  bg: # valine background
  visitor: false
  option: 欢迎留言
```

#### 显示最新评

```yaml
# Aside widget - Newest Comments
newest_comments:
  enable: true
  sort_order: # Don't modify the setting unless you know how it works
  limit: 6
  storage: 10 # unit: mins, save data to localStorage
  avatar: true
```



### 本地搜索

#### 安装插件

```shell
npm install hexo-generator-search --save
```

#### 修改主题配置文件

```yaml
# Local search
local_search:
  enable: true
  preload: false
  CDN:
```



### 音乐播放

#### 安装插件

```shell
npm install --save hexo-tag-aplayer
nmp install aplayer
```

#### 修改站点配置文件

```yaml
# aplayer 
aplayer:
  meting: true
  asset_inject: false
```

#### 修改主题配置文

```yaml
# Inject the css and script (aplayer/meting)
aplayerInject:
  enable: true
  per_page: true
```

#### 普通界面播放器设置

以本博客为例，在博客音乐界面`\source\music\index.md`文件中添加：

```js
---
title: 音乐 
date: 2022-11-10 13:23:22
top_img: /img/music_img.jpg
type: "music"
comments: false
aplayer: true

---

{% meting "7751121816" "netease" "playlist" "autoplay" "mutex:false" "listmaxheight:500px" "preload:none" "theme:#ad7a86" "loop:all"%}
```

server:  `netease`（网易云音乐），`tencent`（QQ音乐），`kugou`（酷狗音乐），`xiami`（虾米音乐），`baidu`（百度音乐）。建议网易云

ID获取：打开网易云音乐，选择喜欢的歌单，在网页版打开，获取歌单list，填入即可。使用的时候将上边的ID号换为自己喜欢的歌单即可。

#### 全局吸底Aplayer模式

##### 修改主题配置文件

```yaml
#插入Aplayer html
# Inject
# Insert the code to head (before '</head>' tag) and the bottom (before '</body>' tag)
# 插入代码到头部 </head> 之前 和 底部 </body> 之前
inject:
  head:
  bottom:
      - <div class="aplayer no-destroy" data-id="7751121816" data-server="netease" data-type="playlist" data-fixed="true" data-autoplay="true" data-order="random" data-lrctype="1"> </div> # data-lrctype="1" 不显示歌词
   
pjax: # 切换页面，音乐不会中断
  enable: true
  exclude:
```

##### 关于`Aplayer html`

```html
<!--建议使用网易云，新建歌单，注意不要包含VIP音乐，否则无法解析-->
<div class="aplayer no-destroy" 
     data-id="7751121816" <!--必须字段，网易云网页播放地址最后ID-->
     data-server="netease" 
     data-type="playlist" 
     data-fixed="true" 
     data-autoplay="true">
</div>
<!-- 配置全局吸底，data-fixed 和 data-mini 也必须配置，配置为 true -->
```



### 图库

#### Gallery相册图库

写法：

```html
<div class="gallery-group-main">
{% galleryGroup name description link img-url %}
{% galleryGroup name description link img-url %}
{% galleryGroup name description link img-url %}
</div>
```

- name：图库名字
- description：图库描述
- link：连接到对应相册的地址
- img-url：图库封面的地址

在`photos/index.md` 文档中添加(注意是文本格式，不是markdown的html)

```html
<div class="gallery-group-main">
{% galleryGroup '壁纸' '收藏的一些壁纸' '/photos/wallpaper' https://s2.loli.net/2022/11/17/W8eGPEQT2tiBkMu.jpg %}
{% galleryGroup '动漫' '喜欢的动漫' '/photos/cartoon' https://s2.loli.net/2022/11/17/bmLOYuS9Pv7UKh6.jpg %}
</div>

```

在上面代码中：

```
name:壁纸
description：收藏的一些壁纸
link：/photos/wallpaper ，存放图片的子页面
img-url：https://s2.loli.net/2022/11/17/W8eGPEQT2tiBkMu.jpg  ,我的图床图库图片

```

#### Gallery相册

写法：

```markdown
{% gallery %}
markdown 图片格式
{% endgallery %}

```

新建子页面：

```shell
$ hexo n page cartoon
$ mv -f cartoon ./photos # 我将所有图库子页面都放到了photos文件夹下

```

在子页面`cartoon/index.md`中添加：

```markdown
---
title: 卡哇伊通
date: 2022-11-17 17:03:06
top_img: /img/photo_img.jpg
comments: false

---
{% gallery %}
![ct02.jpg](https://s2.loli.net/2022/11/17/meLbhBivr3Yc1og.jpg)
![ct07.jpg](https://s2.loli.net/2022/11/17/aNWQY748KCIzRgA.jpg)
![ct05.jpg](https://s2.loli.net/2022/11/17/VrqCWUtz5BSP8Og.jpg)
![ct03.jpg](https://s2.loli.net/2022/11/17/Xl5uj4icyZ2bnkt.jpg)
![ct10.jpg](https://s2.loli.net/2022/11/17/bmLOYuS9Pv7UKh6.jpg)
![ct01.jpg](https://s2.loli.net/2022/11/17/KzxTyB9ZwRh2Itg.jpg)
![ct08.jpg](https://s2.loli.net/2022/11/17/NGvuYR13ZAVKXJs.jpg)
![ct04.jpg](https://s2.loli.net/2022/11/17/MR2yeGEPpQm8jha.jpg)
![ct09.jpg](https://s2.loli.net/2022/11/17/xOYFKrQeBvdfVMg.jpg)
![ct06.jpg](https://s2.loli.net/2022/11/17/7DhkBnVpzIomJOU.jpg)
{% endgallery %}

```



### 音乐

```markdown
---
title: 音乐 
date: 2022-11-10 13:23:22
top_img: /img/music_img.jpg
type: "music"
comments: false
aplayer: true

---

{% meting "7751121816" "netease" "playlist" "autoplay" "mutex:false" "listmaxheight:500px" "preload:none" "theme:#ad7a86" "loop:all"%}

```

[参见8.4 普通界面音乐播放器设置]()

### 影视

1. 安装豆瓣电影插件

   ```shell
   $ npm install hexo-butterfly-douban --save
   # 更新
   $ npm install hexo-butterfly-douban --update --save
   
   ```

2. 修改站点配置文件

   ```yaml
    douban:
     user: 264594053
     builtin: true
     book:
       title: 'This is my book title'
       quote: 'This is my book quote'
       meta: true
       comments: true
       top_img: https://cccccc.png
       aside: true
       path: books
       limit:
     movie:
       title: 'This is my movie title'
       quote: 'This is my movie quote'
       meta: true
       comments: true
       top_img: https://cccccc.png
       aside: true
       path: movies
       limit:
     game:
       title: 'This is my game title'
       quote: 'This is my game quote'
       meta: true
       comments: true
       top_img: https://cccccc.png
       aside: true
       path: games
       limit:
     timeout: 10000 
   
   ```

   

### 主题美化

#### 全局背景渐变

1. 在主题文件夹`source\css` 文件夹立新增一个`css`文件

2. 添加如下代码

   ```css
   /*页面背景自定义*/
   #web_bg {
       background: -webkit-linear-gradient(
         0deg,
         rgba(247, 149, 51, 0.1) 0,
         rgba(243, 112, 85, 0.1) 15%,
         rgba(239, 78, 123, 0.1) 30%,
         rgba(161, 102, 171, 0.1) 44%,
         rgba(80, 115, 184, 0.1) 58%,
         rgba(16, 152, 173, 0.1) 72%,
         rgba(7, 179, 155, 0.1) 86%,
         rgba(109, 186, 130, 0.1) 100%
       );
       background: -moz-linear-gradient(
         0deg,
         rgba(247, 149, 51, 0.1) 0,
         rgba(243, 112, 85, 0.1) 15%,
         rgba(239, 78, 123, 0.1) 30%,
         rgba(161, 102, 171, 0.1) 44%,
         rgba(80, 115, 184, 0.1) 58%,
         rgba(16, 152, 173, 0.1) 72%,
         rgba(7, 179, 155, 0.1) 86%,
         rgba(109, 186, 130, 0.1) 100%
       );
       background: -o-linear-gradient(
         0deg,
         rgba(247, 149, 51, 0.1) 0,
         rgba(243, 112, 85, 0.1) 15%,
         rgba(239, 78, 123, 0.1) 30%,
         rgba(161, 102, 171, 0.1) 44%,
         rgba(80, 115, 184, 0.1) 58%,
         rgba(16, 152, 173, 0.1) 72%,
         rgba(7, 179, 155, 0.1) 86%,
         rgba(109, 186, 130, 0.1) 100%
       );
       background: -ms-linear-gradient(
         0deg,
         rgba(247, 149, 51, 0.1) 0,
         rgba(243, 112, 85, 0.1) 15%,
         rgba(239, 78, 123, 0.1) 30%,
         rgba(161, 102, 171, 0.1) 44%,
         rgba(80, 115, 184, 0.1) 58%,
         rgba(16, 152, 173, 0.1) 72%,
         rgba(7, 179, 155, 0.1) 86%,
         rgba(109, 186, 130, 0.1) 100%
       );
       background: linear-gradient(
         90deg,
         rgba(247, 149, 51, 0.1) 0,
         rgba(243, 112, 85, 0.1) 15%,
         rgba(239, 78, 123, 0.1) 30%,
         rgba(161, 102, 171, 0.1) 44%,
         rgba(80, 115, 184, 0.1) 58%,
         rgba(16, 152, 173, 0.1) 72%,
         rgba(7, 179, 155, 0.1) 86%,
         rgba(109, 186, 130, 0.1) 100%
       );
     }
   
   ```

   

3. 在主题文件`inject`配置项，引用该`css`文件

   ```
   
   ```

#### 页脚与主题图片保持一致

```yaml
# Footer Background
footer_bg: true

```

#### 背景特效

1. 背景动态线条

   在主题配置文件中设置

   ```yaml
   # canvas_nest
   # https://github.com/hustcc/canvas-nest.js
   canvas_nest:
     enable: true
     color: '186,85,211' #color of lines, default: '0,0,0'; RGB values: (R,G,B).(note: use ',' to separate.)
     opacity: 0.7 # the opacity of line (0~1), default: 0.5.
     zIndex: -1 # z-index property of the background, default: -1.
     count: 99 # the number of lines, default: 99.
     mobile: true
   
   ```

2. 鼠标点击爱心

   ```yaml
   # Mouse click effects: Heart symbol (鼠標點擊效果: 愛心)
   click_heart:
     enable: true
     mobile: true
   
   ```

3. 打字效果

   ```yaml
   # Typewriter Effect (打字效果)
   # https://github.com/disjukr/activate-power-mode
   activate_power_mode:
     enable: true
     colorful: true # open particle animation (冒光特效)
     shake: true #  open shake (抖动特效)
     mobile: false
   
   ```

#### 留言板信封

1. 安装插件

   ```shell
   npm install hexo-butterfly-envelope --save
   
   ```

2. 站点配置文件添加：

   ```yaml
   # envelope_comment
   # see https://akilar.top/posts/e2d3c450/
   envelope_comment:
     enable: true #控制开关
     custom_pic:      
       cover: https://npm.elemecdn.com/hexo-butterfly-envelope/lib/violet.jpg #信笺头部图片
       line: https://npm.elemecdn.com/hexo-butterfly-envelope/lib/line.png #信笺底部图片
       beforeimg: https://npm.elemecdn.com/hexo-butterfly-envelope/lib/before.png # 信封前半部分
       afterimg: https://npm.elemecdn.com/hexo-butterfly-envelope/lib/after.png # 信封后半部分
     message: #信笺正文，多行文本，写法如下
       - 有什么想问的？
       - 有什么想说的？
       - 有什么想吐槽的？
       - 哪怕是有什么想吃的，都可以告诉我哦~
     bottom: 自动书记人偶竭诚为您服务！ #仅支持单行文本
     height: #1050px，信封划出的高度
     path: /comment #【可选】comments 的路径名称。默认为 comments，生成的页面为 comments/index.html
     front_matter: #【可选】comments页面的 front_matter 配置
       title: 留言板
       top_img: /img/comment_img.jpg
       comments: true
   
   ```

#### 添加卡通人物(看板娘)

1. 安装插件

   ```shell
   npm install --save live2d-widget-model-shizuku
   
   ```

2. 修改站点配置文件

   ```yaml
   live2d:
     enable: true
     scriptFrom: local # 默认
     tagMode: false # 标签模式, 是否仅替换 live2d tag标签而非插入到所有页面中
     debug: false # 调试, 是否在控制台输出日志
     model:
       use: live2d-widget-model-shizuku  #模型选择
     display:
       position: right  #模型位置
       width: 150       #模型宽度
       height: 300      #模型高度
       hOffset: 20
       vOffset: -20
     mobile:
       show: false      #是否在手机端显示
   
   ```

#### 公告下方添加两个小人

在 `node_modules\hexo-theme-butterfly\layout\includes\widget\card_announcement.pug` 下添加如下代码：

```css
.xpand(style='height:200px;')
  canvas.illo(width='800' height='800' style='max-width: 200px; max-height: 200px; touch-action: none; width: 640px; height: 640px;')
script(src='https://fastly.jsdelivr.net/gh/xiaopengand/blogCdn@latest/xzxr/twopeople1.js')
script(src='https://fastly.jsdelivr.net/gh/xiaopengand/blogCdn@latest/xzxr/zdog.dist.js')
script#rendered-js(src='https://fastly.jsdelivr.net/gh/xiaopengand/blogCdn@latest/xzxr/twopeople.js')
style.
  .card-widget.card-announcement {
  margin: 0;
  align-items: center;
  justify-content: center;
  text-align: center;
  }
  canvas {
  display: block;
  margin: 0 auto;
  cursor: move;
  }

```

#### 首页字体

在主题`source\css`新建一个`css`文件`custom.css`, 添加如下代码

```css
@font-face {
    font-family:'arzhu';
    src:url('/font/三极行楷简体-粗.ttf');; /* 修改成你的字体 */
    font-display:swap
}
h1#site-title {
    font-family:arzhu!important
}
span#subtitle {
    font-family:arzhu!important
}
a#site-name {
    font-family:arzhu!important
}

```

在主题的配置文件里找到 `inject` 配置项，引用刚刚新建的 css 文件即可：

```yaml
# Inject
# Insert the code to head (before '</head>' tag) and the bottom (before '</body>' tag)
# 插入代码到头部 </head> 之前 和 底部 </body> 之前
inject:
  head:
      - <link rel="stylesheet" href="/css/custom.css" media="defer" onload="this.media='all'">
  bottom:

```

