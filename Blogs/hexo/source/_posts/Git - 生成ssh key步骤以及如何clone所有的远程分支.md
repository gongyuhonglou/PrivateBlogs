---
title: Git - 生成ssh key步骤以及如何clone所有的远程分支
date: 2018-01-02 22:22:22
tags: [分布式版本控制系统, Git]
categories: Git
---


这里以配置github的ssh key为例：

### **1.**  **配置**** git ****用**** 户 ****名和**** 邮 ****箱**

设置Git的user name和email：

$ git config --global user.name &quot;用户名&quot;

$ git config --global user.email &quot;邮箱&quot;

在config后加上 --global 即可全局设置用户名和邮箱。

### **2.**  **生成**** ssh key**

生成密钥：

$ ssh-keygen -t rsa -C &quot;邮箱&quot;
按3个回车，密码为空。

然后根据提示连续回车即可在~/.ssh目录下得到id\_rsa和id\_rsa.pub两个文件，id\_rsa.pub文件里存放的就是我们要使用的key。

### **3.**  **上**** 传 ****key**** 到 ****github**

clip &lt; ~/.ssh/id\_rsa.pub

1. 复制key到剪贴板

- 登录github
- 点击右上方的Accounting settings图标
- 选择 SSH key
- 点击 Add SSH key

### **4.**  **测试是否配置成**** 功**

ssh -T

git@github.com

如果配置成功，则会显示： Hi username! You&#39;ve successfully authenticated, but GitHub does not provide shell access.

### ** **** 开始使用 ****github**

### **1.**** 获取源码 ****：**

$ git clone ssh://git@bitbucket.yuneec.com.git

2.这样你的机器上就有一个repo了。
3.git于svn所不同的是git是分布式的，没有服务器概念。所有的人的机器上都有一个repo，每次提交都是给自己机器的repo
仓库初始化：

git init

生成快照并存入项目索引：

git add .

文件,还有git rm,git mv等等…
项目索引提交：

git commit -m &quot;说明&quot;

4.协作编程：
将本地repo于远程的origin的repo合并，
推送本地更新到远程：

git push origin master

更新远程更新到本地：

git pull origin master

补充：
添加远端repo：

$ git remote add upstream git://github.com/pjhyett/github-services.git

重命名远端repo：

$ git://github.com/pjhyett/github-services.git为&quot;upstream&quot;



## **解决本地多个**** ssh key ****问题**

有的时候，不仅github使用ssh key，工作项目或者其他云平台可能也需要使用ssh key来认证，如果每次都覆盖了原来的id\_rsa

文件，那么之前的认证就会失效。这个问题我们可以通过在~/.ssh目录下增加config文件来解决。

下面以配置搜狐云平台的ssh key为例。

### **1.**  **第一步依然是配置**** git ****用**** 户 ****名和**** 邮 ****箱**

git config user.name

&quot;用户名&quot;git config user.email &quot;邮箱&quot;

### **2.**  **生成**** ssh key ****时同时指定保存的文件**** 名**

ssh-keygen

-t rsa -f ~/.ssh/id\_rsa.sohu -C &quot;email&quot;

上面的id\_rsa.sohu

就是我们指定的文件名，这时~/.ssh目录下会多出id\_rsa.sohu和id\_rsa.sohu.pub两个文件，id\_rsa.sohu.pub里保存的就是我们要使用的key。

### **3.**  **新增并配置**** config**

文件

#### **添加**** config**

文件

如果config

文件不存在，先添加；存在则直接修改

touch ~/.ssh/config

#### **在**** config**

文件里添加如下内容(User表示你的用户名)

Host \*.cloudscape

.sohu

.com

IdentityFile ~/.ssh/id\_rsa.sohu User test

### **4.**  **上**** 传 ****key**** 到云平台后台****(****省略****)**

### **5.**  **测试**** ssh key ****是否配置成功**

ssh -T git@git.cloudscape

.sohu

.com

成功的话会显示：

Welcome to

GitLab, username!

至此，本地便成功配置多个ssh key。日后如需添加，则安装上述配置生成key，并修改config文件即可。



### **6.**** 如何 ****clone**** 所有的 ****远**** 程分支**

更新远程分支到本地： git fetch -p

                              git branch -a

git一般有很多分支，我们clone到本地的时候一般都是master分支，那么如何切换到其他分支呢？主要命令如下：

**1. 查看远程分支**

$ git branch -a
我在mxnet根目录下运行以上命令：

~/mxnet$ git branch -a

\* master

  remotes/origin/HEAD -&gt; origin/master

  remotes/origin/master

  remotes/origin/nnvm

  remotes/origin/piiswrong-patch-1

  remotes/origin/v0.9rc1

可以看到，我们现在在master分支下

**2. 查看本地分支**

~/mxnet$ git branch

\* master

**3. 切换分支**

$ git checkout -b v0.9rc1 origin/v0.9rc1

Branch v0.9rc1 set up to track remote branch v0.9rc1 from origin.

Switched to a new branch &#39;v0.9rc1&#39;

＃已经切换到v0.9rc1分支了

$ git branch

  master

\* v0.9rc1

＃切换回master分支

$ git checkout master

Switched to branch &#39;master&#39;

Your branch is up-to-date with &#39;origin/master&#39;.

解决：（1）

首先，你需要使用$ git clone这个命令克隆一个本地库。
之后它会自动克隆一个master分支（这个貌似是必须的）。
之后不会克隆任何一个分支下来的。
假定你需要一个dev（此处假定远程库中已经存在此分支，也就是你需要克隆的）分支用于开发的话，你需要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是用这个命令创建本地dev分支：
$ git checkout -b dev origin/dev

再同步下：
$ git pull

这样就实现了克隆dev分支。
————————————————————————————



解决：（2）

[Git](http://lib.csdn.net/base/git) clone只能clone远程库的master分支，无法clone所有分支，解决办法如下：

1. 找一个干净目录，假设是git\_work
2. cd git\_work
3. git clone http://myrepo.xxx.com/project/.git ,这样在git\_work目录下得到一个project子目录
4. cd project
5. git branch -a，列出所有分支名称如下：
remotes/origin/dev
remotes/origin/release
6. git checkout -b dev origin/dev，作用是checkout远程的dev分支，在本地起名为dev分支，并切换到本地的dev分支
7. git checkout -b release origin/release，作用参见上一步解释
8. git checkout dev，切换回dev分支，并开始开发。