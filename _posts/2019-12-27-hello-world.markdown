---
layout:     post
title:      "Hello, World!"
subtitle:   " 如何搭建个人博客"
date:       2019-12-27 15:51:00
author:     "Mike Lyou"
header-img: "img/post-bg-2015.jpg"
tags:
    - Blog
    - 教程

# excerpt_separator: <!--more-->      # 使自动获取摘要在 `<!--more-->`处停止
---


> 不要停笔，生活还在继续。

## 目录

1. [前言](#前言)
2. [相关的概念和工具](#相关的概念和工具)
3. [搭建博客全过程](#搭建博客全过程)
4. [更新博客方法](#更新博客方法)
5. [后记](#后记)
6. [致谢](#致谢)

## 前言

刚刚开始研究生生活的我，学习知识的欲望又重新被点燃，希望能通过写总结来促进和巩固对知识的学习。就在这时，我发现写博客这个方法，再合适不过了。

于是在 finals 结束后，我开始寻找教程，开始搭建自己的博客。博客的第一个版本，我使用的是 [@cnfeat](https://github.com/cnfeat) 的 [简明 GitHub Pages与 jekyll 教程](https://www.cnfeat.com/blog/2014/05/11/how-to-build-a-blog/) 及配套模板。个人认为教程写的很好，按照教程我一步步搭好了博客。然而这一版博客还没开始用，我就想换模板了，原因是觉得有点丑（虽然后来事实证明丑并不是模版的问题orz）。

于是我找到了另一个模板： [@Hux](https://github.com/Huxpro)[的博客模板](https://github.com/Huxpro/huxblog-boilerplate)。本以为简单换个模板就完事了，谁知出现了很多问题，导致原本三天可以搞定的事一星期才解决（当然中间摸鱼了好几天）。具体遇到的问题会在详细步骤中提到。

历经千辛万苦，在一个平静的下午，终于把[我的个人博客](https://mikelyou.cpm)搭建成功了。

这篇文章详细讲述了我搭建博客的过程，并列出了所有的参考资料，算得上半个教程吧。既可供自己将来查阅，也可供他人查看，解决遇到的相同问题。

这是博客里的第一篇文章，初次与这个世界见面，让我们大喊：
```Hello, world!```

## 相关的概念和工具

在讲搭建博客的具体步骤前，弄清楚一些概念会有所帮助。在搭建博客的过程中会用到多个工具，在这里简单列举一下。如果看不懂可以跳过，在实际搭建过程中出现疑惑再回来看。

###### 什么是域名、DNS 和 IP

- **域名** 就是我们常见的`www.baidu.com`或其他后缀的一串网址，其类似于现实生活中一家店铺的名字，比如“张三烧烤”（我瞎编的）。

- **IP** 是形如`208.80.152.2`（wiki的IP）的一串字符，是网站的真正地址。好比只知道“张三烧烤”这家店的名字并不能带你走到店里，你需要知道它的具体地址，比如“第五大道269号”（也是瞎编的）。

- **DNS** 是将域名和IP连接起来的东西。好比地图册，可以告诉我们“张三烧烤”的具体地址是“第五大道269号”。

- 想了解更详细的内容请自行百度，或者这里我随便找了一篇文章：[域名、DNS、IP地址的对应关系](https://www.jianshu.com/p/6323a4f0ada4)。


###### 什么是ruby、gem 和 jekyll

- **`ruby`**是一种脚本语言。

- `ruby gem`是用`ruby`语言写的一个“程序”，简称**`gem`**（`ruby 1.9.2`及其以上是已经默认安装了`ruby gem`的）。

- **`jekyll`**是基于`ruby`的博客生成“软件”，需要在安装`ruby`后通过`gem`命令安装。

目前常见的博客搭建有两种：一种是 GitHub+jekyll，另一种是GitHub+Hexo。本博客使用前一种 GitHub+jekyll 方法，也只讨论这种方法。

（下面这段是我自己的想法，不一定正确）

在 GitHub 上`fork`喜欢的`jekyll`模板后，博客内容实际上还未生成，此时访问`username.github.io`只会看到 GitHub Pages 的 `“Site Not Found”` 。我们需要将`repository`给`clown`到本地，并使用`jekyll`“运行” 或者说 “编译”，产生“`_site`”文件夹，这个文件夹里的内容才是真正显示在博客上的。而使用`jekyll`的一个好处在于，它可以生成本地服务器，在你将一切都编辑好之后，使用 GitHub Desktop 一次提交，避免产生很多不美观的修改记录。

###### 需要安装以下工具（后面数字为本人所使用的版本号）：

- `ruby 2.6.5`
- `gem 3.0.3`
- `jekyll 4.0.0` 		#本人是在windows系统下安装的

###### 需要注册以下账户（注意妥善保存账号密码）：

- GitHub账户
- 在域名商的账户（如 GoDaddy），用于购买域名
- DNS 服务商账户（如 HE），用于使用 DNS 服务
- ~~Steam 账户，用于搞不定时放松心情~~


###### 购买的域名和GitHub Pages的关系

我们的博客托管在GitHub Pages，也就是`username.github.io`这个仓库（repository）中，而我们购买的域名如`whatever.com`只是一个网址，当我们在浏览器中输入`whatever.com`时，由于 DNS 将二者关联起来，网页会直接跳转至我们的博客，也是我们的仓库`username.github.io`，只不过浏览器中显示的还是`whatever.com`。

###### 准备开始
搭建博客会需要一点耐心和一点钻研精神。在这个过程中如果卡住了，百度一下别人有没有出现过类似的问题，检查一下自己有没有操作错误，善用“重头再来法”和~~“游戏放松法”~~。另外，建议在你平时学习的地方进行这个过程，会比坐在沙发上效率百倍。

如果你已经做好了时间和心理的准备，就开始搭建你自己的第一个博客吧。冲鸭~

## 搭建博客全过程

我建议在开始所有操作之前，打开一个记事本或笔记软件，把所有用到的网址、内容、参考文章统统记下来，害怕泄露隐私就写在纸上，以防忘记。无论是什么东西，忘记了都很麻烦。

博客的搭建主要参考了 **[@陈素封cnfeat](https://github.com/cnfeat)** 的 **[简明 GitHub Pages与 jekyll 教程](https://www.cnfeat.com/blog/2014/05/11/how-to-build-a-blog/)** 以及 **[@无心CasualMing](https://github.com/CasualMing)** 的 **[jekyll安装](https://wuxin.netlify.com/passages/begin/2017-5-24-jekyll%E5%AE%89%E8%A3%85%E5%8F%8A%E9%81%87%E5%88%B0%E7%9A%84%E9%97%AE%E9%A2%98/)** 两篇教程， 使用了 **[@黄玄Hux](https://github.com/Huxpro)** 的 **[博客模板](https://github.com/Huxpro/huxblog-boilerplate)**。

接下来是搭建博客的详细步骤：

###### 1. 购买域名：
我在域名商  ~~去他爹~~  [GoDaddy](https://www.godaddy.com)  购买的。购买过程很简单，难点在于想好你的域名叫什么；购买保护隐私的钱和域名价格差不多了，我看到的教程都不建议购买。参考cnfeat的教程。

###### 2. 注册DNS服务：
广受好评的有国内服务商[DNSpod](http://www.dnspod.cn)和国外服务商[HE](https://ipv6.he.net)。DNSpod 的使用参考cnfeat的教程，HE 的使用参考这篇教程[HE的使用教程](https://www.ancii.com/aqz5yz5ad/)。这一步先注册，具体设置看后面。

###### 3. 安装`Node.js`和`Git`：
参考cnfeat的教程。

###### 4. 注册GitHub账户：
前往[GitHub官网](https://github.com)。取个好名字，不要杀马特或中二病突发，将来仓库的名字必须是`你的用户名.github.io`。

###### 5. 配置`SSH Keys`：
参考cnfeat的教程。其教程中的代码都是在`cmd`中输入的，前面的`$ `不是我们需要输入的内容。实在不懂可以先看看[cmd应用基础扫盲教程](https://lellansin.wordpress.com/2012/12/15/cmd%E5%BA%94%E7%94%A8%E5%9F%BA%E7%A1%80-%E6%89%AB%E7%9B%B2%E6%95%99%E7%A8%8B/)。

###### 6. 将独立域名与 GitHub Pages 的空间绑定

- DNS 设置：前往DNS服务商填写配置，配置方法分别参考 cnfeat的教程 和 HE的使用教程。（HE似乎不能添加`·`记录，就改填`@`记录吧。`A`记录是GitHub Pages的IP, `NS`记录是DNS服务商自己提供的网址，`CHNAME`记录是形如`username.github.io`的你的博客仓库, `TTL`都设置成`86400`就没问题。没反应就清理一下缓存。）

- 在 GoDaddy 修改 DNS 地址：找到名为 Nameservers(NS) 的设置，将其原有内容删除，修改为 DNS 服务商提供的地址。设置方法分别参考 cnfeat的教程 和 HE的使用教程。

- 在GitHub仓库填写`CHANME.md`文件，或在设置中填写个性化域名，即你购买的形如`whatever.com`的域名。

虽然不清楚原理，但似乎必须上面三项都需要设置正确，才可以访问博客。这里卡主不要弃疗，设置生效可能会有延迟。清理浏览器缓存有时会有奇效，具体方法百度。（我在这卡了很久，清理缓存瞬间解决）

###### 7. 使用 GitHub Pages 建立博客：
对于多数人来说，就是直接fork别人的模板啦，方法参考cnfeat的教程（这里网址写的很容易看错，多看几遍）

**！**就在这时我突然决定换模板，随后遇到诸多问题，怀疑人生好几天，然后发现还少了后面两步。

###### 8. 安装`ruby`（包括`rubygem`）：
这里主要参考这篇文章: [jekyll搭建](https://wuxin.netlify.com/passages/begin/2017-5-24-jekyll%E5%AE%89%E8%A3%85%E5%8F%8A%E9%81%87%E5%88%B0%E7%9A%84%E9%97%AE%E9%A2%98/)。

与文中不同的是，我安装的是最新`ruby 2.6.5`，当时的疑惑是“为什么我没有devkit文件夹？？”

实际上不用管它，它在不知道哪里已经装好了，直接尝试安装`jekyll`，如果哪个工具版本不支持会有提示，然后就相应的更新（重装大法好，我不知道重装了多少遍）。

在国内gem的源似乎被墙，可参考[这篇文章](https://dailc.github.io/2016/10/29/jekyllbuild.html)。

###### 9. 安装`jekyll`：
也参考这篇文章： [jekyll搭建](https://wuxin.netlify.com/passages/begin/2017-5-24-jekyll%E5%AE%89%E8%A3%85%E5%8F%8A%E9%81%87%E5%88%B0%E7%9A%84%E9%97%AE%E9%A2%98/), 以及 [jekyll官方主页](http://jekyllcn.com/)。

**至此，博客的搭建工作完成。**

## 更新博客方法

现在博客已经搭建成功，并且事实上，我们已经可以通过在网页编辑`username.github.io`仓库内的内容来更新博客了（可以尝试一下）。但是大家一般不推荐在网页端操作，而是采用下面的方法：**通过搭建本地服务器，在修改的同时随时预览网页，确认无误后一次性提交更新。**这样的好处在于，可以及时预览编辑产生的效果，且不会产生大量修改记录。第一次可能会觉得很复杂，但熟悉操作后就会比在网页操作方便很多。

具体步骤如下：

###### 1. 将仓库clown至本地
使用 [GitHub Desktop](https://desktop.github.com) 将仓库（也就是博客模板）clown至本地。参考cnfeat的教程。

###### 2. 使用`jekyll`搭建本地服务器
这一步可参考 [jekyll搭建](https://wuxin.netlify.com/passages/begin/2017-5-24-jekyll%E5%AE%89%E8%A3%85%E5%8F%8A%E9%81%87%E5%88%B0%E7%9A%84%E9%97%AE%E9%A2%98/) 中“安装jekyll”那一节。

我的仓库位置在`E:\GitHub\mikelyou.github.io`，需要以管理员模式打开`cmd`并输入一下几行命令：
```
E:					#进入E盘
cd E:\GitHub\mikelyou.github.io		#进入仓库所在目录
jekyll serve				#开服，网址会写在下面，我的是`http://127.0.0.1:4000`

Ctrl+C					#关服
```

###### 3. 修改或添加内容
修改本地文件，然后在本地服务器生产的网页就可以看到改动。我们可以反复修改直至满意。

修改和添加内容个人觉得很简单，就是在文件之间抄一抄改一改。好的模板都会有详细的说明文件`README.md`，并会在相关代码出加有注释，不(ai)予(mo)赘(neng)述(zhu)。

这里有 **[GitHub Markdown语法](https://help.github.com/cn/github/writing-on-github/basic-writing-and-formatting-syntax#ignoring-markdown-formatting)** 的官方帮助页面。

关于仓库中各个文件夹是干什么用的，可以参考 **[jekyll官方文档](http://jekyllcn.com/docs/structure/)**。

###### 4. 上传更新
保存本地文件的修改，关闭服务器，在GitHub Desktop一次性上传所有更新，可以记录一下改了哪里。然后博客就更新啦。

## 后记

本人是学材料专业的，这些玩意儿真的完全不懂，好在以前学过基础的编程，能看得懂简单的配置文件。

虽然思想上有所准备，但搭建博客的过程还是比我想象的更曲折一点。有句话说，“专业的事，留给专业的人做”，而能够利用别人专业的成果，做自己要做的事，则是我等需要具备的能力。搭建博客的过程着实让我学到了很多，希望在今后更新博客的过程中，依然可以持续不断的学习。

欢迎交流和指点。

2019年12月27日 于Science图书馆

## 致谢

特别感谢 **[@黄玄Hux](https://github.com/Huxpro)** 精致详细的博客模板，以及 **[@陈素封cnfeat](https://github.com/cnfeat)** 与 **[@无心CasualMing](https://github.com/CasualMing)** 的教程。

本人不才，能在短短一周内搭建出一个高端大气上档次的个人博客，靠的当然有个人的努力，但也绝对离不开各位陌生大佬们的帮助，在这里向大佬们表示感谢。建立此博客以及撰写此文所用到的参考资料都在下面列出。本人学识和精力有限，如有错误，欢迎斧正。

###### 参考模板和教程：

- Hux的模板和使用说明：
	- 模板（本博客使用）：[HuxBlog Boilerplate](https://github.com/Huxpro/huxblog-boilerplate)
	- 使用说明：[README.zh.md](https://github.com/Huxpro/huxblog-boilerplate/blob/master/README.zh.md)

- cnfeat模板及教程：
	- 模板：[cnfeat/blog.io: 简单直接可用博客模板](https://github.com/cnfeat/blog.io)
	- 教程（主要参考）：[如何搭建一个独立博客——简明 GitHub Pages与 jekyll 教程](https://www.cnfeat.com/blog/2014/05/11/how-to-build-a-blog/)

- ruby gem 与 jekyll 的安装和使用
	- CasualMing 的 jekyll安装（主要参考）：[jekyll安装及遇到的问题](https://wuxin.netlify.com/passages/begin/2017-5-24-jekyll%E5%AE%89%E8%A3%85%E5%8F%8A%E9%81%87%E5%88%B0%E7%9A%84%E9%97%AE%E9%A2%98/)
	- jekyll博客搭建：[jekyll博客搭建之艰辛之路(基本概念和处理报错)](https://dailc.github.io/2016/10/29/jekyllbuild.html)

- 官方网站们：
  - [GoDaddy](https://www.godaddy.com)
  - [DNSpod](http://www.dnspod.cn)
  - [HE](https://ipv6.he.net)
  - [GitHub](https://github.com)
  - [jekyll](http://jekyllcn.com/)


- 其他参考
	- [GitHub Markdown语法](https://help.github.com/cn/github/writing-on-github/basic-writing-and-formatting-syntax#ignoring-markdown-formatting)

	- [cmd应用基础扫盲教程](https://lellansin.wordpress.com/2012/12/15/cmd%E5%BA%94%E7%94%A8%E5%9F%BA%E7%A1%80-%E6%89%AB%E7%9B%B2%E6%95%99%E7%A8%8B/) 和 [CMD命令进入某个目录](https://blog.csdn.net/aidenliu/article/details/5390113)

	- [域名、DNS、IP地址的对应关系](https://www.jianshu.com/p/6323a4f0ada4)
