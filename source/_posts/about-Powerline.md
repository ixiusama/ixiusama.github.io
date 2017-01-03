---
layout: post
title: "关于 Powerline vim 美化插件"
date: 2015-11-21 14:59:27
comments: true**
categories: liunx
tags: 
	- linux 
	- vim
	- 美化插件
	- Powerline
---


{% cq %} 编程是一种艺术，学着从中获得美的享受。程序设计=写作提纲，写程序过程，就是创作过程！ {% endcq %}

关于 Powerline
Powerline 是一款 vim 状态栏美化插件，它还可以美化其他程序比如 


zsh,bash,tmux,iPython,Awesome and Qtile 。

<!-- more -->

> [参考Github](https://github.com/powerline/powerline)
> [参考Powerline 官方手册](https://powerline.readthedocs.org/en/latest/)

这里主要记录我在 bash 上安装及使用方法， vim 插件我使用 vim-airline搭配 powerline 字体符号补充包。
# 安装及使用 #
## 安装插件 ##

----------

需要先安装 `python-pip` 及 `git`，方法自行 Google

安装 powerline

    pip install --user git+git://github.com/powerline/powerline

修改 `~/.profile` 文件，

    sudo vim ~/.profile

添加以下内容到后面：

	if [ -d "$HOME/.local/bin" ]; then
 	   PATH="$HOME/.local/bin:$PATH"
	fi

## 安装字体 ##

----------

我使用 Gnome Terminal，因此使用下面方法安装。

	wget https://github.com/Lokaltog/powerline/raw/develop/font/PowerlineSymbols.otf https://github.com/Lokaltog/powerline/raw/develop/font/10-powerline-symbols.conf
	mkdir -p ~/.fonts/ && mv PowerlineSymbols.otf ~/.fonts/
	fc-cache -vf ~/.fonts
	mkdir -p ~/.config/fontconfig/conf.d/ && mv 10-powerline-symbols.conf ~/.config/fontconfig/conf.d/
使用插件美化 Bash


    source ~/.local/lib/python2.7/site-packages/powerline/bindings/bash/powerline.sh

为了让他自行启动，可以编辑 `~/.bashrc` 文件

    vim ~/.bashrc

添加以下内容：

	if [ -f ~/.local/lib/python2.7/site-packages/powerline/bindings/bash/powerline.sh ]; then
    source ~/.local/lib/python2.7/site-packages/powerline/bindings/bash/powerline.sh
	fi
另 Gnome Terminal 支持 256 色：
添加以下内容到 `~/.bashrc` 文件中：

`if [[ ($COLORTERM == gnome-terminal || $(cat /proc/$PPID/cmdline) == *gnome-terminal* )
   && $TERM != screen* ]]; then
   export TERM=xterm-256color
fi`
此配置使 256 色仅在 Gnome Terminal 中显示且不在 screen/tmux 会话中。

## 总结 ##

更详细的方法参考： [How can i install and user powerline plugin](http://askubuntu.com/questions/283908/how-can-i-install-and-use-powerline-plugin)
