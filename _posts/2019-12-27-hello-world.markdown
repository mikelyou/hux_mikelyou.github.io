---
layout:     post
title:      "Hello, World!"
subtitle:   " \"Hello World, Hello Blog\""
date:       2019-12-27 15:51:00
author:     "Mike Lyou"
header-img: "img/post-bg-2015.jpg"
tags:
    - 生活
---

> “Finally, it works. ”

搭个博客，要了老命。

## 前言

原本搭了一个博客，但觉得有点丑，于是换了一个模板；谁知换模板之后出现了很多问题，导致原本三天可以搞定的事一星期才解决。（当然中间摸鱼的日子也算在里面了）趁现在还记得，先写一下搭建博客的过程，以防以后用得到。

## 博客的搭建

首先把参考的所有内容列在这里：

- 因为不懂cmd命令，我还查了基础的cmd用法：[cmd应用基础 扫盲教程](https://lellansin.wordpress.com/2012/12/15/cmd%E5%BA%94%E7%94%A8%E5%9F%BA%E7%A1%80-%E6%89%AB%E7%9B%B2%E6%95%99%E7%A8%8B/)和[CMD命令进入某个目录](https://blog.csdn.net/aidenliu/article/details/5390113)

- [jekyll博客搭建之艰辛之路(基本概念和处理报错)](https://dailc.github.io/2016/10/29/jekyllbuild.html)

- [ruby 安装 运行](https://www.cnblogs.com/lyy-2016/p/5642032.html)

- [记录一下jekyll安装及遇到的问题](https://wuxin.netlify.com/passages/begin/2017-5-24-jekyll%E5%AE%89%E8%A3%85%E5%8F%8A%E9%81%87%E5%88%B0%E7%9A%84%E9%97%AE%E9%A2%98/)

- 使用的模板：[HuxBlog Boilerplate](https://github.com/Huxpro/huxblog-boilerplate)

- 被放弃的前一模板：[cnfeat/blog.io: 简单直接可用博客模板](https://github.com/cnfeat/blog.io)

使用的各工具版本：

- ruby 2.6.5p114 (2019-10-01 revision 67812) [x64-mingw32]
- gem 3.0.3
- jekyll 4.0.0

搞了一通之后大概猜到问题在哪里了，这个要从各工具的关系说起（我之前完全不懂，可能说的也不对）：

`ruby`是一种脚本语言，而`rubygem`是用`ruby`语言写的一个“程序”，简称`gem`（`ruby 1.9.2`及其以上就已经默认安装了`ruby gem`的）；

`jekyll`是基于`ruby`的，需要在安装`ruby`后通过`gem`命令安装；

（最confusin的一点）在github上fork喜欢的`jekyll`模板后，博客内容实际上还未生成，此时访问只会看到GitHub Pages的“Site Not Found”；我们需要将`repository`给`clown`到本底，并使用`jekyll`“运行”或者说“编译”，产生“`_site`”文件夹，这个文件夹里的内容才是真正显示在博客上的；而使用`jekyll`的一个好处在于，它可以生成本地服务器，在你将一切都编辑好之后，使用`github desktop`一次提交，避免产生很多不美观的修改记录。

## 搭建全过程

- 购买域名：我参考了cnfeat的教程，去godaddy购买的
- 安装`Node.js`和`Git`：参考cnfeat的教程
- 注册GitHub账户
- 配置`SSH Keys`：参考cnfeat的教程
- 注册使用免费DNS服务器：我使用了HE
	-如何配置（搞了半天），虽然不清楚原理，但在域名商、DNS服务商、github仓库三处都需要合理设置，而且设置生效可能会有延迟，清理缓存有时会有奇效。
- Fork别人的博客模板并修改：参考cnfeat的教程（很简单，但新人不看教程完全不知道该店哪里）

这时我决定换模板，随后遇到诸多问题，怀疑人生好几天，然后进行以下操作：
- 安装ruby：这里主要参考这篇文章：[记录一下jekyll安装及遇到的问题](https://wuxin.netlify.com/passages/begin/2017-5-24-jekyll%E5%AE%89%E8%A3%85%E5%8F%8A%E9%81%87%E5%88%B0%E7%9A%84%E9%97%AE%E9%A2%98/)。与文中不同的是，我安装的是最新`ruby 2.6.5`，当时的疑惑是“为什么我没有devkit文件夹？？”实际上不用管它，它在不知道哪里已经装好了，直接尝试安装`jekyll`，如果哪个工具版本不支持，就相应的更新（重装大法好，我不知道重装了多少遍）。
- 安装`jekyll`
- 使用github desktop将仓库clown（也就是博客模板）至本地
- 修改相关内容，并使用jekyll搭建本地服务器进行预览
- 提交修改。此时就可以看到博客的更新了。

很不全面，今晚补充一下。
