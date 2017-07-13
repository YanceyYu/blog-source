---
title: 如何优雅的在博客中添加图片
date: 2017-07-13 11:59:58
categories: 搭建博客
tags: 图床神器
---
## 前言
不知道大家发博客的时候怎么处理图片，我写博客的时候为了方便自己看一般是先在`为知笔记`里写一份，然后再把.md文件粘贴到博客文件夹里。其实在为知笔记里写`Markdown`笔记很方便，截图可以直接粘贴，本地图片可以直接上传，网络图片直接粘贴链接就可以了。

可是在博客里使用图片就很不方便了，因为我们大部分使用的是本地图片或者是截图，我得先把图片按一定规则重新命名放在博客文件夹下，然后再在Markdown文件中把图片的绝对路径写入才会引入图片。这样不仅麻烦，笔记、博客两端的图片还不能通用，每次生成静态页面和提交GitHub的时候由于图片过多还会变得很慢。

可是如何优雅的在博客中添加图片呢？下面给大家介绍一下**图床神器**。

## 图床神器
什么是图床神器呢，我们看一下`Mac OS`和`Windows`下两款图床神器是怎么介绍自己的。

**iPic** (Mac OS)
有了图床神器 iPic，不论屏幕截图、还是复制图片，都可以自动上传、保存 Markdown 格式的链接，直接粘贴插入，够懒人吧？

使用 Hexo | Heroku 或 WordPress 写博客、在公众号发文章、在知乎讨论、在豆瓣灌水、在论坛发帖、跨境做外贸电商 …

iPic 带给你从未有过的插图体验。

**MPic** (Windows)
一款支持多种上传方式且自动生成MarkDown链接的图床工具。

大家看了有没有心动呢，下面我介绍一下`Windows`下的`MPic`的使用方法，`Mac OS`的`iPic`可以参考 **[iPic 使用教程](http://toolinbox.net/iPic/)**。
<!-- more -->
## 如何使用图床神器MPic
### 注册七牛云账号
由于MPic是基于七牛云的，我们通过MPic上传的图片都是上传到七牛云存储上。所以我们首先需要去[七牛云官网](https://www.qiniu.com/)注册账号然后登录，这里注册后需要实名认证，可以授权支付宝认证，也可以人工审核认证。

### 新建空间
登录后选择左侧`对象存储`。
![mark](http://oszefrx4t.bkt.clouddn.com/blog/170713/4IiC4k8KgC.png)

点击左侧`新建存储空间`。
![mark](http://oszefrx4t.bkt.clouddn.com/blog/170713/5CeBdg206L.png)

按照要求填写，`访问控制`我们选择`公开工具 `，这样通过外链可以直接访问，点击`确认创建`，记住`存储空间名称`，稍后配置MPic会用到。
![mark](http://oszefrx4t.bkt.clouddn.com/blog/170713/1lGbLl3l2g.png)

### 找到外链域名和密钥
存储空间创建好后点击`内容管理`会看到`外链默认域名`，稍后配置MPic会用到。
![mark](http://oszefrx4t.bkt.clouddn.com/blog/170713/3B176ka678.png)

点击右上角`个人面板`选择`密钥管理`。
![mark](http://oszefrx4t.bkt.clouddn.com/blog/170713/L7gG3me3f9.png)

打开后我们可以看到`AK(AccessKey)`和`SK(SecretKey)`，稍后配置MPic会用到。
![mark](http://oszefrx4t.bkt.clouddn.com/blog/170713/6361gAm69c.png)

## 下载安装配置MPic
[MPic官网](http://mpic.lzhaofu.cn/)下载安装包。安装包是一个压缩包，解压后打开`MPic.exe`，可以看到MPic的主界面。
![mark](http://oszefrx4t.bkt.clouddn.com/blog/170713/3HFG3gbhJI.png)

点击左上角`设置账号`，这里的七牛云配置为上一步所说的一些信息，填入即可，图片瘦身可选，点击保存后我们就可以用了。
![mark](http://oszefrx4t.bkt.clouddn.com/blog/170713/eDCGjCK2fk.png)

直接拖拽图片到主界面就可以上传图片了，图片直接上传到七牛云，点击复制直接复制为Markdown格式。
![mark](http://oszefrx4t.bkt.clouddn.com/blog/170713/KA8kcfeL4g.png)

默认设置是MarkDown格式、复制图片自动上传、截图自动上传，可以在Windows右下角图标上点击右键进行设置。