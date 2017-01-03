---
layout: post
title: 为 Next 主题文末添加版权等信息
comments: true
toc: true
mathjax: true
date: 2016-02-15 11:29:55
tags: 
- Next
- Hexo
- 版权信息
category: Hexo
---

前言
==

平时在博客上面写点感想，想给文章自动添加一个版权声明以及自动文章的链接，样式应简洁，信息应便于复制。

先谈谈一下自己的要求。发布一篇文章之后可以在文末自动生成一个该文的链接，并且配合版权声明。而且是在每篇文末，不是在网站。
要求有了，就看下一步怎么实现了。先确定一下代码放置的位置，因为是文末，所以经过分析模板代码最终决定放在如下代码之后。话说HTML代码不懂，英文还是看得明白一点点。


<!--more-->

正文
==
对于 `hexo next` 主题
-----------------

对于 `hexo next` 主题而言先找到（`\themes\next\layout\post.swig`）

在区域内添加如下代码：

	  <div class="page-footer">
	      {% raw %}{% if not is_index %}{% endraw %}
	        <div id="eof" class="print-invisible">
	          <hr class="eof">
	        </div>
	        
	        <div class="copyright" style="clear:both;">
	           <p><span>本文标题:</span><a href="{% raw %}{{ url_for(page.path) }}{% endraw %}">{% raw %}{{ page.title }}{% endraw %}</a></p>
	           <p><span>文章作者:</span><a href="/" title="访问 {% raw %}{{ theme.author }}{% endraw %} 的个人博客">{% raw %}{{ theme.author }}{% endraw %}</a></p>
	           <p><span>发布时间:</span>{% raw %}{{ page.date.format("YYYY年M月D日 - HH时MM分") }}{% endraw %}</p>
	           <p><span>最后更新:</span>{% raw %}{{ page.updated.format("YYYY年M月D日 - HH时MM分") }}{% endraw %}</p>
			   <p><span>本文字数:</span><span class="page-count">本文一共有{% raw %}{{ wordcount(page.content) }}{% endraw %}字</span></p>
	           <p><span>原始链接:</span><a href="{% raw %}{{ url_for(page.path) }}{% endraw %}" title="{% raw %}{{ page.title }}{% endraw %}">{% raw %}{{ page.permalink }}{% endraw %}</a></p>
	           <p><span>许可协议:</span><i class="fa fa-creative-commons"></i> <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/" title="Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)">Attribution-NonCommercial 4.0</a></p>
	           <p><span>转载请保留以上信息。</span></p>
	        </div>
	      {% raw %}{% endif %}{% endraw %}
	
		  {% raw %}{% if not is_index and (post.prev or post.next) %}{% endraw %}
	        <div class="post-nav">
	          <div class="post-nav-prev post-nav-item">
	            {% raw %}{% if post.prev %}{% endraw %}
	              <a href="{% raw %}{{ url_for(post.prev.path) }}{% endraw %}">{% raw %}{{post.prev.title}}{% endraw %}</a>
	            {% raw %}{% endif %}{% endraw %}
	          </div>
	
	          <div class="post-nav-next post-nav-item">
	            {% raw %}{% if post.next %}{% endraw %}
	              <a href="{% raw %}{{ url_for(post.next.path) }}{% endraw %}">{% raw %}{{post.next.title}}{% endraw %}</a>
	            {% raw %}{% endif %}{% endraw %}
	          </div>
	        </div>
	      {% raw %}{% endif %}{% endraw %}
	
	    </div>

对于其他主题
------
可以参考 [hexo-theme-yelee](https://github.com/MOxFIVE/hexo-theme-yelee/commit/0e452a4aaffffce735c2497a2960b2eabc523f6e) 这个主题的设置

更新历史
- 2016年2月15日 19:54 初稿

> 参考阅读
- [文末自动插入“版权声明”神马的 作者：ZWWoOoOo](http://zww.me/archives/25440)
- [article copyright 文末版权声明](https://github.com/MOxFIVE/M-Hexo-Blog/issues/13 "article copyright 文末版权声明")
- [为Google Blogger添加自动版权声明和文章链接的方法](https://www.howsci.com/google-blogger-auto-copyright-and-permalink.html "为Google Blogger添加自动版权声明和文章链接的方法")
- [漩涡的 Blog](https://xuanwo.org/ "漩涡的 Blog")