---
layout: post
title: 提高姿势水平
date: 2016-01-01 14:09:48
comments: true
toc: true
mathjax: true
tags: 
    - 姿势
    - 翻墙
    - ss
category: VPS

---
{% cq %} 生命不息，折腾不止

————罗永浩 {% endcq %}

写在前面：今年是新年的第一天，从昨天一直happy到今天早上8点才睡下。 ~~原本说要先写一个过去一年的总结的，但是无奈看到这个还没有做的文章......~~ ~~我是来补档的~~使用Docker搭建SS服务实现科学上网

<img src="http://7xoirq.com1.z0.glb.clouddn.com/docker.jpg" class="full-image" />

本文基于 [Crossing's Blog](http://crossingmay.com/2015/12/10/dockerforfree/) 转载并修改。
<!--more-->
一、Docker介绍
==========

Docker是什么？

Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）。几乎没有性能开销,可以很容易地在机器和数据中心中运行。最重要的是,他们不依赖于任何语言、框架或包装系统。

利用docker ，我们可以很方便的搭建各类服务比如wordpress ,nginx，Minecraft等等，上述这些容器 阿水都已经一一尝试了一遍，比如wordpress用docker还是有诸多不便，图片上传等服务有异常。不过据悉微软也相当支持该技术，即将发布针对docker的小型操作系统。除了搭建以上这些，像SS这种科学上网肯定也是可以的。

二、应用
====

国内有很多docker创业型公司提供docker服务，并且有一定的免费额度，比如时速云，DaoCloud，灵雀云 等等，就不一一列举了，试用之后都挺不错，比如我开发web应用时就是用的时速云搭建的Mongodb服务，因为灵雀云已经开通了亚太地区的docker服务器，很容易达到番茄的目的，今天就跟你介绍一下如何使用灵雀云免费容器服务搭建SS并获取账号地址。

注册账户
----
首先打开[灵雀云](https://console.alauda.cn/ap/register?)注册页面，注册完成后,进去控制台，控制台地址:https://console.alauda.cn/。

创建服务应用
------
如下图，将选项卡调整到 香港一区（AZURE），点击 创建服务。

 

选择最后一项 Docker/第三方镜像


将【`index.alauda.cn/dubuqingfeng/ubuntu-shadowsocks`】填入，点击 选择

docker执行步骤
1.打开终端，ssh登陆（可以到hostus的控制台里添加SSH keys，这样就不需要输入登陆密码了）

	$ ssh root@[ip address]  #hostus提供的vps的ip
2.安装SS

	docker pull tommylau/shadowsocks
	or

	docker pull oddrationale/docker-shadowsocks
3.SS配置

	docker run -d -p 2015:2015 oddrationale/docker-shadowsocks -s 0.0.0.0 -p 2015 -k [password] -m aes-256-cfb #input your password instead [password]
4.检查

	docker ps
`status`显示up就是安装成功了！

5.退出`sshexit`

6.维护：如果容器挂掉，可以`docker stop` `docker rm`死掉的容器，从头再来一次就可以啦！



> Tip 跟着这篇教程我也搭了一个自己的ss服务，使用一个星期了，在晚上高峰期的时候看u2b会卡顿，为了流畅就只能降低分辨率，最高仅支持720p，如果不在意这几点，感觉还是相当不错的。
2015年12月以后灵雀云的北京1区和香港1区都不能再使用优惠券了，所以打算采用灵雀云的同学，都要充点钱进去，一天24小时开着大概也只要5毛钱，一个月连续差不多15块钱。关注灵雀云微信号后，发用户名和邮箱给后台，还能获得5元香港1区的礼品券，每天只用8小时，可以使用1个月（PS：是的，这里就是广告，然而占了广告位却拿不了广告费～）。（pps：香港1区的出口带宽比国内要好很多。）

总结
==
本站资源均来源于网络，仅供交流学习之用，严禁作为商业用途，请自觉于观看后24小时内忘记。本片版权归原作者所有，由此引发的任何版权纠纷本站概不负责。

> 参考阅读
[使用Docker搭建SS服务实现科学上网](http://ashui.net/archives/2015/1041.html)

> [在Docker中部署Shadowsocks](http://www.jianshu.com/p/864a7d2a2a5f)

> [基于 Docker － 5 分钟科学上网](https://ruby-china.org/topics/27455)

> [Docker + DigitalOcean + Shadowsocks 5分钟科学上网](http://liujin.me/blog/2015/05/27/Docker-DigitalOcean-Shadowsocks-5-%E5%88%86%E9%92%9F%E7%A7%91%E5%AD%A6%E4%B8%8A%E7%BD%91/)

> [曲径没了，如何使用Docker快速构建你的专属翻@墙服务？](http://dockone.io/article/550)
> 