---
title: GitHub Pages绑定自己的域名
date: 2017-07-10 23:16:11
categories: 搭建博客
tags: 
---
我们刚刚搭建的博客通过访问`https://yanceyyu.github.io`可以正常访问，由于是GitHub托管，所以链接包含统一的github.io，这里我们可以绑定自己的域名，下面介绍下GitHub Pages如何绑定自己的域名。
## 申请域名
可以申请域名的网站很多，这里我是通过阿里云旗下的[万网](https://wanwang.aliyun.com/)申请的。我申请的域名是yanceyyu.top。

## 域名解析
域名解析是把域名指向网站空间IP，让人们通过注册的域名可以方便的访问到网站的一种服务。这里就相当于把`https://yanceyyu.github.io`映射到我们刚刚申请的域名`http://yanceyyu.top`。域名解析也可以通过很多网站，我使用的是免费的[DNSPOD](https://www.dnspod.cn/)。
首先访问[DNSPOD官网](https://www.dnspod.cn/)进行注册，然后登录。点击左侧菜单栏的`域名解析`，然后点击右侧的`添加域名`，在空白处添加刚才申请的域名。
![](/images/addon-domain/dnspod-resolve.jpg)
<!-- more -->
然后点击`添加记录`，这里我们添加两条记录，
主机记录分别为`@`何`www`，这样通过`http://yanceyyu.top`和`http://www.yanceyyu.top`都可以访问，
记录类型都为`CNAME`域名指定，也可以选择`A`IP指定，
记录值都为`yanceyyu.github.io.`，注意链接后面有个“.”，其他为默认即可。
![](/images/addon-domain/dnspod-add-record.jpg)

## 修改域名DNS
然后我们访问域名网站，找到刚才申请的域名，我这里用的是[阿里云的域名控制台](https://netcn.console.aliyun.com/core/domain/list)，点击管理。
![](/images/addon-domain/aliyun-domain-list.jpg)

点击`DNS修改`，把DNS服务器修改为域名解析的服务器，我这里是改为DNSPOD的`f1g1ns1.dnspod.net`。
![](/images/addon-domain/aliyun-dns.jpg)

## 博客绑定域名
在自己博客文件夹的根目录添加一个文件命名为`CNAME`，里面的内容为域名，不要http以及www等前缀，只需写入域名本身,例如：
```
yanceyyu.top
```
>如果是直接在博客文件夹的根目录添加文件`CNAME`的话，会遇到一个问题就是在执行`hexo generate`、`hexo deploy`之后hexo会把根目录下的CNAME文件删除。

所以要把`CNAME`文件添加到`/source`目录下，这样执行`hexo generate`、`hexo deploy`之后hexo会自动把`CNAME`推送到远程`master`分支的根目录下。

最后通过在博客文件夹下执行以下语句：
```
$ hexo generate
$ hexo deploy
```
等几分钟，浏览器输入自己域名就可以访问博客了。