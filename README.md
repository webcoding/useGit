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


# Git命令行与github网站关联 


使用ssh加密实现与github网站的关联，避免每次同步都需要填写帐户密码，首次产生一个ssh key：

<pre>
cd ~/.ssh
ssh-keygen -t rsa
#直接N次回车即可，默认为id_rsa）
</pre>

如果没有.ssh目录，则自己新建一个目录即可:
<pre>
cd ~/
mkdir .ssh
cd .ssh
</pre>

设置关联（复制上面产生的key——id_rsa.pub中代码——全选即可）
在github网站setting中找到Add SSH Keys，添加复制的内容即可。

下面提供一些常用的文件/文件夹操作的命令：
<pre>
创建：mkdir .ssh
修改：mv .ssb .ssh
删除：rm -rf .ssh
创建文件：touch README.md
输出文本：cat id_rsa
</pre>

如此即关联完毕。

第一次使用需要设置全局config，一般设置下面的即可：

<pre>
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
</pre>

新版本在使用git push时，会提示设置git config --global push.default 
将其设置为simple就行了，如下：

<pre>
git config --global push.default simple
</pre>

以上配置完毕，就可以clone一个远程项目了，如下：(注意选择项目目录，别clone到.ssh目录下了)

<pre>
git clone git@github.com:webcoding/useGit.git
</pre>

之后就可以修改项目文件，提交上传了。修改文件后可以操作如下命令：

<pre>
git status //查看修改了什么
git add .  //跟踪修改的文件.代表当前文件夹(间接代表当前目录所有文件)，也可以用指定的文件
git commit -m "简单的注释，修改了什么"  //注意git对中文的支持不太友好，暂未提供优化方法
git push   //提交到远程分支(github网站上)

git pull   //从远程分支更新
</pre>

如果想新建分支等，可以参看 [Git详解之三 Git分支](http://www.tcreator.info/webSchool/tools/git-3-branch.html)

用的多了就熟练了，Git命令行确实很简单而且功能十分强悍！建议多用用命令行模式。

# 图形化软件TortoiseGit与github网站关联 

如果你不喜欢Git命令行，那么你可以使用图形化软件TortoiseGit来管理，TortoiseGit 是 TortoiseSVN的Git版，它很好的实现了与windows资源管理器的融合，使用界面与TortoiseSVN非常类似。

安装好 [TortoiseGit](https://code.google.com/p/tortoisegit/downloads/list) (有中文包的) 后，需要如下操作，但首先你要了解一点：

TortoiseGit 使用扩展名为ppk的密钥，而不是ssh-keygen生成的rsa密钥。也就是说使用ssh-keygen -C "username@email.com" -t rsa产生的密钥在TortoiseGit中不能用。而基于github的开发必须要用到rsa密钥，因此需要用到TortoiseGit的putty key generator工具来生成既适用于github的rsa密钥也适用于TortoiseGit的ppk密钥。

**具体操作如下：**

运行TortoiseGit开始菜单中的puttygen程序，点击“Generate”按钮，鼠标在上图的空白地方来回移动直到进度条完毕，就会自动生一个随机的key。保存public key（此需要添加到github网站上） 和private key（此后缀为.ppk，后面要用）

设置关联同上Git的关联，除此之外，需要右键指定的项目，选择TortoiseGit->Settings，设置Remote 其Putty即为上面保存的.ppk文件。麻烦之处是针对每个项目初次都要设置remote中的.ppk的路径。（参看更详细 [TortoiseGit配置说明](http://www.tcreator.info/webSchool/tools/git-TortoiseGit.html) 3.4这一段—— 建立沟通远程版本库与TortoiseGit的联系）

如此便操作完毕，可以无障碍使用了。

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
<pre>
cloudyan@IT0101 /E/wamp/www/webframe/cnBootstrap (dev)
$ git push     // 常规操作，系统会提示远程没有当前dev分支，并提示操作方法新建远程分支
fatal: The current branch dev has no upstream branch.
To push the current branch and set the remote as upstream,

    git push --set-upstream origin dev


cloudyan@IT0101 /E/wamp/www/webframe/cnBootstrap (dev)
$ git push --set-upstream origin dev   // 设置远程分支
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:webframe/cnBootstrap.git
 * [new branch]      dev -> dev
Branch dev set up to track remote branch dev from origin.
</pre>
<pre>
cloudyan@IT0101 /E/wamp/www/webframe/cnBootstrap (dev)
$ git branch --list  //查看分支，新建了分支并切换成功同时与远程分支建立了联系
* dev
  gh-pages
</pre>

新建并关联成功
  
  
## 从主干下拉分支并关联分支

针对远程已经新建了分支， 在本地如何关联远程的分支

<pre>
cloudyan@IT0101 /E/wamp/www/webframe/cnBootstrap (master)
$ git fetch origin
</pre>
<pre>
cloudyan@IT0101 /E/wamp/www/webframe/cnBootstrap (master)
$ git checkout dev
Branch dev set up to track remote branch dev from origin.
Switched to a new branch 'dev'
</pre>
<pre>
cloudyan@IT0101 /E/wamp/www/webframe/cnBootstrap (dev)
$ git branch --list
* dev
  master
</pre>

关联并操作成功
