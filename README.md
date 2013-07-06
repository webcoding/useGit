useGit
======

这是一个学习Git 用于测试的项目，所需软件

- 命令行 - Git客户端 [http://code.google.com/p/msysgit/downloads/list](http://code.google.com/p/msysgit/downloads/list)
- 图形化界面 - TortoiseGit [https://code.google.com/p/tortoisegit/downloads/list](https://code.google.com/p/tortoisegit/downloads/list)

在使用之前建议先大体了解一下git的相关基础：

## 如果学习使用并测试项目，请使用 [Webtest](https://github.com/webframe/webtest) 来测试学习。
不要用正在线运营的项目

Git详解教程列表：
---------------
* [Git详解之一 Git起步](http://www.tcreator.info/webSchool/tools/git-1-getstart.html)
* [Git详解之二 Git基础](http://www.tcreator.info/webSchool/tools/git-2-base.html)
* [Git详解之三 Git分支](http://www.tcreator.info/webSchool/tools/git-3-branch.html)
* [Git详解之四 服务器上的Git](http://www.tcreator.info/webSchool/tools/git-4-on-server.html)
* [Git详解之五 分布式Git](http://www.tcreator.info/webSchool/tools/git-5-distributed.html)
* [Git详解之六 Git工具](http://www.tcreator.info/webSchool/tools/git-6-tool.html)
* [Git详解之七 自定义](http://www.tcreator.info/webSchool/tools/git-7-custom.html)
* [Git详解之八 Git与其他系统](http://www.tcreator.info/webSchool/tools/git-8-git-and-other-system.html)
* [Git详解之九 Git内部原理](http://www.tcreator.info/webSchool/tools/git-9-internal-principle.html)


其他更多Git教程及疑问请看[Git教程列表](http://www.tcreator.info/tags.php?/GIT/)。

# Git与github操作指南

## Git命令行模式与github网站关联 

使用ssh加密实现与github网站的关联，避免每次同步都需要填写帐户密码，首次产生一个ssh key：

<pre>
cd ~/.ssh 

// 如果没有.ssh目录，则自己新建此目录即可，如下
// cd ~/
// mkdir .ssh
// cd .ssh

ssh-keygen -t rsa  //直接 N 次回车即可，默认名为id_rsa，不用修改即可
#
</pre>

设置关联（复制上面产生的key——id_rsa.pub中代码——全选即可）
在github网站setting中找到Add SSH Keys，添加复制的内容即可。

如此即关联完毕，如此在之后与github网站的push、pull操作则不用再输入github帐户密码了，非常方便。

下面提供一些命令行中常用的文件/文件夹操作命令：
<pre>
创建：mkdir .ssh
修改：mv .ssb .ssh
删除：rm -rf .ssh
创建文件：touch README.md
输出文本：cat id_rsa
</pre>

### 首次使用需要的一些配置设置

第一次使用git，一般需要设置全局config，如下：

<pre>
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
</pre>

第一次使用git push时，会提示设置git config --global push.default 将其设置为simple就行了，如下：

<pre>
git config --global push.default simple  //你可以直接如此设置，不必等操作遇到才设置
</pre>

以上配置完毕，就可以clone一个远程项目了，下面会给出一个完整详细的git项目操作示例，在文末还会将命令行示例中的常用命令做一汇总列表，方便查阅参考。

## GIt命令行模式操作项目的详细步骤示例(此处以[Git测试项目](https://github.com/pandoraui/webtest)为例详解）

为了方便练习，确保有各种的权限操作，你可以fork一个[git测试项目webtest](https://github.com/pandoraui/useGit)，之后操作的时候把路径换成自己的就行了。

首先把项目克隆到本地（注意要选择项目目录，别clone到之前的.ssh目录下了)
<pre>
//在项目目录右键选择Git Bash
Jack@ALICE /E/git
$ git clone git@github.com:pandoraui/webtest.git  //(注意选择项目目录，此处我们以E:/git文件夹为例)
cd
$ cd webtest //操作需要在项目文件夹内，不然直接进行git命令操作时，会提示错误
</pre>

下面我们对内部文件进行及提交（更详细的基础操作，请参看[Git基础](http://www.tcreator.info/webSchool/tools/git-2-base.html)）

git status  //查看文件当前处于什么状态
git commit -a -m "edit intro"  //添加、修改以及合并提交
git push 推送到远程分支（github网站/Git服务器上），第一次操作新分支时，系统会提示远程没有当前testing分支，并提示操作方法新建远程分支，如下：
fatal: The current branch dev has no upstream branch.
To push the current branch and set the remote as upstream,

    git push --set-upstream origin dev


cloudyan@IT0101 /E/wamp/www/webframe/cnBootstrap (dev)
$ git push --set-upstream origin testing //把新建的本地分支推送到远程

git pull //从远程分支下拉更新（从默认的当前远程分支），直接merge合并到当前项目中
git pull git@github.com:other/useGit.git  //从其他项目链接合并更新

管理分支

git branch testing   //新建分支
git checkout testing //切换分支
git checkout master  //切换回主干

git checkout -b testing //新建分支并切换过去
相当于执行下面这两条命令：
git branch testing
git checkout testing

修改分支testing后合并到主干
git checkout master  //首先切换到主干
git merge testing    //合并分支testing

git branch --list  //查看分支，新建了分支并切换成功同时与远程分支建立了联系

合并后，testing分支完成历史使命，就可以删掉了
git branch -d testing  //此时如果此之前已经将此分支推送到了远程，那么本地分支删除，远程github网站上还是有此分支的。

如果在合并git merge testing的时候，出现了下面的错误提示
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
产生了冲突，可以git status(逻辑上说，这种问题只能由人来裁决。)

解决完冲突，执行merge添加、修改以及合并提交命令即可。
    
//本地分支删除后，下面删除远程分支testing
git push origin :testing  

如此，这些命令能满足最常用的git操作。

# 图形化软件TortoiseGit与github网站关联 

如果你不喜欢Git命令行，那么你可以在安装以上软件后，使用图形化软件TortoiseGit来管理，TortoiseGit 是 TortoiseSVN的Git版，它很好的实现了与windows资源管理器的融合，使用界面与TortoiseSVN 非常类似。

安装好 [TortoiseGit](https://code.google.com/p/tortoisegit/downloads/list) (有中文包的) 后，需要如下操作，但首先你要了解一点：

TortoiseGit 使用扩展名为ppk的密钥，而不是ssh-keygen生成的rsa密钥。也就是说使用ssh-keygen -C "username@email.com" -t rsa产生的密钥在TortoiseGit中不能用。而基于github的开发必须要用到rsa密钥，因此需要用到TortoiseGit的putty key generator工具来生成既适用于github的rsa密钥也适用于TortoiseGit的ppk密钥。

如此，就需要在TortoiseGit中也要设置与github网站的关联。

**具体操作如下：**

运行TortoiseGit开始菜单中的puttygen程序，点击“Generate”按钮，鼠标在其软件界面中的空白地方来回移动直到进度条完毕，就会自动生一个随机的key。保存public key（此需要添加到github网站上） 和private key（此后缀为.ppk，后面要用）

在github网站上添加key操作Git key的添加，除此之外，需要右键指定具体的项目，选择TortoiseGit->Settings，设置Remote 其Putty即为上面保存的.ppk文件。麻烦之处是针对每个项目初次都要设置remote中的.ppk的路径。（参看更详细 [TortoiseGit配置说明](http://www.tcreator.info/webSchool/tools/git-TortoiseGit.html) 3.4这一段—— 建立沟通远程版本库与TortoiseGit的联系）

事实上，在clone一个新项目时，可以使用图形化界面，其中有一项便是**加载putty密钥**，选择密钥的路径即可，如
C:\Users\Jack\.ssh\pandora.ppk 如此，之后在该项目的右键settings-remote处便已经添加了密钥路径，效果同上操作。

如此之后便可以无障碍使用图形化界面上传下拉git项目了。

如有疑问可以加QQ群：187260298 咨询讨论，Good Luck ！


### 遇到错误：###

在clone一个项目后做git命令操作时，出现下面错误解决办法：

fatal: Not a git repository (or any of the parent directories): .git

**解决办法：**你得进入你的工作目录下，然后再git status 或者其它命令就没问题了。



## 新建分支并关联到远程(github网站)

如果远程已经有了分支，请使用章节（从主干下拉分支并关联分支）的命令

<pre>
cloudyan@IT0101 /E/wamp/www/webframe/cnBootstrap (master)
$ git branch dev    //新建分支
$ git checkout dev  //切换分支
$ git branch --list  //本地切换至新分支，但此时新分支并未在远程(github网站)新建
* dev
  gh-pages
  master
</pre>

如果远程没有此分子,那么当你操作push命令时,

<pre>
$ git push     // 常规操作，系统会提示远程没有当前dev分支，并提示操作方法新建远程分支
fatal: The current branch dev has no upstream branch.
To push the current branch and set the remote as upstream,

    git push --set-upstream origin testing


cloudyan@IT0101 /E/git/webtest (testing)
$ git push --set-upstream origin testing   // 设置远程分支
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:pandoraui/webtest.git
 * [new branch]      testing -> testing
Branch dev set up to track remote branch dev from origin.
</pre>

<pre>
cloudyan@IT0101 /E/git/webtest (testing)
$ git branch --list  //查看分支，新建了分支并切换成功同时与远程分支建立了联系
* testing
  master
</pre>

新建并关联成功
  
  
## 从主干下拉分支并关联分支

针对远程已经新建了分支， 在本地如何关联远程的分支

<pre>
cloudyan@IT0101 /E/git/webtest (master)
$ git fetch origin
</pre>
<pre>
cloudyan@IT0101 /E/git/webtest (master)
$ git checkout dev
Branch dev set up to track remote branch dev from origin.
Switched to a new branch 'dev'
</pre>
<pre>
cloudyan@IT0101 /E/git/webtest (testing)
$ git branch --list
* testing
  master
</pre>

关联并操作成功

这里是git命令行操作最常用的操作命令以及说明，如下：

<pre>
git status //查看修改了什么
git add .  //跟踪修改的文件.代表当前文件夹(间接代表当前目录所有文件)，也可以用指定的文件
git commit -m "简单的注释，修改了什么"  //注意git对中文的支持不太友好，暂未提供优化方法
git push   //提交到远程分支(github网站上)，如果远程没有此分支，系统会提示如何操作，命令如下：
git push --set-upstream origin proname //对应远程的项目名称proname

git pull   //从远程分支更新（从默认项目分支）
git pull git@github.com:other/useGit.git  //从其他项目分支合并更新

git branch testing   //新建分支
git checkout testing //切换分支
git checkout master  //切换回主干

git checkout -b testing //新建分支并切换过去
相当于执行下面这两条命令：
git branch testing
git checkout testing

修改分支testing后合并到主干
git checkout master  //首先切换到主干
git merge testing    //合并分支testing

合并后，testing分支完成历史使命，就可以删掉了
git branch -d testing

如果在合并git merge testing的时候，出现了下面的错误提示
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
产生了冲突，可以git status(逻辑上说，这种问题只能由人来裁决。)
</pre>

如果想新建分支等，可以参看 [Git详解之三 Git分支](http://www.tcreator.info/webSchool/tools/git-3-branch.html)

用的多了就熟练了，Git命令行确实很简单而且功能十分强悍！建议多用用命令行模式。
