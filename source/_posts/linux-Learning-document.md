---
layout: post
title: "Linux 学习手札"
date: 2015-11-21 14:59:27
comments: true**
categories: liunx
tags: 
	- linux 
	- 学习
	- 小白
---


{% cq %} 无论你读什么书，都应当问问自己：『为什么我要读它？我想从中获取什么？』如果你不能给予自己满意的回答，你就应当放弃它。 {% endcq %}


Linux 学习对于我来说一直以来都是断断续续的，上手过的系统很多 [ubuntu](www.ubuntu.com/download) [redhat](http://www.redhat.com/en/resources/rhel-desktop-datasheet) [debian](http://www.debian.org/) [fedora](https://getfedora.org/) [startos](http://www.startos.org/) [centos](https://www.centos.org/) 但是都没有坚持下去，因为想找到一个通俗易懂的Linux 的教程真的是难上加难。


直到我用了kali Liunx 感觉居然还不错，这个不是日常使用版本的 Liunx 的系统上手居然有意外的随手感，难道是我不太喜欢束缚？就像我用安卓机的第一天到手还不到12个小时就要去root它一样。233 kail Liunx 系统只有一个账号（root）虽然你可以添加其他没有root权限的账号但是感觉怪麻烦的，所以没有理。对于其他的系统的话都是默认没有root的账号存在的，root 账号在 Linux 中是一个禁忌的存在因为它的权限很高它甚至可以命令系统自己删掉自己。这在windos 中是根本不能想象的。

废话不多说，这篇手札是我从我的Kali Linux 学习手记中整理出来的。


<!-- more -->
 
首先我们要说的是 sudo 命令：
  这个命令是用于一些需要使用 root 权限的命令获取权限的一个命令用法：

    sudo +需要root权限的命令


