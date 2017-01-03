---
layout: post
title: Python爬虫学习
comments: true
toc: true
mathjax: true
date: 2016-01-31 20:59:55
tags: 
     - python 
     - 学习
     - 爬虫
category: python
---

前记
==

<!-- HTML -->
<blockquote class="blockquote-center"> 人生苦短，我用Python！

</blockquote>

什么是Python爬虫
===========

底下这段话是百度百科对网络爬虫的解释


> 爬虫，即网络爬虫，大家可以理解为在网络上爬行的一直蜘蛛，互联网就比作一张大网，而爬虫便是在这张网上爬来爬去的蜘蛛咯，如果它遇到资源，那么它就会抓取下来。想抓取什么？这个由你来控制它咯。




<!--more-->


其实说简单点就是一段自动化执行的程序，用来在网络上收集你想要的内容，最出名的网络爬虫应用算是 google 和 百度 的网络爬虫了，他们每天都要爬取网络上海量的数据，爬取数据，然后再做数据分析处理，然后通过搜索展示给我们，可以说网络爬虫是搜索引擎的根基。

今天我要讲的网络爬虫肯定没有那么搜索引擎所用的爬虫那么高深，但是我相信复杂的东西其实都是由很多简单的东西构成的，所以今天就来讲下最简单的网络爬虫。

<blockquote class="blockquote-center"> Talk is cheap. Show me the code.

　　Linus Torvalds
</blockquote>

实例
==

我们打开个 TXT 文本写入：

	#coding=utf-8 
	import urllib2 #标注引入python自带的urllib2库

	def fetchWebPage(url):
		page = urllib2.urlopen(url); #打开url链接
		html = page.read() #读取网页内容
		return html; #返回结果

	htmlContent = fetchWebPage("http://www.baidu.com/")
	print htmlContent`

然后把名字改为 `baidu.py` 

运行就会看到网页返回结果，希望大家有机会的话也去敲敲代码实现下。

版本信息

书中演示代码基于以下版本：

语言/框架 | 版本号 
---------|------
Python   | 2.7 


> 参考阅读
[Python 爬虫学习系列教程——极客学院 []()](http://wiki.jikexueyuan.com/project/python-crawler-guide/ "Python 爬虫学习系列教程")