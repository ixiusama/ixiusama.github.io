---
layout: post
title: "简明Github Pages与Hexo过程"
date: 2015-11-22 00:13:00
comments: true**
categories: Hexo
toc: true
tags: 
	- Geek
	- 博客
	- Hexo
	- Github Pages
---

这是一篇尽量详尽的独立博客搭建教程，里面介绍了包括但不限于域名注册、DNS设置、github和Hexo设置等过程，这是可能我写得最长的一篇教过程。我想将我搭建博客的过程在一篇文章中尽可能详细地还原出来，希望能给后来者一个明确的指引。让小白都看得懂是我的这篇文章的主旨。


<!-- more -->
# 前言 #
一切都是心血来潮，整个过程应该是从昨天晚上8点在V2EX上看到有人发Hexo的主题感觉很漂亮还有一点*[Material Design](http://dwz.cn/2dapy2 "Material Design")*的风格，十分对我的胃口。


作为一个技术小白，而且英语不是很好很多教程都看得不知如何是好，在网上的很多教程都是程序员写的，学习程序语言多了就会不小心沾染让一些程序的思维，让没有前情提要的小白看得云里雾里的，稍微有些细节描述得不清楚的地方都不知道问哪个？想去百度百度有不是那么的友好，翻了十几页它给我的全是广告，上google又永远都是404。所以，在自己的博客搭建完成之后，我决定要将我搭建博客的过程全记录下来，以供后期和我一样的小白参考。


# 为什么要搭建一个博客？ #
1. 自己可以掌控一切

2. 高度的私人定制

3. 没有各种坑爹的收费服务

4. 有一个真正自己的私人平台


# 我是一个刚刚从新手村出来的小白怎么办？ #
这个教程可能有些难，但是我相信你用心还是能够看懂的。

实在不行的话你还可以看看这个[用静态页面生成静态博客](http://isnowfy.github.io/about-simple-cn.html "用静态页面生成静态博客  by isnowfy") byisnowfy

当然我并不是很希望你一开始就这么做。先把眼神往下挪一下吧。


# 做这个博客要求有什么？ #
1. 碰到问题学会自己解决

2. 有一定的耐心，能够在没有他人的帮助下完成一个博客（PS：学会用搜索引擎）



# 做完以后我能得到什么？ #

- 一个私人博客;
- 一些网页的基础知识;
- 一些别人没有的小技能;
- 打开新世界大门;
- 以后在网上搜寻东西的时候会有加成*buff*;
- 学着用github，享受github的便利，上面有很多大牛，眼界会开阔很多；
- 顺便看看github工作原理，了解最好的团队协作流程;
- 变得有些Geek。


# GitHub Pages是什么？ #

GitHub Pages本用于介绍托管在GitHub的项目， 不过，由于他的空间免费稳定，用来做搭建一个博客再好不过了。

> 虽然也有人讨论过[在GitHub Pages上搭建bolg是否道德](http://www.zhihu.com/question/20717014 "使用 GitHub Pages 来做博客是否道德？——知乎")的问题。但是我觉得哪怕不分享代码，而仅仅是写博客。只要你觉得对得起你的读者就是道德就可以了，因为积累这种知识性的内容和愿意分享的作者，我想没有网站会拒绝吧。

![](http://7xoirq.com1.z0.glb.clouddn.com/P02jekyllrb.png)

# OK！让我们开始吧！ #

## 前情提要 ##
依次下载安装如下软件：

1. [Node.js](https://nodejs.org/en/ "node.js")(我安装的是v5.1.0-x64)
  
![下载Node.js](http://7xoirq.com1.z0.glb.clouddn.com/Node.js.png)

之后没有什么需要注意的 就是一路NEXT就好了

然后我们检查一下是不是要求的组件都安装好了，同时按下`Win`和`R`，打开运行窗口：

![win-run](http://7xoirq.com1.z0.glb.clouddn.com/P02win-run.png)


在新打开的窗口中输入`cmd`，敲击回车，打开命令行界面。（下文将直接用打开命令行来表示以上操作，么么哒！~）


在打开的命令行界面中，分别输入：


    1.` node -v`
    2. `npm -v`


如果结果如下图所示，则说明安装正确，可以进行下一步了，如果不正确，则需要回头检查自己的安装过程。

![Node.js  run](http://7xoirq.com1.z0.glb.clouddn.com/P02Node.js%20%20run.png)

2. [Git](http://git-scm.com/)（我的版本是2.6.3）
3. 
根据自己的Windows版本选择相应的安装文件，要是不知道，就安装32-bit的吧。

![Git下载](http://7xoirq.com1.z0.glb.clouddn.com/Git.png)

和Node.js一样，大部分设置都只需要保持默认，但是出于我们操作方便考虑，建议PATH选项按照下图选择：（不小心跳过了也没有关系我们本次的教程与这个选项没有关系但是这个选项会关系到你完成本次教程的后期调整）

![Git-path-setting](http://7xoirq.com1.z0.glb.clouddn.com/P02Git-path-setting.png)

我们来检查一下Git是不是安装正确了，打开命令行，输入：

    git --version

如果结果如下图所示，则说明安装正确，可以进行下一步了，如果不正确，则需要回头检查自己的安装过程。

![Git run](http://7xoirq.com1.z0.glb.clouddn.com/P02Git%20run.png)


安装运行的本地环境我们安装好了，我们要开始配置网络的环境了。

# 新手篇 #
## 注册GitHub ##

访问：[http://www.github.com/](http://www.github.com/ "github")，在下图的框中，分别输入自己的用户名，邮箱，密码。

![GitHub sign up](http://7xoirq.com1.z0.glb.clouddn.com/P02Github%20sign%20up.png)






> 再次强调不要使用163邮箱，我也不知道为什么反正用163邮箱就是收不到注册邮件。

然后前往自己刚才填写的邮箱，点开Github发送给你的注册确认信，确认注册，结束注册流程。
**一定要确认注册，否则无法使用gh-pages！**

# 创建代码库 #

登陆之后，点击页面右上角的加号，选择**`New repository`**：

![](http://7xoirq.com1.z0.glb.clouddn.com/P02New%20repository.png)

进入代码库创建页面：
在`Repository name`下填写`XXXX.github.io`(XXXX可以填写你的用户名)，`Description (optional)`下填写一些简单的描述（不写也没有关系），如图所示：

![](http://7xoirq.com1.z0.glb.clouddn.com/P02Create%20a%20new%20repository.png)


创建之后，你将会看到如下界面：

![](http://7xoirq.com1.z0.glb.clouddn.com/P02ture.png)

# 开启gh-pages功能 #

点击界面右侧的`Settings`，你将会打开这个库的`setting`页面，向下拖动，直到看见`GitHub Pages`，如图：

![](http://7xoirq.com1.z0.glb.clouddn.com/P02Github-pages.png)

Github将会自动替你创建出一个gh-pages的页面。
如果你的配置没有问题，那么大约15分钟之后，`XXXX.github.io`这个网址就可以正常访问了~
如果`XXXX.github.io`已经可以正常访问了，那么Github一侧的配置已经全部结束了。

# 配置SSH keys #

配置好了我们的本地和网上的那我要如何让本地git项目与远程的github建立联系呢？用`SSH keys`。

# 检查SSH keys的设置 #


首先我们需要检查你电脑上现有的ssh key：

    cd ~/. ssh #检查本机的ssh密钥

# 生成新的SSH Key： #

    ssh-keygen -t rsa -C "邮件地址@youremail.com"

**注意1**: 此处的邮箱地址，你可以输入自己的邮箱地址；

**注意2**: 此处的「-c」的是大写的「c」


系统这时会显示

    Generating public/private rsa key pair.
    Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):

回车就好不需要理

然后系统会要你输入密码：

    Enter passphrase (empty for no passphrase):<输入加密串>
    Enter same passphrase again:<再次输入加密串>

在回车中会提示你输入一个密码，这个密码会在你提交项目时使用，如果为空的话提交项目时则不用输入。这个设置是防止别人往你的项目里提交内容。

注意：输入密码的时候**没有任何提示**，你直接输入就可以了。

最后看到这样的界面，就成功设置ssh key了：

![set ssh key](http://7xoirq.com1.z0.glb.clouddn.com/P02set%20ssh%20key.png)

# 添加SSH Key到GitHub #

在本机设置SSH Key之后，需要添加到GitHub上，以完成SSH链接的设置。

1、打开本地C:\Users\XXXXX(你的电脑用户名)\.ssh\id_rsa.pub文件。此文件里面内容为刚才生成人密钥。如果看不到这个文件，你需要设置显示隐藏文件。准确的复制这个文件的内容，才能保证设置的成功。

2、登陆github系统。点击右上角的 Account Settings--->SSH Public keys ---> add another public keys

3、把你本地生成的密钥复制到里面（key文本框中）， 点击 add key 就ok了

![ssh key](http://7xoirq.com1.z0.glb.clouddn.com/P02ssh%20key.png)

# 测试 #

可以输入下面的命令，看看设置是否成功，git@github.com的部分不要修改：

    ssh -T git@github.com

如果是下面的反馈：

    The authenticity of host 'github.com (207.97.227.239)' can't be established.
    RSA key fingerprint is 00:27:00:a5:00:28:00:36:74:1b:56:4d:00:df:00:48.
    Are you sure you want to continue connecting (yes/no)?

不要紧张，输入yes就好，然后会看到：

    Hi XXXX! You've successfully authenticated, but GitHub does not provide shell access.

# 设置用户信息 #

现在你已经可以通过SSH链接到GitHub了，还有一些个人信息需要完善的。

Git会根据用户的名字和邮箱来记录提交。GitHub也是用这些信息来做权限的处理，输入下面的代码进行个人信息的设置，把名称和邮箱替换成你自己的，名字必须是你的真名（有些人说要真名但是我不置可否），而不是GitHub的昵称。

    git config --global user.name "XXXX"//用户名
    git config --global user.email  "XXXX@mail.com"//填写自己的邮箱

## SSH Key配置成功 ##

若有问题，请重新设置。常见错误请参考：


[GitHub Help - Generating SSH Keys](https://help.github.com/articles/generating-ssh-keys/)

# Hexo介绍 #

Hexo的作者是[tommy351](https://github.com/hexojs/hexo)，官方介绍，Hexo是一个简单、快速、强大的博客发布工具。

# 安装Hexo #

在自己认为合适的地方创建一个文件夹，然后在文件夹空白处按`鼠标右键`，然后点击Git Bash Here。（同样要记住啦，下文中会使用在`当前目录打开命令行`来代指上述的操作）

输入：


    npm install -g hexo

前面的操作完成之后，需要安装一个插件（hexo-deployer-git）才能正常发布文章。

    npm install hexo-deployer-git --save

# 部署Hexo #

    hexo init


Hexo随后会自动在目标文件夹建立网站所需要的所有文件。

输入以下命令

    hexo g
    hexo s

现在我们已经搭建起本地的hexo博客了，执行以上命令，然后到浏览器输入localhost:4000看看。

# 克隆主题 #

建立了Hexo文件之后就可以克隆好看的主题了
可以到下面这个链接进行查看，选择自己喜欢的主题。
[有那些好看的hexo主题？——知乎](http://www.zhihu.com/question/24422335 "有那些好看的hexo主题？")

以我目前使用的yilia主题为例：
[官方项目地址](https://github.com/litten/hexo-theme-yilia "hexo-theme-yilia")

## 安装 ##

第一步输入以下内容：

 `git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia`

第二步配置

修改hexo根目录下的 `_config.yml` ： `theme: yilia`
建议使用Notepad++打开和编辑 否则可能会报错

第三步更新
分别执行以下两个命令


    cd themes/yilia
    cd ..
    cd ..
    git pull


注意：Hexo有两个config.yml文件，一个在根目录，一个在theme下，此时修改的是在根目录下的。

# 本地查看调试 #

    $ hexo g #生成
    $ hexo s #启动本地服务，进行文章预览调试
(“#”是备注可以不用复制)

浏览器输入[http://localhost:4000](http://localhost:4000)，查看搭建效果。此后的每次变更_config.yml 文件或者上传文件都可以先用此命令调试调试成功了之后就可以上传了，尤其是当你想调试出自己想要的主题时。


# 上传文件到服务器 #

    hexo d

期间可以需要输入密码，此处密码是配置ssh的时候所设定的密码。

到此为止你已经开设好一个域名并且已经修改成你喜欢的主题了

# 新技能get√ #

您现在开始可以在这上面写文章了。具体操作如下：

# 添加新文章 #
打开Hexo目录下的`source`文件夹，所有的文章都会以md形式保存在`_pos`t文件夹中，只要在_post文件夹中新建md类型的文档，就能在执行`hexo g`的时候被渲染。您可以执行 hexo s 进行本地化的预览浏览器输入[http://localhost:4000](http://localhost:4000)，查看。

新建的文章头需要添加一些yml信息，如下所示：

    title: hello-world   //在此处添加你的标题。
    date: 2014-11-7 08:55:29   //在此处输入你编辑这篇文章的时间。
    tags: [ACM, UVa, C/C++]  //在此处添加这篇文章的标签，多个标签需要使用`[ ]`来包裹，用`,`来分隔。
    categories: Exercise   //在此处输入这篇文章的分类。
    toc: true  //在此处设定是否开启目录，需要主题支持。
    ---

如果对于 markdown 语言不熟悉的同学可以使用 `markdownpad` 进行编辑编辑过程像在 word 中编辑文件一样的简单。

但是这只是初步的定制化，想要更深入的请 follow me

# 进阶篇 #
## 私人定制 ##


您可以在 _config.yml （根目录下的）中修改大部份的配置。

[官网](https://hexo.io/zh-cn/docs/configuration.html)有详细的说明在此不赘述

 
还有要注意的是在主题的目录下，也有一个_config.yml 配置文件，您可以在这里对您的页面进行更加定制性的修改。

以[yilia主题](https://github.com/litten/hexo-theme-yilia)为例
		# Header
		menu:
		  主页: /
		  所有文章: /archives
		  # 随笔: /tags/随笔
		
		# SubNav
		subnav:
		  github: "#"
		  weibo: "#"
		  rss: "#"
		  zhihu: "#"
		  #douban: "#"
		  #mail: "#"
		  #facebook: "#"
		  #google: "#"
		  #twitter: "#"
		  #linkedin: "#"
		
		rss: /atom.xml
		
		# Content
		excerpt_link: more
		fancybox: true
		mathjax: true
		
		# 是否开启动画效果
		animate: true
		
		# 是否在新窗口打开链接
		open_in_new: false
		
		# Miscellaneous
		google_analytics: ''
		favicon: /favicon.png
		
		#你的头像url
		avatar: 
		#是否开启分享
		share: true
		#是否开启多说评论，填写你在多说申请的项目名称 duoshuo: duoshuo-key
		#若使用disqus，请在博客config文件中填写disqus_shortname，并关闭多说评论
		duoshuo: true
		#是否开启云标签
		tagcloud: true
		
		#是否开启友情链接
		#不开启——
		#friends: false
		#开启——
		friends:
		  奥巴马的博客: http://localhost:4000/
		  卡卡的美丽传说: http://localhost:4000/
		  本泽马的博客: http://localhost:4000/
		  吉格斯的博客: http://localhost:4000/
		  习大大大不同: http://localhost:4000/
		  托蒂的博客: http://localhost:4000/
		
		#是否开启“关于我”。
		#不开启——
		#aboutme: false
		#开启——
		aboutme: 我是谁，我从哪里来，我到哪里去？我就是我，是颜色不一样的吃货…

在这个配置文档中作者都会有着详细的说明，如何对于网页的修改。

如果您实在的遇到了不懂得东西您还可以在[这里](https://github.com/litten/hexo-theme-yilia/issues)（以yilia为例）向作者提出您的疑问和不解的地方。



# 选择合适的域名 #

每当看到别人的博客的炫酷的 .com .cn .org 域名的时候都会觉得很牛逼。而我们这种小白在用博客的时候还是用别人的域名如：.github.io  .qzone.qq.com 这种域名的时候感觉多少有点不爽。

购买域名的网站很多 [godaddy](https://www.godaddy.com/) [阿里云（原万网）](http://wanwang.aliyun.com//) [新网](http://www.xinnet.com/) 中的任意一家，自己权衡价格即可。

> 在中国的话，.cn全都需要进行备案，如果不想备案的话，请注册别的顶级域名

下以阿里云（原万网）为例：

## 1、查域名； ##

你可以选择一个你喜欢的名字，域名就是让人好记嘛！~

![](http://7xoirq.com1.z0.glb.clouddn.com/P02ali%20yuming.png)

点击`查域名`

![](http://7xoirq.com1.z0.glb.clouddn.com/P02goumaiyuming.png)


> **注意：很多的域名第一年的价格可能很便宜但是多几年的话就会非常贵，在选购的时候要注意甄别。**

##  2、确认购买  ##


选择之后`确认购买`

确认购买。修改购买年限，默认是两年，可以修改成1/2/3/5/10年，随自己喜欢。

和淘宝网的购买过程十分的类似。

## DNS解析 ##


购买好后点击头像进入 `管理控制台` 





如下图进入 DNS 解析

![](http://7xoirq.com1.z0.glb.clouddn.com/P02DNSkongzhi.png)

设置以下图进行

![](http://7xoirq.com1.z0.glb.clouddn.com/P02dnsjiexi.png)

其中A的两条记录指向的ip地址是github Pages的提供的ip



192.30.252.153

192.30.252.154



如博客不能登录，有可能是 github 更改了空间服务的ip地址，记得及时到在[GitHub Pages](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/)查看最新的ip即可

www指定的记录是你在 github 注册的仓库。

设置完成后需要等待几分钟


最后，我们对`Github`进行一下配置。
在自己本地的hexo目录下的`source`文件夹中，新建一个`CNAME`文件（注意，没有后缀名。），内容为XXXXX.xxx（您刚才进行购买的域名）。然后再执行一下hexo d，重新上传自己的博客。

![](http://7xoirq.com1.z0.glb.clouddn.com/P02githubshezhi.png)

在github中打开你自己的库，进入库的setting界面，如果看到了如下提示，说明配置成功了。

# OK！~ 教程结束为自己鼓掌吧!~#

