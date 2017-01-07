---
layout: post
title: "yilia主题头像上方背景颜色的修改"
date: 2015-12-22 0:36:21
comments: true**
categories: Hexo
tags: 
	- yilia
	- 主题
	- 头像
	- 背景颜色
	- Hexo
---

原文链接：[yilia主题头像上方背景颜色的修改](http://zhangkaiyue0701.github.io/2015/12/09/hexo_yilia/#yilia_u4E3B_u9898_u5934_u50CF_u4E0A_u65B9_u80CC_u666F_u989C_u8272_u7684_u4FEE_u6539 "yilia主题头像上方背景颜色的修改")
<!-- more -->
首先，我将要使用的图片放入`/themes/yilia/source/img`路径下

然后，更改了yilia主题的css文件样式`/themes/yilia/source/css/_partial/main.styl`
更改内容如下：

	/*修改background为background-image，并设置background-size为cover*/
	.overlay{
	    width: 100%;
		height: 180px;
		background-image: url("../img/bg.jpg"); 
		background-size:cover;
		position: absolute;
		opacity: 0.7;
	}

这样背景就改好啦！

