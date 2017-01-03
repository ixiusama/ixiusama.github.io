---
layout: post
title: "正确添加RSS订阅"
date: 2015-11-21 23:23:05
comments: true**
categories: Hexo
tags: 
	- Hexo 
	- RSS订阅
---
 
{% cq %} 疑问，一页页，层出不穷，千百度得解，原来灯火阑珊，一分辛苦一分才！ {% endcq %}

每次看到别人的博客有RSS订阅功能，感觉特别的神奇一直以为是自动的抓取的，只有自己做了之后才发现是博主自己弄出来的，我一个小白，就想着给自己的博客也添加RSS订阅功能。


<!-- more -->

看网上的教程，都是一句话带过，我们毕竟不是大神不可能全部都懂。而我按照网上的教程愣是没弄出来。
弄了大半天。最后，一点一点的终于让我拼凑出来，就此吧目前我所做的记录一下：


首先，先安装`feed`插件 使用如下命令：

    npm install hexo-generator-feed --save


安装完`hexo-generator-feed`后，将其配置到根目录的`_config.yml`

	
	#Extensions
	##Plugins: http://hexo.io/plugins/
	#RSS订阅
	plugin:
	- hexo-generator-feed
	#Feed Atom
	feed:
	type: atom
	path: atom.xml
	limit: 20	
> ps：引用整段代码在markdown 语言中可以用 `TAB` 进行代码的分离


在你当前主题下的_config.yml下，添加RSS订阅链接即可，这里我用的是Yilia主题，subnav下添加rss：

	# SubNav
	subnav:
	rss: "/atom.xml"

添加之后，运行hexo g后，就会在页面上生成RSS图标。如本博客首页。