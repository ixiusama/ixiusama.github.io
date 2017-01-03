---
layout: post
title: 团队成员在使用 Github 的时候会遇到的问题问题
tags:
  - null
comments: true
toc: true
mathjax: true
date: 2016-03-22 13:14:44
category:
---

<!-- HTML -->
<blockquote class="blockquote-center">实践出真知</blockquote>


问题1：如何上传？问题2：我是传到`github`的哪个地方，是新建立的`repository`还是其他地方？问题3：`fork`团队文件，我知道了，但如何将`github`上的东西`pull`到我的`baidugit`？问题4：如何修改已经上传的文件

<!--more-->

答：问题一

第一步：创建一个文件

    $ cd C:\Users\Administrator\Desktop
    $ mkdir learn
    $ cd learn
    $ pwd
    C:\Users\Administrator\Desktop\learn

![009b667264ecaf57d77e943754a38bd9.png](http://moefq.com/images/2016/03/22/009b667264ecaf57d77e943754a38bd9.png)


创建完毕如上图


第二步：通过`git init`命令把这个目录变成Git可以管理的仓库：

    $ git init

如图：

![f6b31404edd98ff70099b7609905b5df.md.png](http://moefq.com/images/2016/03/22/f6b31404edd98ff70099b7609905b5df.md.png)

第三步：在『文件夹里面工作』
和正常一样在文件夹里面写东西
例如我现在在里面写了一个文件 index.html

![43aeeb8f6d645482d06e25490d47fba0.md.png](http://moefq.com/images/2016/03/22/43aeeb8f6d645482d06e25490d47fba0.md.png)

第三步：用命令`git add`告诉Git，把文件添加到暂存库（stage）：

    $ git add index.html

![f6b31404edd98ff70099b7609905b5df.png](http://moefq.com/images/2016/03/22/f6b31404edd98ff70099b7609905b5df.png)


然后用命令`git commit`告诉Git，把修改的文件提交到当前分支（master）：

    $ git commit -m "wrote a readme file"

![af256e0aebf073133f46c98aea890616.png](http://moefq.com/images/2016/03/22/af256e0aebf073133f46c98aea890616.png)

第四步：连接远程代码库
在github上创立项目
刚才新建了个项目叫 dome 

![d4e30b4c4eb152c8480429a6f6b298e2.png](http://moefq.com/images/2016/03/22/d4e30b4c4eb152c8480429a6f6b298e2.png)

箭头指向的是其 ssh 地址

![f8317ea1717a957b967e5a3b775698f3.png](http://moefq.com/images/2016/03/22/f8317ea1717a957b967e5a3b775698f3.png)

刷新下github 就会在 dome下看到

![d912adc240fc2c6ad8614314ccc5f907.png](http://moefq.com/images/2016/03/22/d912adc240fc2c6ad8614314ccc5f907.png)

Ok现在就上传成功了
 

答问题二：传到github的新建立`repository` 下你打开网页就能看到。
答问题三：fork团队文件就是相当于在你的账号下开了一个仓库，这个仓库你有完全的权限，不用再开一个仓库。如果你是想下载你的仓库的话可以使用clone 命令
如我的dome仓库的下载 这个命令会下载到你运行git的位置。
    git clone git@github.com:ixiusama/dome.git
答问题四：就像你上传文件一样在本地修改好文件再上传一次就可以了。Github会自动的修改文件。
