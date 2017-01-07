---
layout: post
title: "Shadowsocks 之优化篇"
date: 2015-12-20  10:22:11
comments: true**
categories: VPS
tags: 
	- vps
	- linux
	- shadowsocks
---

{% cq %} 一切困难和考验，都是为了成为更加优秀的自己！ {% endcq %}

Shadowsocks 之优化篇


正常配置完 Shadowsocks 后，Shadowsocks 通常只有100kb/s的速度，看个图片都有可能会卡。

<!-- more -->

## 前言 ##

----------

优化 Shadowsocks server 的前提条件是内核版本在 3.5 以上，可通过uname -ir查看当前内核版本，如果版本过低，需要升级。
以下我的 VPS 内核版本升级的简单步骤：
> VPS ： Digitalocean
> 系统版本： CentOS 7 64bit
更新内核
- 查看当前内核版本信息

	uname -ir
	3.10.0-123.8.1.el7.x86_64 x86_64

Digitalocean 关于 Kernels 的更新操作可参考[这里](https://www.digitalocean.com/community/tutorials/how-to-update-a-digitalocean-server-s-kernel)

- 更新并安装最新版本

	yum update
	yum list --showduplicates kernel	             # 列出可用的 kernel 版本
	--------------------------------
	yum install kernel-*(3.10.0-229.el7)*		 # 安装所需版本


- 验证安装及列出服务器上所有已安装的 kernels：

	cd /boot
	ls vmlinuz*


- 记住版本信息,进入 [Digitalocean 控制面板](https://www.digitalocean.com/community/tutorials/how-to-update-a-digitalocean-server-s-kernel-using-the-control-panel#changing-the-kernel-in-the-digitalocean-control-panel) ,修改想要使用的内核版本。



- Poweroff then poweron.

## [Optimize the shadowsocks server](http://shadowsocks.org/en/config/advanced.html) ##

- 增加 TCP 连接数量

	echo '* soft nofile 51200
	* hard nofile 51200' >> /etc/security/limits.conf
	* 
在启动 ss 服务之前设置下 ulimit

    ulimit -n 511200

编辑 /etc/sysctl.conf 文件

    vi /etc/sysctl.conf

加入以下内容：

    # max open files
    fs.file-max = 51200
    # max read buffer
    net.core.rmem_max = 67108864
    # max write buffer
    net.core.wmem_max = 67108864
    # max processor input queue
    net.core.netdev_max_backlog = 250000
    # max backlog
    net.core.somaxconn = 4096
    # resist SYN flood attacks
    net.ipv4.tcp_syncookies = 1
    # reuse timewait sockets when safe
    net.ipv4.tcp_tw_reuse = 1
    # turn off fast time wait sockets recycling
    net.ipv4.tcp_tw_recycle = 0
    # short FIN timeout
    net.ipv4.tcp_fin_timeout = 30
    # short keepalive time
    net.ipv4.tcp_keepalive_time = 1200
    # outbound port range
    net.ipv4.ip_local_port_range = 10000 65000
    # max SYN backlog
    net.ipv4.tcp_max_syn_backlog = 8192
    # max timewait sockets held by system simultaneously
    net.ipv4.tcp_max_tw_buckets = 5000
    # 
    net.ipv4.tcp_fastopen = 3
    # 
    net.ipv4.tcp_mem = 25600 51200 102400
    # TCP receive buffer
    net.ipv4.tcp_rmem = 4096 87380 67108864
    # TCP write buffer
    net.ipv4.tcp_wmem = 4096 65536 67108864
    # turn on path MTU discovery
    net.ipv4.tcp_mtu_probing = 1
    #
    net.ipv4.tcp_congestion_control = hybla
刷新配置文件使之生效：

    sysctl -p

修改服务器中 shadowsocks 的 json 文件以开启 fast open:

    fast_open: true

SSH 到路由器，进行如下操作:
   
    echo 3 > /proc/sys/net/ipv4/tcp_fastopen

----------

## 锐速 ##

锐速是一款非常不错的TCP底层加速软件，可以非常方便快速地完成服务器网络的优化，配合 ShadowSocks 效果奇佳。目前锐速官方也出了永久免费版本，适用带宽20M、3000加速连接，个人使用是足够了。如果需要，先要在锐速官网注册个账户。

然后确定自己的内核是否在锐速的支持列表里，如果不在，请先更换内核，如果不确定，请使用 [手动安装](http://my.serverspeeder.com/w.do?m=lslm)。

确定自己的内核版本在支持列表里，就可以使用以下命令快速安装了。

    wget http://my.serverspeeder.com/d/ls/serverSpeederInstaller.tar.gz
    tar xzvf serverSpeederInstaller.tar.gz
    bash serverSpeederInstaller.sh
输入在官网注册的账号密码进行安装，参数设置直接回车默认即可，
最后两项输入 y 开机自动启动锐速，y 立刻启动锐速。之后可以通过`lsmod`查看是否有appex模块在运行。

到这里还没结束，我们还要修改锐速的3个参数，`vi /serverspeeder/etc/config`

    rsc="1" #RSC网卡驱动模式  
    advinacc="1" #流量方向加速  
    maxmode="1" #最大传输模式
digitalocean vps的网卡支持rsc和gso高级算法，所以可以开启`rsc="1"`，`gso="1"`。

重新启动锐速

    service serverSpeeder restart

----------

## net-speeder（不推荐限流量的VPS） ##

`net-speeder `原理非常简单粗暴，就是发包翻倍，这会占用大量的国际出口带宽，本质是损人利己，不建议使用。

(1) Ubuntu/Debian 下安装依赖包

    apt-get install libnet1
    apt-get install libpcap0.8
    apt-get install libnet1-dev
    apt-get install libpcap0.8-dev

(2) Centos 下安装依赖包
需要配置 epel 第三方源。下载 epel ：[http://dl.fedoraproject.org/pub/epel/](http://dl.fedoraproject.org/pub/epel/) 。例如，Centos 7 x64：

    wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
    rpm -ivh epel-release-7-5.noarch.rpm
    yum repolist
然后安装依赖包：

    yum install libnet libpcap libnet-devel libpcap-devel

**(3) 下载官方的 tar.gz 压缩包。解压安装运行：**

    wget http://net-speeder.googlecode.com/files/net_speeder-v0.1.tar.gz 
    tar zxvf net_speeder-v0.1.tar.gz
    cd net_speeder
    chmod 777 *
    sh build.sh -DCOOKED

首先你需要知道你的网卡设备名，可以使用 ifconfig 查看。假设是eth0，那么运行方法是:

    ./net_speeder eth0 "ip"

关闭 net-speeder

    killall net_speeder

哦，对了，作者已经将 net-speeder 迁移到 [GitHub](https://github.com/snooda/net-speeder) 了，感兴趣的可以关注、贡献。
