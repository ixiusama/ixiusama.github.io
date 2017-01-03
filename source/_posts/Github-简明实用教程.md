---
layout: post
title: Github-简明实用教程
tags:


comments: true
toc: true
mathjax: true
date: 2016-03-20 10:27:12
category:
---

<!-- HTML -->
<blockquote class="blockquote-center"> Github-简明实用教程
仅介绍常用功能
为的是快速上手 Github </blockquote>

顺带模拟一次安装到团队协作工作的一整个过程

<!--more-->
安装Git(在Windows上)
================

在windows上使用 Git 需要安装各种环境，但是由于安装和配置都比较复杂，就不和你多说了。

现在有一个集成的项目 [git for windows](https://git-for-windows.github.io/ "git for windows")

一路默认安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

安装完成后，还需要最后一步设置，在命令行输入：

	$ git config --global user.name "Your Name"

	$ git config --global user.email "email@example.com"

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。

> 注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

第一步:创建版本库(目录)
=============

第一步:
----

首先，选择一个合适的地方，创建一个空目录：(此处使用桌面)

	$ cd C:\Users\Administrator\Desktop
	$ mkdir learngit
	$ cd learngit
	$ pwd
	C:\Users\Administrator\Desktop\learngit

>为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）**不包含中文**。


第二步：
----

通过`git init`命令把这个目录变成Git可以管理的仓库：

    $ git init

第三步：
----

把文件添加到版本库

>**友情提醒**：千万不要使用Windows自带的**记事本**，会出现报错的情况，建议你下载[Notepad++](http://notepad-plus-plus.org/ "Notepad++")代替记事本。（平时看代码也方便，不同的代码不同的颜色方便识别）



第二步: Git 的基本技能
==============

平时的操作可以直接在刚才创建好的版本库（目录）里面完成，完成后可以进行提交


第一步
---

用命令`git add`告诉Git，把文件添加到**暂存库（stage）**：

    $ git add readme.txt


第二步
---

用命令`git commit`告诉Git，把修改的文件提交到**当前分支（master）**：

	$ git commit -m "wrote a readme file"

 `-m` 后是本次提交的说明，一定要写上，方便以后的查找和阅读，切记不要乱写。


在 Git 中有个很重要的概念 就是 工作区和暂存区（stage）与当前分支（master）

在学习的时候可以参考下图会有助于理解

![3b0c4a98a6c705dd05a722c7395d88d9.jpg](http://moefq.com/images/2016/03/21/3b0c4a98a6c705dd05a722c7395d88d9.jpg)

把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区（stage）；

第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支（master）。


Git的分区概念
--------

 区域名称 | 位置 | 用途 |
---|------|---
 工作区(working copy) | 就是你当前PC看到的目录 | 日常文本操作或者查看 
 版本库(version) | 工作区里的隐藏目录 .git | 维持本地git各种管理，分支管理，暂存管理，备份管理等等，不用刻意在意它 
 暂存区(Stage) | 版本库里的东西 | git add命令添加到的就是stage分区，commit就是将暂存区的目标内容提交到当前本地分支 
 远程区(origin) | 服务端的代码 | 有时候也叫 服务库，作为开发组的同步基准，不要和部署代码的远程服务器混淆了，部署到服务器的其实也是一个服务器上的本地工作分支 


第三步: 远程仓库
=========

到目前为止我们学会了，新建个 Git 目录、修改并提交的方法。

现在我们要来学习一下如何使用远程仓库，这是团队协作代码开源的必要的方法。

相信大名鼎鼎的 [Github](https://github.com/ "Github") 大家都有所耳闻吧，现在我们就要使用它，来进行工作了。

在继续阅读后续内容前，请自行注册[Github](https://github.com/ "Github")账号。由于GitHub仓库与你的仓库之间的传输是需要通过SSH协议来进行通信的。所以我们需要进行一些小操作。

第一步
---

创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Git Bash（可右键目标目录打开），创建SSH Key：

	$ ssh-keygen -t rsa -C "youremail@example.com"

一路回车，使用默认值即可

不出意外的话，你可以在用户目录（C:\Users\Administrator）里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，**不能泄露**出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

第二步
---

登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：

![ssh key](http://7xoirq.com1.z0.glb.clouddn.com/P02ssh%20key.png)

第三步
---

登陆之后，点击页面右上角的加号，选择**`New repository`**：

![](http://7xoirq.com1.z0.glb.clouddn.com/P02New%20repository.png)

进入代码库创建页面：
在`Repository name`下填写`XXXX`(XXXX可以填写任意你喜欢的)，`Description (optional)`下填写一些简单的描述（不写也没有关系），如图所示：

![](http://7xoirq.com1.z0.glb.clouddn.com/P02Create%20a%20new%20repository.png)


创建之后，你将会看到如下界面：

![](http://7xoirq.com1.z0.glb.clouddn.com/P02ture.png)

目前，在GitHub上的这个XXXX仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

现在，我们根据GitHub的提示，在本地的XXXX仓库下运行命令：

	$ git remote add origin git@github.com:ixiusama/XXXX.git

第四步
---

可以把本地库的所有内容推送到远程库上：

	$ git push -u origin master

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样：

从现在起，只要本地作了提交，就可以通过命令：

	$ git push origin master


使用Github 的修改文件流程
----------------

	$ git status # 查看本地仓库的修改状态
	
	$ git add # 暂存文件
	
	$ git commit # 提交文件
	
	$ git push origin master # 提交文件至远程代码库

如果你想了解得更加的深入请访问：

[深入理解学习Git工作流](http://www.cnblogs.com/xirongliu/p/4584653.html "深入理解学习Git工作流")



























常用命令
====
查询问题
----
	# 查询当前git本地仓库存在的问题

	git status

	# 查看自己修改了什么

	git diff [文件路径/文件名]
查询修改历史
------
	# 显示被修改文件的修改统计信息

	git log --stat

	# 逐行显示历史

	git log --pretty=oneline

	# 显示最近[number]条的修改

	git log --stat -[number]

	# 显示具体的修改

	git log -p -2

	# 显示我自己的修改

	git log --stat --author=[Your name]

	# 查看单个文件[file path]最近[times]次修改的记录

	git log --stat -[times] -- [file path]
精准的提交
-----
	git commit -m "[commit message]"
提交写错了没事可以这样做
------------
	# 逐行显示历史

	git log --pretty=oneline

	# 针对目标提交

	git rebase -i [commit name]

	# 或者找出分支名的最近[times]次提交

	git rebase -i HEAD~[times]

	# 等待一会儿后，会进入 vi 界面然后会出现[times]行的提交 和操作提示

	pick: [commit name]
	
	pick: [commit name]
	
	pick: [commit name]
	
	...
	
	# 使用vi编辑操作修改你需要改的那个[commit name]，从pick改成edit，然后保存退出查看日志
	
	git log
	
	# 提交正确的message
	
	git commit --amend -m "[message]"
	
	# 最后重置提交一下
	
	git rebase --continue
>这个方法也可以用于修改commit的文件，不过不建议这样做，建立新的提交就行，错了不丢人，丢人的是知错不改，还藏着
查看我的提交历史
--------
	# 查看完全历史
	
	git log
	
	# 逐行显示历史
	
	git log --pretty=oneline
快速回退工作区版本
---------
	# 工作区回退到上一个版本
	
	git reset --hard HEAD^
	
	# 工作区回退到上上个版本
	
	git reset --hard HEAD^^
	
	# 工作区回退到上第 times 个的版本
	
	git reset --hard HEAD^[times]
	
	# 工作区回退到某个名字[commit] 的版本
	
	git reset --hard [commit]
查看自己输入了什么命令的历史
--------------
	git reflog
撤销工作区修改
-------
	# 撤销目标文件[filename]的修改
	
	git checkout -- [filename]
删除工作区文件
-------
	# 删除工作区的[filename]文件
	
	git rm [filename]
找回错误删除的文件
---------
	# 删除错误的文件[filename]
	
	git checkout [filename]






















































> 参考阅读
- [深入理解学习Git工作流](http://www.cnblogs.com/xirongliu/p/4584653.html "深入理解学习Git工作流")
- [廖雪峰的官方网站之Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000 "廖雪峰的官方网站之Git教程")
- [Git pro](https://git-scm.com/book/en/v2 "Git book")