---
layout: post
title: Travis CI 自动部署 Hexo 博客到 Github(带主题版)
tags:
  - null
comments: true
toc: true
mathjax: true
date: 2017-01-03 18:32:50
category:

---

<!-- HTML -->
<blockquote class="blockquote-center">这个世界是懒人推动的</blockquote>

最近考研而且还有很多麻烦的事情就一直没有更新博客而且还有一些奇奇怪怪的事情，导致了 windoge 10 系统崩溃重装了以后各种环境丢失，而且又碰上Hexo 3.0的更新弄得我一脸蒙蔽。

所以就有很长一段时间没有更新 Blog ，最近一两天有时间弄了但是想到之后如果又碰上了什么奇怪的问题弄得环境变化怎么办？所以就想弄一个“一劳永逸”的办法，彻底的解决这个问题。

所以我就找到 Travis CI ，使用 Travis CI 自动部署Hexo客到 Github 上。

以下是我所做的具体步骤与期间遇到的各种"坑"。

<img src="http://7xoirq.com1.z0.glb.clouddn.com/Travis-CI-logo.jpg" class="full-image" />



## 什么是 Travis CI

> Travis CI 是目前新兴的开源持续集成构建项目，它与 jenkins，GO 的很明显的特别在于采用 yaml 格式，同时他是在在线的服务，不像 jenkins 需要你本地打架服务器，简洁清新独树一帜。目前大多数的 github 项目都已经移入到 Travis CI 的构建队列中，据说 Travis CI 每天运行超过 4000 次完整构建。

<!--more-->

一般通过 Hexo 来写 Blog 的时候：

```
- hexo clean
- hexo g(enerate)
- hexo s #查看在本地的显示效果避免无效 push
- hexo d(eploy)
```

就可以清除项目缓存，生成静态网页，然后`push`静态网页到`Github`，然后访问`https://Yourname.github.io`就可以访问更新后的`Blog`了。



由于仅仅是将静态网页文件上传到`github`上，所以只能在具有整个网站源代码的电脑上进行写作，与文章同步与更新，而且每次都要执行`hexo`代码才能看到上传到`Github`上不仅麻烦要拷贝源码而且还需要每次修改后在本机上编译，前期还行到后期文件大的时候需要的时间不可忽略。

### 解决方法

通过`Travis CI`自动部署，自动发布到`github`上，配置一下，便可实现在每次`git push`需要修改的部分，执行完成并发布等命令。不需要完整的网站源码，只将修改的部分，按照以往的`git`操作：![]()![]()

```
add->commit->push
```

便可自动将源代码`push`到`github`, 然后由`travis`自动`clone`项目，并由`travis`的虚拟机自动执行`hexo`网站的生产, 并且`deploy`更新后的网站到`github`上。

## 博客架构

首先我的博客是使用 `Hexo` 来搭建的，托管到 `Github` 提供的 `Gitpage` 服务上，因为`Hexo`必须要源码才能够编译所以就还是需要在网上`push`整站的源码，但是为了网站自动部署再弄一个仓库就有些过于麻烦了，所以我就弄了一个分支（branch）——blog-source 存放整站的源码，让`Travis CI`自动部署。





![http://7xoirq.com1.z0.glb.clouddn.com/gitpage.jpg](http://7xoirq.com1.z0.glb.clouddn.com/gitpage.jpg)

## 具体配置

## 启用要构建的项目

首先如果你要使用 Travis CI，你必须要 GIthub 账号（好像 Travis CI 只支持构建 github 的项目）和一个项目

使用 Github 账号登录 [Travis CI 官网](https://travis-ci.org/)，如下图

![img](http://7xoirq.com1.z0.glb.clouddn.com/1152636-d069a9d80b01b7e4.png)

登录完后会进入如下界面

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI.jpg)

当然如果你以前没用使用过，所以你登录完是没有上图红框内的内容的，这里是因为我在写这篇博客前已经使用了，所以会有这些内容

接下来我们点击 My Repositories 旁边的 +，意思是添加一个要自动构建的仓库，如下图：

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI%201.jpg)

点击后就会来到如下界面：

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI%202.jpg)

可以看到这个界面会显示当前 github 账号的所以项目，如果没有显示，点击右上角的 “Sync account” 按钮，就可以同步过来了（ps：上次用 windows 电脑始终同步不过来项目，最后换成 mac 可以同步了，最后又换回 windows 也可以了，汗 (⊙﹏⊙)b，不太懂，什么个情况）

居然仓库都同步过来了，那么下一步肯定是要开启你需要构建的仓库，可以看到我开启了 lifengsofts.github.io 这个项目，当然这个也是我就是我的博客啦

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI%203.jpg)

开启后我们会看到如下

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI%205.jpg)

还需要进行一些配置，操作如下

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI%204.jpg)

点击红框的那个菜单按钮，就会出现这样的下拉菜单，我们选择设置，来到这个界面，我们勾选3所指向的菜单即可

Build only if .travis.yml is present：是只有在. travis.yml 文件中配置的分支改变了才构建
Build pushes：当推送完这个分支后开始构建

到这一步， 我们已经开启了要构建的仓库，但是还有个问题就是，构建完后，我们怎么将生成的文件推送到 github 上呢，如果不能推送那我们就不需要倒腾一番来使用 Travis CI 服务了，我们要的结果就是，我们只要想 github 一 push，他就自动构建并 push 静态文件到 gitpages 呢，那么下面要解决的就是 Travis CI 怎么访问 github 了

## 在 Travis CI 配置 Github 的 Access Token

标题已经说得很明白了吧，我们需要在 Travis 上配置 Access Token，这样我们就可以在他构建完后自动 push 到 gitpgaes 了，到这里肯定有人要问了，咋你把用户名密码直接写文件里呢，如果你真有这样的问题，那我只能说呵呵~，但我要告诉你的是写里面肯定是可以 push 成功的

### 在 github 上生成 Access Token

首先我们来到 github 的设置界面，点击到 Personal access tokens 页面，点击右上角的 Generate new token 按钮会重新生成一个，点击后他会叫你输入密码，然后来到如下界面，给他取一个名字（随意取即可），下面是勾选一些权限

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI%205.jpg)

生成完后，你需要拷贝下来，只有这时候显示token（仅显示一次之后无法查看），务必要拷贝下来，如果忘了只能重新生成一个了，拷贝完以后我们需要到 Travis CI 网站配置下。

### 在 Travis CI 配置

配置界面还是在项目的 setting 里面，如下图

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI%206.jpg)

至于为什么我们要在这里配置，我想大家肯定应该明白了，写在程序里不安全，配置到这里相当于一个环境变量，我们在构建的时候就可以引用他。
到这里我已经配置了要构建的仓库和要访问的 Token，但是问题来了，他知道怎么构建，怎么生成静态文件吗，怎么 push 的 gitpages，又 push 到那个仓库吗，所以这里我们还需要在源代码的仓库里创建一个. travis.yml 配置文件，放到源代码的根目录，如下图

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI%207.jpg)

. travis.yml 其中内容如下：

```
language: node_js
node_js: stable

# S: Build Lifecycle
before_install:
- export TZ='Asia/Shanghai'
- npm install -g hexo
- npm install -g hexo-cli

install:
  - npm install
  
before_script:
  - npm install -g gulp

script:
  - git submodule init #用于更新主题, 更新源为自己的主题项目，否则会 clone 最新 NexT 主题，而官方主题配置文件没有设置
  - git submodule update
  - hexo clean && hexo g
  - gulp default #使用 gulp 对流程进行优化

 after_script:
  - cd ./public
  - git init
  - git config user.name "ixiusama"
  - git config user.email "ixiusama@hotmail.com"
  - git add .
  - git commit -m "Update docs"
  - git push --force --quiet "https://${GH_TOKEN}@${GH_REF}" master:master

# E: Build LifeCycle

branches:
  only:
    - blog-source
env:
 global:
   - GH_REF: github.com/ixiusama/ixiusama.github.io.git
   #设置 GH_REF，注意更改 yourname
```

其中给你需要更换的又 git config 后面的配置信息
GH_REF 的值更改为你的仓库地址

项目根目录下再新建`.gitmodules`文件，并写入：

```
[submodule "themes/next"]
    path = themes/next
    url = git://github.com/ixiusama/My_NexT_Theme.git
```

则`build`时更新主题的源是自己修改后的主题, 不能用官网`NexT`主题，如果设置成官网主题会发现最终网站发布样式主题是默认的设置，而覆盖掉了原先自己的主题配置。

到这一步我们配置已经完成了，现在就是见证奇迹的时候了

## Push 文章到 Github

到这一步，我们可以写一篇文章，添加到你的博客的_posts 目录下，如图：

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI%208.jpg)

然后 commit 并 push 到你的 Github 上

```
git push origin blog-source:blog-source
```

如果不出意外，我们可以就可以在 Travis CI 网站看到他已经在构建了，如下图：

![img](http://7xoirq.com1.z0.glb.clouddn.com/Travis%20CI%209.jpg)

构建完成后，我们去网站内就可以看到新提交的page了

未完待续。。。（ Travis CI 自动编译时遇到的各种小坑）



> 参考阅读

- [使用 Travis 自动部署 Hexo(1)](http://www.jianshu.com/p/7f05b452fd3a)
- [使用 Travis 自动部署 Hexo(2)](http://www.jianshu.com/p/fff7b3384f46)
- [Hexo 自动部署到 Github](http://www.tuicool.com/articles/AZf2Yzb)
- [手把手教你使用 Travis CI 自动部署你的 Hexo 博客到 Github 上](http://www.2cto.com/kf/201605/505702.html)
- [Travis CI 自动部署 Hexo 博客到 Github](https://xin053.github.io/2016/06/05/Travis%20CI%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2Hexo%E5%8D%9A%E5%AE%A2%E5%88%B0Github/)