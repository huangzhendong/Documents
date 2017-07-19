$ git config --list
core.symlinks=false
core.autocrlf=true
core.fscache=true
color.diff=auto
color.status=auto
color.branch=auto
color.interactive=true
help.format=html
http.sslcainfo=C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt
diff.astextplain.textconv=astextplain
rebase.autosquash=true
credential.helper=manager
filter.lfs.required=true
filter.lfs.clean=git-lfs clean %f
filter.lfs.smudge=git-lfs smudge %f
user.name=huangzhendong
user.email=21551070@zju.edu.cn
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true
core.hidedotfiles=dotGitOnly
remote.origin.url=git@github.com:huangzhendong/kylin.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.master.remote=origin
branch.master.merge=refs/heads/master

$ git config --list
core.symlinks=false
core.autocrlf=true
core.fscache=true
color.diff=auto
color.status=auto
color.branch=auto
color.interactive=true
help.format=html
http.sslcainfo=C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt
diff.astextplain.textconv=astextplain
rebase.autosquash=true
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true
core.hidedotfiles=dotGitOnly
remote.origin.url=git@github.com:huangzhendong/kylin.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.master.remote=origin
branch.master.merge=refs/heads/master


第一章（Git&GitHub的基本命名/使用方法）
序言
    有些事项还是需要进行解释一下，由于国内的特殊环境，导致真正的GitHub不能很好的访问，所以国人又搞了一个Coding，而实际上Coding所包含的命令和Git&GitHub是完全一样的，现在又来了一个OSChina什么玩意，真是够了，无形之中加重国人的学习的复杂度。为了方便本文以Coding为主线进行讲解。

1、Git&GitHub的工作流程
（1）Git可以理解为本地的项目管理工具，就是仅仅使用本地安装的Git以及本地仓库（local repository）进行项目管理
（2）GitHub是一个在线的、分布式的项目管理工具，要使用GitHub，需要在GitHub上先注册一个账号

2、关于Git的fork与clone
对于很多初学者可能会对Git（这里统称为Git命令，虽然有些是只能作用于GitHub上的）中的命令产生各种奇怪的想法，下面就fork和clone做一个区分，先看下图
（1）fork，从别人（可以是个人、组织等）在GitHub上的repository中copy一个项目到自己线上的repository中（fork其实是服务器端的克隆）
（2）clone，是指从自己的repository中copy一个项目到本地上（一定要从自己的账号下clone仓库，这样到后面如果想pull request才有权限，否则是没有权限的）
（3）关于其他的概念，大家也可以参考下图

下面以人气很高的bootstrap为例
（1）在浏览器中，使用自己的账号登入GitHub，然后在搜索栏搜索“bootstrap”
（2）点击搜索出来的“bootstrap”，再点击页面上的“Fork”，就在自己的账号下克隆了一个bootstrap项目
（3）然后使用git clone命令将bootstrap项目克隆到本地，命令：git clone  git@github.com:michaelliao/bootstrap.git
（4）然后发现了一个bug或者新增加了一个功能，往自己的仓库推送
（5）感觉自己干的很漂亮，好，那么在GitHub上发起一个pull request，对方能不能接受你的请求就不好说了
读者如想进行深一步的了解，可以参考下面几篇文章
（1）http://www.zhihu.com/question/20431718
（2）http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137628548491051ccfaef0ccb470894c858999603fedf000
（3）https://github.com/oldratlee/translations/blob/master/git-workflows-and-tutorials/workflow-forking.md

3、Git基本操作
首先创建一个项目，分为两种，第一种通过浏览器进行创建，第二种是通过命令创建。
第一步：（当前使用第一种方式）创建一个项目Demo，下面是我在Coding的SSH地址
git@git.coding.net:ToBeJust/Demo.git

其他步：添加签名
>git config --local/global user.name "huangzhendong"
>git config --local/global user.email "21551070@zju.edu.cn"

第二步：在本地创建一个Demo文件夹，并将本地Demo文件夹与远程仓库进行连接
>cd Demo
>git init（初始化本地仓库）
>touch test.txt
>vim test.txt（添加一些文件）
>git add test.txt
>git commit -s -m 'the first commit'(使用-s加上签名)
>git remote add origin git@git.coding.net:ToBeJust/Demo.git（关联到远程仓库，如果出现fatal:remote origin already exists，执行git remote rm origin，再继续操作）
>git push -u origin master，如果远程仓库的Demo不为空，那需要先进行git pull origin master:master(将远程master分支和本地master分支进行合并)，也可以写成git pull origin master

第三步：创建分支
>git branch mapreduceparallel
>git checkout mapreduceparallel

第四步：查看分支
>git branch
>git branch -a

第五步：删除分支
先删除远程分支
>git branch push origin -delete mapreduceparallel（方法一）  
>git branch push origin :mapreduceparallel（方法二）
再删除本地分支
>git branch -D/d mapreduceparallel（删除本地分支）

第六步：推送分支/拉取分支
>git checkout mapreduceparallel
git pull <远程主机> <远程分支>:<本地分支>
>git pull origin mapreduceparallel(==git pull origin mapreduceparallel:mapreduceparallel)
上面命令还等价于git fetch origin mapreduceparallel,git merge mapreduceparallel
>git push origin mapreduceparallel
>git fetch origin branch1:branch2（获取远程分支branch1，如果远程分支不存在就会直接创建本地分支branch2，如果存在就会将远程分支Copy下来到brach2中）


第七步：更新内容，并将更新推送到分支
>git add TEST.md
>git commit -s -m "change sth."
>git push origin master(更新master主分支)
>git push origin dev(更新dev分支)

4、合并分支
情景，当前我有两个分支，一个是master，另一个是pkg
现在，我在pkg分支下做了一些改动，需要合并到远程分支
>git checkout master
>git merge pkg
>git push origin master（记得最后要提交到远程仓库，不然就仅仅是在本地进行了合并）

5、删除项目
情景是这样的，假设我为了做测试建了一个名为Demo的Git仓库，在远程也有一个仓库和这个相对应，但是实验完后我不想要了，那就需要删除整个项目，下面是我做的有效的一种方式
（1）删除本地项目
直接打开文件夹，找到Demo项目，删除，OK
（2）删除远程项目
登入Coding，找到Demo项目，直接删除，OK（其中会提示你，要求你输如登入的密码）

6、常识
(1)查看本地仓库状态
>git status
(2)查看本地仓库额日志
>git log
(3)删除文件
>git rm ./dev.doc(删除本地文件)
>git commit -m 'delete dev document'
>git push origin master(删除远程文件-同步到远程就删除了远程文件)
(4)添加用户名、邮箱
>git config --global user.name "**"
>git config --gobal user.email "***@***"
注：如果不需要全局设置，可以去掉global参数
-----------------------------------------------------------------------时间戳2015-01-10--清理了GitHub上945856510@qq.com和21551070@zju.edu.cn账号下的所有的项目--------------------------------------------
