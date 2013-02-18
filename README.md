useGit
======

这是一个学习Git 用于测试的项目

软件安装
  Git客户端[http://code.google.com/p/msysgit/downloads/list](http://code.google.com/p/msysgit/downloads/list)

其他软件
  TortoiseGit[https://code.google.com/p/tortoisegit/downloads/list](https://code.google.com/p/tortoisegit/downloads/list)

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


与github网站关联
===============

使用ssh加密实现与github网站的关联，避免每次同步都需要填写帐户密码，首次产生一个ssh key：

<pre>
cd ~/.ssh
ssh-keygen -t rsa
#输入文件名称保存即可，比如：webcoding_rsa
</pre>

设置关联（复制上面产生的key——webcoding_rsa.pub中代码——全选即可）
在github网站setting中找到Add SSH Keys，添加复制的内容即可

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

用的多了就熟练了，git确实很简单而且功能十分强悍！

Good Luck ！
 
### 遇到错误：###

fatal: Not a git repository (or any of the parent directories): .git

**解决办法：**你得进入你的工作目录下，然后再git status 或者其它命令就没问题了。










