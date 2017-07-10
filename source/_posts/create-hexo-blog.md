---
title: 基于Hexo搭建GitHub博客
date: 2017-07-10 17:11:23
categories: GitHub
tags: GitHub,Blog
---
## 关于为何自己搭建博客
为什么要自己建站搭建博客，在网上看到说喜欢写Blog的人，会经历三个阶段。
>第一阶段，刚接触Blog，觉得很新鲜，试着选择一个免费空间来写。
第二阶段，发现免费空间限制太多，就自己购买域名和空间，搭建独立博客。
第三阶段，觉得独立博客的管理太麻烦，最好在保留控制权的前提下，让别人来管，自己只负责写文章。

还有个主要的原因，独立建站不会被和谐，自己不光可以分享一些技术贴还可以发一些所思所想。

如果偏向技术，博客园和CSDN也是个比较不错的选择，不过也需要审核，而且总感觉不够GEEK。

偏向问答、社交可以选择知乎、微博，可是审核特别恶心，动不动就会被和谐。

微博「随时随地发现新鲜事」，这世界 TM 还只能发生你审核过的新鲜事了？

知乎「与世界分享你的知识、经验和见解」，我 TM 还只能分享你审核过的世界了？

## 关于如何搭建博客
### 博客托管GitHub Pages
如何搭建微博，大家可能最先想到的是自己购买云服务器和域名自己搭建。可是自己管理又太麻烦，而且云服务器也不便宜。
于是这里我们使用[GitHub Pages](https://pages.github.com/)来搭建自己的博客。为什么使用GitHub Pages呢？
1. 免费、无限流量、安全，GitHub Pages有免费、无限流量的存储空间，而且作为用户超过900万的项目托管平台，安全可靠。
2. 方便管理，我们把博客交给GitHub管理，享受git的版本管理功能，不用担心文章遗失，不需要自己维护服务器，只需要专注于写文章就好。
3. 可以学习使用GitHub，享受GItHub带来的便利，还可以在GitHub上结识技术牛人。
<!-- more -->
### 静态博客框架选择Hexo
直接写的HTML静态博客维护起来相当麻烦，不支持Markdown，写一篇文章相当于写一个HTML页面，而且往往还需要改很多页面的链接；非专业前端人员页面设计不够友好，还会浪费很多时间在页面设计上。

所以这里我们可以选择一些比较流行的静态博客框架。比如：Jekyll、Hexo、Wordpress、Simple，Octopress，Pelican等等。当初在[Jekyll](http://jekyll.com.cn/)和[Hexo](https://hexo.io/)中纠结，最后我选择了Hexo来搭建自己的博客，和Jekyll相比，选择Hexo主要原因是：
1. Jekyll基于Ruby实现，需要安装Ruby，安装相对困难，而 Hexo基于Node.js实现，安装Node.js开发环境比较简单。
2. 便捷性，同样是快速启动，也同样都是几个命令就可以预览效果，但是Hexo比Jekyll方便，效果也好的多，而且生成静态站点的速度上Hexo也比Jekyll快的多。

## Hexo搭建博客流程
### 注册GitHub账号
这里就不多说了，大家可以进入[GitHub官网](https://github.com/)进行注册。
![](/images/create-hexo-blog/gtihub-sign-up.jpg)

### 创建仓库
登录之后，点击右上角头像旁边的“+”`New repository`创建新仓库。
![](/images/create-hexo-blog/new-repository.jpg)
在创建页面填写仓库信息，`Repository name`为仓库名，命名规则为`github昵称.github.io`，如果使用其他名字需要创建一个没有父节点的分支`gh-pages`。因为github规定，只有以`github昵称.github.io`命名的仓库和该分支中的页面，才会生成网页文件。然后点击`Create repository`按钮。
![](/images/create-hexo-blog/create-a-new-repository.jpg)

### 安装Git环境
为了使用GitHub的，需要安装Git环境，进入[Git官网](https://git-scm.com/downloads)根据系统下载对应版本安装即可。
![](/images/create-hexo-blog/git-downloads.jpg)

### 安装Node.js环境
Hexo基于Node.js实现，所以我们这里需要安装Node.js环境，进入[Node.js官网](https://nodejs.org)下载安装包进行安装即可。
![](/images/create-hexo-blog/node-js.jpg)

### 安装Hexo
有能力的同学可以进入[Hexo官网](https://hexo.io/)查看[Hexo官方文档](https://hexo.io/docs/)自行安装。
![](/images/create-hexo-blog/hexo.jpg)
下面我简单说下安装步骤：
#### 下载安装Hexo
在终端输入输入：
``` linux
$ npm install hexo-cli -g
```

安装好之后输入：
``` linux
$ hexo
```
输出如下说明安装成功。
![](/images/create-hexo-blog/hexo-success.jpg)

#### 初始化博客
建立一个博客文件夹，并初始化博客， folder为文件夹的名称。
``` linux
$ hexo init folder
```

进入博客文件夹。
``` linux
$ cd folder
```

node.js的命令，根据博客既定的dependencies配置安装所有的依赖包。
``` linux
$ npm install
```

初始化博客后，我们可以看到博客文件夹下的目录结构如下：
![](/images/create-hexo-blog/directory-structure.jpg)

### Hexo配置
博客文件夹下的`_config.yml`为站点配置文件。
#### 修改网站相关信息
``` yml
# Site
title: Yancey Blog
subtitle: the blog of yancey start from zero
description: code like poem, write my own life
author: Yancey Yu
language: zh-Hans
timezone: Asia/Shanghai
```

>**注意**：每一项的填写，配置文件中每项配置其":"后面必须有一个空格。

#### 配置个人域名
``` yml
url: http://yanceyyu.top
```

#### 配置部署信息
``` yml
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/YanceyYu/yanceyyu.github.io.git
  branch: master
```
>type：部署类型，repo：仓库地址，branch：分支。

### 发表第一篇文章
新建一篇文章，在终端博客文件夹下输入如下：
``` linux
$ hexo new "first-article"
```

`first-article`为文章标题，我们可以在博客文件夹`source->_posts`下找到我们新建的Markdown文件，我们也可以直接在该文件夹下创建`.md`文件。

![](/images/create-hexo-blog/posts.jpg)

用Markdown编辑器（这里我使用的是MarkdownPad）打开刚才我们创建的文件`first-article.md`,并在末尾加上一段话。
![](/images/create-hexo-blog/first-article.jpg)

保存后，我们在博客文件夹进行本地发布。
``` linux
$ hexo server
```

打开浏览器输入一下网址进行访问。
```
http://localhost:4000/
```

如果发现网址访问不了，可能是端口被占用了。使用如下语句查看端口是否被占用。
``` linux
$ netstat -an|findstr 4000
```

如果被占用可以使用如下语句进行指定端口进行本地发布。
``` linux
$ hexo server -p 4001
```

我们可以在浏览器端看到我们刚刚搭建好的博客。

![](/images/create-hexo-blog/blog-index.jpg)

下面我们把创建好的博客部署到GitHub。输入如下命令：
```
$ hexo generate
$ hexo deploy
```
>hexo generate：生成静态站点文件，hexo deploy：部署到远程站点。

部署成功后我们可以通过访问`https://yanceyyu.github.io`来查看自己的博客。
>yanceyyu.github.io为你之前创建的仓库名，yanceyyu为你自己GitHub昵称。

这样我们就建立好一个简单的博客了，接下来为大家讲解怎么更改域名和更换主题。

