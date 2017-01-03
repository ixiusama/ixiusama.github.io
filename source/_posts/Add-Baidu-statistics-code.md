---
layout: post
title: "添加百度统计代码"
date: 2015-11-22 0:13:13
comments: true**
categories: Hexo
tags: 
	- Hexo 
	- 百度统计
---

{% cq %} 站在Linus的高度，来看待和分析问题。 {% endcq %}

百度统计算是国内比较全面的一个统计平台了吧。虽然Hexo可以使用google的统计服务但是毕竟有堵墙有些时候还是有些不太方便的。

废话不多说下面我们来用最短的时间来展示怎么样快速的添加百度统计代码。

<!-- more -->
首先你要去[百度统计](http://tongji.baidu.com/ "百度统计")注册账号（和平时的百度账号不同），并在后台获取到相关的百度统计代码：

1.编辑文件themes/`yilia`/_config.yml，添加一行配置代码：（灰色代码的地方可能随着你的主题不同而不同`下同`）

		baidu_tongji: true

2.新建文件themes/`yilia`/layout/_partial/baidu_tongji.ejs，内容如下：


    
		<% if (theme.baidu_tongji) { %>
		<script type="text/javascript">
		#申请的百度统计代码
		</script>
		<% } %>	

3.编辑themes/`yilia`/layout/_partial/head.ejs文件，在</head>之前添加代码：




		<%- partial("baidu_tongji") %>



4.发布



5.百度后台上有代码检测功能（刚上线可能没有这么快可以去和杯咖啡看个猫片），过10分钟左右登陆后台检测一下。


不行的话可以重新再尝试一下以上步骤。