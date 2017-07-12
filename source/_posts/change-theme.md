---
title: 更换配置Hexo主题并集成第三方服务
date: 2017-07-11 22:27:53
categories: 搭建博客
tags: [Hexo,NexT]
---
## Hexo主题选择
我们之前用Hexo搭建的博客，默认的主题是`landscape`,可以在博客文件夹`themes`目录下找到该主题文件夹。

默认主题相对来说比较丑，而且功能也比较少，这里我们可以选择自己喜爱的主题进行更换。作为博客的主题，大道至简，选择一款简洁的主题很重要，复杂一点的反而觉得臃肿。下面推荐几个GitHub上Star数量比较靠前的Hexo主题。
*   [iissnan/hexo-theme-next](https://github.com/iissnan/hexo-theme-next)
*   [litten/hexo-theme-yilia](https://github.com/litten/hexo-theme-yilia)
*   [TryGhost/Casper](https://github.com/TryGhost/Casper)
*   [wuchong/jacman](https://github.com/wuchong/jacman)
*   [A-limon/pacman](https://github.com/A-limon/pacman)
*   [daleanthony/uno](https://github.com/daleanthony/uno)
*   [orderedlist/modernist](https://github.com/orderedlist/modernist)
*   [AlxMedia/hueman](https://github.com/presscustomizr/hueman)
*   [kathyqian/crisp-ghost-theme](https://github.com/kathyqian/crisp-ghost-theme)
*   [xiangming/landscape-plus](https://github.com/xiangming/landscape-plus)

我选择的是第一个NexT主题，目前为止GitHub上Star数量已达8548，颇具人气。
特点：
* 页面简洁，功能完善
* 有比较完整的使用文档
* 第三方服务集成的比较好，像搜索、评论、分享、统计分析等都有集成

主题源码：[iissnan/hexo-theme-next](https://github.com/iissnan/hexo-theme-next)
主题效果：[IIssNan's Notes](http://notes.iissnan.com/)
主题使用文档：[theme-next](http://theme-next.iissnan.com/)
我这里参考了[EZLippi](http://www.ezlippi.com/)的博客的主题配置，大家也可以做下参考，[EZLippi NexT主题源码](https://github.com/EZLippi/hexo-theme)。
我的博客：[Yancey Blog](http://yanceyyu.top/)
我的博客源码：[blog-source](https://github.com/YanceyYu/blog-source)
<!-- more -->
## 下载主题
进入到Hexo博客目录执行以下语句把主题下载到`themes/next`目录下.
``` linux
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```

## 应用主题
把Hexo目录下`_config.yml`站点配置文件的`theme`字段的值更改为`next`，如下：
``` yml
theme: next
```

## 配置主题
进入Hexo文件夹`themes->next`目录下找到`_config.yml`**主题配置文件**并打开，以下所说的主题配置文件都是指这个，**站点配置文件**为Hexo目录下的`_config.yml`。

### 选择样式
NexT主题提供了三种样式,根据个人喜好进行选择，我这里选择的`Mist`
```
# Schemes
scheme: Mist
#scheme: Muse
#scheme: Pisces
```

### 添加标签tags页面
在Hexo目录下，新建一个页面，命名为tags。
``` linux
$ hexo new page tags
```

在`source->tags`下生成一个`index.md`，内容如下所示，如果要关闭tags页面的评论可以设置comments为false。
```
---
 title: 标签
 date: 2017-07-06 16:19:40
 type: "tags"
 comments: false
 ---
```

### 添加分类页面
在Hexo目录下，新建一个页面，命名为categories。
```
$ hexo new page categories
```

在`source->categories`下生成一个`index.md`，内容如下所示：
```
---
 title: 分类
 date: 2017-07-06 16:20:54
 type: "categories"
 comments: false
 ---
```

### 添加关于页面
在Hexo目录下，新建一个页面，命名为about。
```
$ hexo new page about
```
在`source->about`下生成一个`index.md`，内容如下所示，大家可以再下面填上自己的介绍。
```
---
 title: about
 date: 2017-07-06 18:05:56
 ---
```

### 添加404页面

新建一个404.html文件，放到`themes\next\source`目录下，也可以放到`source`目录下，内容你自己定。我这里用的是腾讯公益404页面，寻找丢失儿童，让大家一起关注此项公益事业！效果如下 [http://www.ixirong.com/404.html](http://www.ixirong.com/404.html)，内容如下：

```
<!DOCTYPE HTML>
<html>
<head>
  <meta http-equiv="content-type" content="text/html;charset=utf-8;"/>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="robots" content="all" />
  <meta name="robots" content="index,follow"/>
  <link rel="stylesheet" type="text/css" href="https://qzone.qq.com/gy/404/style/404style.css">
</head>
<body>
  <script type="text/plain" src="http://www.qq.com/404/search_children.js"
          charset="utf-8" homePageUrl="/"
          homePageName="回到我的主页">
  </script>
  <script src="https://qzone.qq.com/gy/404/data.js" charset="utf-8"></script>
  <script src="https://qzone.qq.com/gy/404/page.js" charset="utf-8"></script>
</body>
</html>
```

### 设置菜单
#### 设置菜单显示
根据需要选择显示的菜单,或者添加自定义菜单。
```
menu:
  home: / #主页
  categories: /categories #分类页
  archives: /archives #归档页
  tags: /tags #标签页
  about: /about #关于页面
  #commonweal: /404.html #公益404页面
```

#### 设置菜单显示内容
之前们在站点配置文件中设置的语言为`zh-Hans`,我们需要在Hexo文件夹`themes->next->languages`目录下找到`zh-Hans.yml`，里面显示的中文对应上一步的menu。
```
menu:
  home: 首页
  archives: 归档
  categories: 分类
  schedule: 日程
  tags: 标签
  about: 关于
  search: 搜索
  commonweal: 公益404
```
#### 设置菜单图标
对应的字段是 `menu_icons`。 此设定格式是 `item name: icon name`，其中 `item name` 与上一步所配置的菜单名字对应，`icon name` 是 Font Awesome 图标的名字。而 `enable` 可用于控制是否显示图标，你可以设置成 `false` 来去掉图标。
```
menu_icons:
  enable: true
  home: home
  about: user
  categories: th
  schedule: calendar
  tags: tags
  archives: archive
  sitemap: sitemap
  commonweal: heartbeat
```

### 设置 RSS
RSS是站点用来和其他站点之间共享内容的一种简易方式（也叫聚合内容），通常被用于新闻和其他按顺序排列的网站，例如Blog。

通过RSS阅读器，可以浏览RSS文件、订阅博客、订阅新闻，这些内容就会自动出现你的阅读器里，一旦有了更新，RSS阅读器就会自己通知你。

NexT 中 RSS 有三个设置选项，满足特定的使用场景。 更改 **主题配置文件**，设定 `rss` 字段的值：

`false`：禁用 RSS，不在页面上显示 RSS 连接。
```
rss: false
```

留空：使用 Hexo 生成的 Feed 链接， 需要先执行以下语句安装插件。
```
$ npm install hexo-generator-feed --save
```
然后在**主题配置文件**加入以下语句：
```
rss:
```

具体的链接地址：适用于已经烧制过 Feed 的情形。

### 其他配置
```
favicon: /favicon.ico #网站标题logo
keywords: "Yancey" #博客关键字
since: 2017 #站点建立时间
copyright: false #主题版权信息显示
font: #字体设置
social: #侧边栏个人站点链接
links_title: #侧边栏友情链接
avatar: #头像
```
**更多配置请参考[NexT主题配置](http://theme-next.iissnan.com/theme-settings.html)
**
## 第三方服务
### 评论系统
[DISQUS](www.disqus.com/)，第三方社会化评论系统最出名的要数DISQUS了，无奈现在国内已经被墙了。
[多说](http://duoshuo.com/)，国内版的DISQUS，已于2017年6月1日正式关停服务。
[网易云跟贴](https://gentie.163.com/)，官方公告云跟贴产品将于2017年8月1日停止服务。
找了很多第三方评论系统，大部分国外的都得翻墙，所以最后还是选择国内的[友言](http://www.uyan.cc/),论第三方评论的何去何从，不知道友言还能挺多久。

首先我们需要在[友言官网](http://www.uyan.cc/)注册并登录，然后获取代码。
主题已经集成很多第三方评论系统，我们只需要修改主题配置文件`_config.xml`加上刚刚获取的代码即可。
```
youyan_uid: 1251878
```

### 内容分享服务
内容分享我是用的**JiaThis**，只需要修改主题配置文件添加/修改字段 `jiathis`，值为 `true`即可。
```
# JiaThis 分享服务
jiathis: true
```

### 搜索服务
**Local Search**
添加百度/谷歌/本地 自定义站点内容搜索

1. 安装 `hexo-generator-searchdb`，在站点的根目录下执行以下命令：
```
$ npm install hexo-generator-searchdb --save
```

2. 编辑 **站点配置文件**，新增以下内容到任意位置：
```
# Local search
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

3. 编辑 **主题配置文件**，启用本地搜索功能：
```
# Local search
local_search:
   enable: true
```

### 数据统计功能
#### 不蒜子统计
编辑**主题配置文件**中的`busuanzi_count`的配置项。
当`enable: true`时，代表开启全局开关。若`site_uv`（访客数）、`site_pv`（访问量）、`page_pv`（文章访问量）的值均为`false`时，不蒜子仅作记录而不会在页面上显示，需要在页面显示哪项可以改为`true`。
>`page_pv`统计的文章访问量只会在文章页面显示，不会再主页文章上显示。
``` yml
# Show PV/UV of the website/page with busuanzi.
# Get more information on http://ibruce.info/2015/04/04/busuanzi/
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: <i class="fa fa-user"></i> 本站访客数
  site_uv_footer: 人次
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-eye"></i> 本站总访问量
  site_pv_footer: 次
  # custom pv span for one page only
  page_pv: false
  page_pv_header: <i class="fa fa-file-o"></i> 本文总阅读量
  page_pv_footer: 次
```

#### 阅读次数统计（LeanCloud)
[LeanCloud](https://leancloud.cn/)
进入[注册页面](https://leancloud.cn/login.html#/signup)注册。完成邮箱激活后，点击头像，进入`控制台`页面，点击`应用->创建新应用`。
![](/images/change-theme/leancloud-console.jpg)

创建完应用，点击应用，`创建 Class`名称为`Counter`。
![](/images/change-theme/leancloud-create-class1.jpg)
![](/images/change-theme/leancloud-create-class2.jpg)

点击`设置->应用Key`获取秘钥信息。
![](/images/change-theme/leancloud-set-key.jpg)

修改**主题配置文件**，添加/修改如下：
```
# add post views
leancloud_visitors:
  enable: true
  app_id: **你的app_id**
  app_key: **你的app_key**
```

>其中，app_id和app_key在你所创建的应用的`设置->应用Key`中的`APP ID`和`APP KEY`。

>阅读次数统计不仅会在文章页面显示，还会在主页文章上显示。

**Web安全性**
为了保证应用的统计计数功能仅应用于自己的博客系统，你可以在`应用->设置->安全中心`的`Web安全域名`中加入自己的博客域名，以保证数据的调用安全。

### 站点地图（sitemap）
#### 什么是sitemap
可方便网站管理员通知搜索引擎他们网站上有哪些可供抓取的网页，简单的说就是让百度和谷歌可以搜到我们的博客。

#### 博客中添加对sitemap的支持
在Hexo博客根目录，分别用下面两个命令来安装针对谷歌和百度的插件。
```
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save
```

在站点配置文件`_config.yml`中，添加如下内容。
``` yml
# sitemap
sitemap:
  path: sitemap.xml
baidusitemap:
  path: baidusitemap.xml
```

修改完后，输入 `hexo server`,在浏览器输入`http://localhost:4000/sitemap.xml` 就可以查看站点地图效果。

#### 让百度收录我们的博客
进入[百度站长工具](http://zhanzhang.baidu.com/dashboard/index)，点击添加站点
![](/images/change-theme/baidu-add-site.jpg)
按照步骤添加站点，第一步：输入网站
![](/images/change-theme/baidu-add-site1.jpg)

第二步：站点属性
![](/images/change-theme/baidu-add-site2.jpg)

第三步：验证网站
![](/images/change-theme/baidu-add-site3.jpg)

这里我选的`CNAME验证`,需要去你的域名解析网站添加一条记录，主机记录为上一步`CNAME验证`你的域名前的字符串。
![](/images/change-theme/baidu-add-cname.jpg)

>验证完成后，将会认为您是网站的拥有者。网站定期检查验证记录为保持验证通过的状态，请保留验证的文件、html标签或CNAME记录。

选择`网页抓取->链接提交`，这里推荐自动推送和sitemap。
![](/images/change-theme/baidu-webpage-crawling.jpg)

这里选择的自动`提交->sitemap`。
![](/images/change-theme/baidu-site.jpg)

添加完会在下方看到一条数据，处于等待状态。
![](/images/change-theme/baidu-site-status.jpg)

>对于新站，一般7天左右收录，这期间需要经常更新一下原创文章。如果说超过半个月没有收录，那么就要和百度反馈了。

#### 让谷歌收录我们的博客
进入[Google站长工具](https://www.google.com/webmasters/tools)，登录Google账号后点击`添加属性`，填入自己的博客域名。
![](/images/change-theme/google-add-site.jpg)

然后验证网站的所有权，这里有很多种方法，我选择的是`备用方法->域名提供商->添加 CNAME 记录`，和之前百度站点验证的方法一样，需要向解析域名网站添加一条记录。
![](/images/change-theme/google-verify-site.jpg)

最后选择菜单栏`抓取->站点地图`，在右侧添加自己博客的`sitemap.xml`就OK了。
![](/images/change-theme/google-add-sitemap.jpg)验证完成后

>谷歌比百度容易收录，对于新站，一般2-4天就可以完全收录。

**更多第三方服务请参考[NexT第三方服务集成](http://theme-next.iissnan.com/third-party-services.html)**
