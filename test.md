---
title: 我的第一篇博客
categories: [日常]
tags: [日常]
group: archive
icon: globe
layout: post
keywords: Start
description: 我的第一篇博客
---

使用git在线写hexo博客的方法

传统的博客要么是在cnblog、csdn或jianshu这样的平台上，注册账号撰写、子域名访问，要么是自己花钱买虚拟服务器（vps）搭建wordpress或typecho动态博客。第一种虽然免费，但无法自定义域名，第二种可DIY程度高，单要花钱，而且要一定的技术能力。

本文介绍的搭建博客的方法也不是我自创的，网上许多个人技术博客正式这样的：使用github的pages功能，把写好的博客文章免费在这类代码托管平台，如 gitcafe.com, git.oschina.net, git.coding.net, git.ustclug.org ，并可以自定义域名访问。可实现的工具有jekyell/octpress和hexo，它们都是先写好固定格式的文章（一般是markdown），然后渲染成可浏览模式。

当然没有十全十美的办法，这种在线方式写内容切记要经常“提交到master”，不要轻易后退浏览器或者关掉，否则不要来骂我，大不了直接用markdown编辑器本地写，随时保存了——我自己也倾向于，*先在本地md编写*，*再push到oschina git仓库*，*最后deploy到gitcafe*，即解决了同步问题，也解决了忘记提交保存丢失的问题。

# 1. 准备工作

- 注册gitcafe,oschina账号
最终访问的文章内容就是放在Github或gitcafe上的，它们本来都只是公共免费的代码托管平台，利用它们提供的Pages服务打的擦边球，初衷是做项目的演示/介绍页面。Github无疑是最火的，但是国外的访问速度略慢（其实CDN服务已经做到延迟可以接受的程度了），另一个好处是IP是国外的，不要备案。

gitcafe.com或者coding.net做的也是同样的服务，但国内访问速度很快，正常30-40ms 。至于备案，据说gitcafe被某机构找去谈话了，然后它就把pages服务器干脆放到香港，所以也免了，看[这里](https://www.v2ex.com/t/154448)。

## 设置gitcafe博客仓库
1. 添加ssh公钥
https://gitcafe.com/GitCafe/Help/wiki/Pages-%E7%9B%B8%E5%85%B3%E5%B8%AE%E5%8A%A9#wiki
2. 创建与用户名相同的项目
Gitcafe会自动把这样的项目识别成一个Pages项目
图


3. 


- 速度快，易编辑（带图片）
- 个人域名

- ssh密钥

- markdown编辑器（markdown pad 2 或 Mou）
- 
# 2. 使用hexo免费部署到gitcafe


## 2.1 安装hexo

1. git
在windows上安装，需要先下载git，[下载地址](https://git-scm.com/download/win)。Mac下默认已经有git。

2. node.js
安装nodejs，直接下载[安装包](https://nodejs.org/en/)，选择windows或者Mac平台的LTS版。

3. 安装hexo
```
$ npm install -g hexo-cli 
$ hexo init  seanlook
$ cd seanlook
$ npm install
```
第一步，安装全局模块，即hexo命令。
第二步，在当前自己目录（seanlook）里面，下载博客源码，安装nodejs依赖模块，默认是hexo的最新版本，在node_modules可看到。如果你想指定安装hexo版本，可加入`--no-install`参数，然后修改package.json，再执行第三步。
第三步，安装package.json里面指定的依赖包，一般init都已安装好。

hexo-cli是博客的命令行管理工具，可以用它来安装hexo、生成博客、发布等等操作，node_modules目录下面的hexo才是我们平常所说的2.0、3.0版本。*假如*我想从3.2.0切回3.1.1版本，可以这样：
```
$ cd seanlook
$ hexo uninstall hexo
$ hexo install hexo@3.1.1 --save
```

4. hexo插件
hexo可以通过[插件](https://hexo.io/plugins/)定制自己的功能，如标签、分类、归档、markdown等都是内置的，还有订阅（hexo-generator-feed）、站点地图（hexo-generator-sitemap）、发布为git(hexo-deployer-git)等常用插件，需要安装

```
cd seanlook
hexo install hexo-generator-sitemap --save
hexo install hexo-generator-feed --save
hexo install hexo-deployer-git --save
```


## 2.2 运行`hexo `

命令行运行`hexo s`，在浏览器打开 `http://localhost:4000` 就可以快速在本地预览博客了，超简单。

实际常用的管理命令：
```
hexo clean    #清理缓存文件和生成的发布目录，一般需要归档打包的时候用
hexo generate #将写好的markdown格式文章渲染成html格式来发布或预览
hexo server   #在本地预览整个博客站点，可简写成 hexo s
hexo deploy   #部署博客到网上

hexo d -g     # hexo deploy --generate 缩写，渲染并部署
```

## 2.3 完善hexo
### 2.3.2 标签云和分类页
### 2.3.6 关于和404页面
### 2.3.3 站点统计（百度）
### 2.3.1 主题安装（Next）
### 2.3.4 多说评论
评论
最新评论
### 站内搜索（Swiftype）
### feed和社交链接


# 3. 文章目录使用oschina Git管理


新环境只需要安装好hexo

最后列一下：

1. 打开电脑，我要继续写作了  
先从oschina拉取最新的内容：git pull -u origin master
1. 用markdown pad 2 或Mou本地创作
随时保存。下午继续上午的写作，就不需要再拉取了，因为你没有在其它平台/终端上改动
1. 写到一半天黑了，回家  
把所有改动同步到oschina：oschina:git add . , git commit . git push...
4. 完成一篇要发布  
先hexo d -g在本地预览一下
再执行第3步，把改动推送到oschina仓库
最后发布到github: hexo d -g
5. 回到家，发现有错别字或格式问题  
因为是很小的问题，没必要本地修改、提交、推送，直接在oschina仓库里面在线编辑md文章
你在不急于发布，又没有电脑写作环境时，也可以临时在线写作
6. 在家文思泉涌，或者无聊，继续白天的写作
当然是先进行第1步了，然后重复后面的流程。
7. 回到家里发现，公司的改动没有同步到oschina
没有更好的办法，改怎么写继续怎么写
写完提交同步到oschina，回到公司第一步还是拉去最新的，然后解决/合并冲突
8. 你换电脑了，全新环境
按照文章里面的步骤安装好hexo，解压误source文章目录的博客源码
