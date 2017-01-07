---
layout: post
title: Hexo 加入字数统计 WordCount
comments: true
toc: true
mathjax: true
date: 2016-02-14 19:38:05
tags: 
- 字数统计
- WordCount
- Hexo
categories: Hexo
---

<!-- HTML -->
<blockquote class="blockquote-center">
适合年度总结的时候对于自己这段时间的学习写作成果进行总结。
</blockquote>


灵感来自简书。

字数统计的结果跟简书有差异，主要是由于本插件只统计了中文字数和英文单词数。

特别适合年度总结的时候对于自己这段时间的学习写作成果进行总结。

也可以根据文本的多少在文章前面自动加上 **『长文预警！本文属于字数大于1W字的长文。』**

<!--more-->

本文需要的一个工具就是WordCount

项目地址： [https://npmjs.org/package/hexo-wordcount](https://npmjs.org/package/hexo-wordcount)

安装和使用
=====

安装
--

    npm i --save hexo-wordcount

使用
--

以下内容主要以 hexo next 主题为例：

修改 `Themes` 模板文件，在 `Post` （即：`Hexo\themes\next\layout\_macro\post.swig`）文章模板区域加入：

`<span class="post-count">{% raw %}{{ wordcount(post.content) }}{% endraw %}</span>`

即可统计单篇文章的字数。

`<span class="post-count">{% raw %}{{ totalcount(site) }}{% endraw %}</span>`

上面这句是统计总字数的，可以放到`Footer`或其他位置里。

也可以在 `<span class="post-count">` 后  `</span>`前 对显示文本进行个性化定制。（ps：`{% raw %}{{ totalcount(site) }}{% endraw %}` 是总体字数）
 

更新日志
====
- 2016年2月14日 19:48 针对 hexo next 写了对于WordCount的安装




> 参考阅读
- [hexo-wordcount](https://npmjs.org/package/hexo-wordcount)