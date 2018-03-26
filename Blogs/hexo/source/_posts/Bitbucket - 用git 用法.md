---
title: Bitbucket - 用git 用法
date: 2018-01-03 22:22:22
tags: [Bitbucket, 分布式版本控制系统, Git]
categories: Git
---


**核心流程： 从远端中心repo那里** [Git](http://lib.csdn.net/base/git) ** clone 到本地，再在本地开发（add, commit）, 通常会利用branch管理，如果觉得code 没问题了，就push到远端的中心repo上。这里中心的repo 就是 bitbucket上的repo。**

git 之后 不需要 减号-

1. git  clone https的path

把repo下载到本地

2. git status

查看哪些文件修改了。

如果提交前，想看看具体那些文件发生变化，可以通过git-diff来查看。git diff 与 git status 区别?

3. git  add filelist 或者\* 告诉git，这些file改变了，将要commit。只是起到通知和标识的作用

相当于上传照片的时候，&quot;选中&quot;照片的功能，commit 则相当于上传

4. git commit

git commit -m &quot;   &quot;

5. git branch分支管理

在 git 版本库中创建分支的成本几乎为零，所以，不必吝啬多创建几个分支。当第一次执行git init时，系统就会创建一个名为&quot;master&quot;的分支。在bitbucket中已经创建了master分支（trunk）我们只需要clone下来即可。而其它分支则通过手工创建。下面列举一些常见的分支策略，这些策略相信会对你的日常开发带来很大的便利。

1.创建一个属于自己的个人工作分支，以避免对主分支 master 造成太多的干扰，也方便与他人交流协作。

2.当进行高风险的工作时，创建一个试验性的分支，扔掉一个烂摊子总比收拾一个烂摊子好得多。

3.合并别人的工作的时候，最好是创建一个临时的分支用来合并，合并完成后在&quot;fatch&quot;到自己的分支（合并和fatch后面有讲述，不明白就继续往下看好了）



**查看分支**  – git branch

调用git branch可以查看程序中已经存在的分支和当前分支

**创建分支**  – git branch 分支名

要创建一个分支，可以使用如下方法:

1. git branch 分支名称

2. git checkout –b 分支名

使用第一种方法，虽然创建了分支，但是不会将当前工作分支切换到新创建的分支上，因此，还需要命令&quot;git checkout 分支名&quot; 来切换， 而第二种方法不但创建了分支，还将当前工作分支切换到了该分支上。

另外，需要注意，分支名称是有可能出现重名的情况的， 比如说，我在master分支下创建了a和b两个分支，然后切换到b分支，在b分支下又创建了a和c分支。 这种操作是可以进行的。 此时的a分支和master下的a分支实际上是两个不同的分支。因此，在实际使用时，不建议这样的操作，这样会带来命名上的疑惑。

**删除分支**  – git branch -d或–D 分支名

-d 是删除，-D是强制删除

git branch –D 分支名可以删除分支，但是需要小心，删除后，发生在该分支的所有变化都无法恢复。

**切换分支**  – git checkout 分支名

如果分支已经存在， 可以通过 git checkout 分支名 来切换工作分支到该分支名

**合并分支**  – git merge

git merge的用法为：git-merge &quot;some memo&quot; 合并的目标分支 合并的来源分支。如：

如果合并有冲突，git会由提示，当前，git merge已经很少用了， 用git pull来替代了。

用法为：git pull 合并的目标分支 合并的来源分支。 如git-pull . dev1



## **分支的管理**

到目前为止，你已经学会了如何创建、合并和删除分支。除此之外，我们还需要学习如何管理分支，在日后的常规工作中会经常用到下面介绍的管理命令。

git branch 命令不仅仅能创建和删除分支，如果不加任何参数，它会给出当前所有分支的清单：

$ git branch

  iss53

\* master

  testing

注意看 master 分支前的 \* 字符：它表示当前所在的分支。也就是说，如果现在提交更新，master 分支将随着开发进度前移。若要查看各个分支最后一个提交对象的信息，运行 git branch -v：

$ git branch -v

  iss53   93b412c fix javascript issue

\* master  7a98805 Merge branch &#39;iss53&#39;

  testing 782fd34 add scott to the author list in the readmes

要从该清单中筛选出你已经（或尚未）与当前分支合并的分支，可以用 --merged 和 --no-merged 选项（Git 1.5.6 以上版本）。比如用 git branch --merged 查看哪些分支已被并入当前分支（译注：也就是说哪些分支是当前分支的直接上游。）：

$ git branch --merged

  iss53

\* master

之前我们已经合并了 iss53，所以在这里会看到它。一般来说，列表中没有 \* 的分支通常都可以用 git branch -d 来删掉。原因很简单，既然已经把它们所包含的工作整合到了其他分支，删掉也不会损失什么。

另外可以用 git branch --no-merged 查看尚未合并的工作：

$ git branch --no-merged

  testing

它会显示还未合并进来的分支。由于这些分支中还包含着尚未合并进来的工作成果，所以简单地用 git branch -d 删除该分支会提示错误，因为那样做会丢失数据：

$ git branch -d testing

error: The branch &#39;testing&#39; is not fully merged.

If you are sure you want to delete it, run &#39;git branch -D testing&#39;.

不过，如果你确实想要删除该分支上的改动，可以用大写的删除选项 -D 强制执行，就像上面提示信息中给出的那样。

与远程sever操作！！ clone pull push

2.7 远程获取一个git库 git-clone

在2.1节提到过，如果你不是一个代码模块的发起者，也不会使用到git-init命令，而是更多的是使用git-clone。通过这个命令，你可以从远端完整获取一个git库，并可以通过一些命令和远端的git交互。

基于git的代码管理的组织结构，往往形成一个树状结构，开发者一般从某个代码模块的管理者的git库通过git-clone取得开发环境，在本地迭代开发后，再提交给该模块的管理者，该模块的管理者检查这些提交并将代码合并到自己的库中，并向更高一级的代码管理者提交自己的模块代码。

git-clone的使用方法如下： git-clone [ssh://]username@ipaddr:path。 其中， &quot;ssh://&quot;可选，也有别的获取方式，如rsync。 Path是远端git的根路径，也叫repository。

通过git-clone获取远端git库后，.git/config中的开发者信息不会被一起clone过来。仍然需要为.git/config文件添加开发者信息。此外，开发者还需要自己添加. gitignore文件

另外，通过git-clone获取的远端git库，只包含了远端git库的当前工作分支。如果想获取其它分支信息，需要使用&quot;git-branch –r&quot; 来查看， 如果需要将远程的其它分支代码也获取过来，可以使用命令&quot; git checkout -b 本地分支名远程分支名&quot;，其中，远程分支名为git-branch –r所列出的分支名， 一般是诸如&quot;origin/分支名&quot;的样子。如果本地分支名已经存在，则不需要&quot;-b&quot;参数。

2.8 从远程获取一个git分支 – git-pull

与git-clone不同， git-pull可以从任意一个git库获取某个分支的内容。用法如下：

git-pull username@ipaddr: 远端repository名 远端分支名:本地分支名。这条命令将从远端git库的远端分支名获取到本地git库的一个本地分支中。其中，如果不写本地分支名，则默认pull到本地当前分支。

需要注意的是，git-pull也可以用来合并分支。 和git-merge的作用相同。 因此，如果你的本地分支已经有内容，则git-pull会合并这些文件，如果有冲突会报警。

2.9 将本地分支内容提交到远端分支 – git-push

git-push和git-pull正好想反，是将本地某个分支的内容提交到远端某个分支上。用法：

git-push username@ipaddr: 远端repository名 本地分支名:远端分支名。这条命令将本地git库的一个本地分支push到远端git库的远端分支名中。

需要格外注意的是，git-push好像不会自动合并文件。这点我的试验表明是这样，但我不能确认是否是我用错了。因此，如果git-push时，发生了冲突，就会被后push的文件内容强行覆盖，而且没有什么提示。 这在合作开发时是很危险的事情。

2.10 库的逆转与恢复 – git-reset

库的逆转与恢复除了用来进行一些废弃的研发代码的重置外，还有一个重要的作用。比如我们从远程clone了一个代码库，在本地开发后，准备提交回远程。但是本地代码库在开发时，有功能性的commit，也有出于备份目的的commit等等。总之，commit的日志中有大量无用log，我们并不想把这些 log在提交回远程时也提交到库中。 因此，就要用到git-reset。

Git-reset的概念比较复杂。它的命令形式：git-reset [--mixed | --soft | --hard] [&lt;commit-ish&gt;]

命令的选项：

--mixed

这个是默认的选项。 如git-reset [--mixed] dev1^(dev1^的定义可以参见2.6.5)。它的作用仅是重置分支状态到dev1^, 但是却不改变任何工作文件的内容。即，从dev1^到dev1的所有文件变化都保留了，但是dev1^到dev1之间的所有commit日志都被清除了，而且，发生变化的文件内容也没有通过git-add标识，如果您要重新commit，还需要对变化的文件做一次git-add。这样，commit后，就得到了一份非常干净的提交记录。

--soft

相当于做了git-reset –mixed，后，又对变化的文件做了git-add。如果用了该选项， 就可以直接commit了。

--hard

这个命令就会导致所有信息的回退， 包括文件内容。 一般只有在重置废弃代码时，才用它。 执行后，文件内容也无法恢复回来了。

3. 基于git的合作开发

对于酷讯来说，当我们采用了Git，如何进行合作开发呢？ 具体步骤如下：

3.1 获取最新代码

酷讯会准备一个中心git代码库。首先，我们将整理好的代码分模块在git中心库中建立git库。并将文件add到中心库中。 接下来，开发者通过git-clone将代码从中心库clone到本地开发环境。
对于较大的项目，我们还建议每个组选择一个负责人，由这个负责人负责从中心库获取和更新最新的代码，其它开发者从这个负责人的git代码库中clone代码。此时，对开发者来说，这个负责人的git库就是中心库了。

3.2 和中心库进行代码合并

使用过CVS的人都知道， 在commit之前，都要做一次cvs update，以避免和中心库冲突。Git也是如此。

现在我们已经经过了code review， 准备向中心库提交变化了， 在开发的这段时间，也许中心库发生了变化，因此，我们需要在向中心库提交前，再次将中心库的master分支git-pull到本地的master分支上。并且和dev分支做合并。最终，将合并的代码放入master分支。

如果开发过程提交日志过多，可以考虑参照2.10节的介绍做一次git-reset。

此外，如果发现合并过程变化非常多， 出于代码质量考虑，建议再做一次code review

3.3提交代码到中心库

此时，已经完全准备好提交最终的代码了。 通过git-push就可以了。

3.4合作流程总结

大家可以看到，使用git进行合作开发，这一过程和CVS有很多相似性，同时，增强了以下几个环节：

1. 开发者在本地进行迭代开发，可以经常的做commit操作且不会影响他人。 而且即使不在线也可以进行开发。只需要最后向中心库提交一次即可。

2. 大家都知道，如果CVS管理代码，由于我们会常常做commit操作。但是在commit之前cvs update时常会遇到将中心库上的其它最新代码checkout下来的情况，此时，一旦出现问题，就很难确认到底是自己开发的bug还是其它用户的代码带来了影响。 而使用git则避免了用户间的开发互相影响。

3. 更有利于在代码提交前做code review。以往用cvs， 都是代码提交后才做code view。如果发生问题， 也无法避免服务器上有不好的代码。 但是用git，真正向中心库commit前，都是在本地开发，可以方便的进行code review， 然后才提交到中心库。更有利于代码质量。而且，大家应该可以感到，使用git的过程中，更容易对代码进行code review，因为影响因素更小。

4. 创建多分支，更容易在开发中进行多种工作，而使工作间不会互相影响。 比如user2对user1的代码进行code review时，就可以非常方便的保留当时的开发现场，并切换到user1的代码分支，在code review完毕后，也可以非常方便的切换会曾经被中断的工作现场。

诚然，带来这些好处的同时，确实也使得操作比CVS复杂了一些。但我们觉得和前面所能获得的好处相比，这些麻烦是值得的。 当大家用惯了之后会发现，这并不增加多大的复杂性， 而且开发流程会更加自然。