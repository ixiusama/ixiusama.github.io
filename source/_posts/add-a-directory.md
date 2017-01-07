---
layout: post
title: "给文章加上目录"
date: 2015-12-22 11:36:22
comments: true**
categories: Hexo
toc: true
tags: 
	- yilia
	- 主题
	- 目录
	- Hexo
---

{% cq %} 目标分解，目标指导行动！在使用中学习，用到什么学什么，需要什么学什么！不要灌输，而要吸收 {% endcq %}

# 正文 #
本段参考文章[VoidKing的hexo主题优化](http://www.voidking.com/2015/05/31/deve-hexo-theme-optimize/)  [twiceyuan的为Hexo添加文章目录](http://twiceyuan.com/2015/01/12/%E4%B8%BAHexo%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E7%9B%AE%E5%BD%95/) 以及[The_D的关于github和hexo](http://zhangkaiyue0701.github.io/2015/12/09/hexo_yilia/#u7ED9_u6587_u7AE0_u52A0_u4E0A_u76EE_u5F55)
大家要是写了一篇长文章，当然是生成相应的目录更有利于阅读啦，下面讲一下怎么改造yilia主题使article生成目录！

<!-- more -->
 
## 显示效果 ##
效果如本文
文章目录
修改`/themes/yilia/layout/_partial/article.ejs`，在<%- post.content %>前面加上如下代码：

	 <% if(post.toc !== false){ %>
		<div id="toc" class="toc-article">
		  <strong class="toc-title">文章目录</strong>
		  <%- toc(post.content) %>
		</div>
	<%}%>

修改`/themes/yilia/source/css/_partial/article.styl`，在末尾加上如下代码

	 /*toc*/
	.toc-article
	  background #eeeeee
	  margin 0 0 0 0.2em
	  padding 1em
	  border-radius 5px
	  .toc-title
	    font-size 120%
	  strong
	    padding 0.3em 1
	ol.toc
	  width 100%
	  margin 1em 2em 0 0
	#toc
	  line-height 1.5em
	  font-size 1em
	  float right
	  .toc
	    padding 0 
	    li
	      list-style-type none
	  .toc-child 
	    padding-left 1.5em
	#toc.toc-aside
	  display none
	  width 13%
	  position fixed
	  right 2%
	  top 320px
	  overflow hidden
	  line-height 1.5em
	  font-size 1em
	  color color-heading
	  opacity .6
	  transition opacity 1s ease-out
	  strong
	    padding 0.3em 0
	    color color-font
	  &:hover
	    transition opacity .3s ease-out
	    opacity 1
	  a
	    transition color 1s ease-out
	    &:hover
	      color color-theme
	      transition color .3s ease-out

在编辑md文件时，在头部添加toc: true，OK！大功告成！

有BUG,暂时没有头绪。想想先...







# 大标题1 #
## 小标题1 ##
## 小标题2 ##
## 小标题3 ##
# 大标题2 #
## 小标题1 ##
## 小标题2 ##