## git

### git简介
**创建版本库**
什么是版本库呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。
第一步：
创建一个文件夹
第二步：通过git init命令把这个目录变成Git可以管理的仓库
```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。删除.git文件夹就相当于丢弃git版本库

如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见。


**将文件提交到版本库的步骤：**
第一步：
提交到暂存区

> $ git add readme.txt

第二部：
把文件提交到仓库

-m是提交时的描述，我们每次提交最好都要有-m标记提交文件的内容，方便查找

>$ git commit -m "wrote a readme file"


### 对git版本库的回退操作

**查看仓库当前的状态**

>$ git status

git status命令可以让我们时刻掌握仓库当前的状态,告诉我们什么文件被修改了，需要保存

而且我们可以运用：git diff 查看修改的查看具体修改的内容

>git diff

**版本回退**

版本控制系统肯定有某个命令可以告诉我们历史记录，在Git中，我们用git log命令查看：
git log命令显示从最近到最远的提交日志

>$ git log

当历史记录非常多的时候，可以试试加上--pretty=oneline参数

>$ git log --pretty=oneline  

我们看到记录中一长串的字母和记录是版本库的版本号，我们可以根据版本号恢复版本库

在历史记录中的HEAD代表着当前版本库的版本号，HEAD^指的是上个版本库版本号，HEAD相当于一个指针指向当前版本库的版本号

**回退到上一个版本**

>$ git reset --hard HEAD^

**查看你所有的操作记录**

Git提供了一个命令git reflog用来记录你的每一次命令：

>$ git reflog

当你因为回退到某一个版本但是不是你想要的，你需要回退到最新版本但是没有版本号记录，你可以采用git reflog

 ### 版本库的概念

 工作区、暂存区和版本库（Repository）

 git add 是把文件提交给版本库的暂存区
 git commit 实际上就是把暂存区的所有内容提交到当前分支，将版本库的HEAD指针指向这个版本
 ![](/img/git工作区暂存区和版本库.jpg)

 ### 撤销版本库的修改

 git checkout -- file(必须是文件夹名)可以丢弃工作区的修改：

 >$ git checkout -- readme.txt

 一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

用命令git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区：

>$ git reset HEAD readme.txt

**删除文件**

你手动还是用命令删除了一个文件，并保存到版本库中，但是你删除错误你可以使用git checkout -- <file> 来恢复：

>$ git checkout -- test.txt

### 远程仓库

**创建ssh钥匙**
第1步：创建SSH Key。

>$ ssh-keygen -t rsa -C "youremail@example.com"

创建成功，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，id_rsa.pub是公钥

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容。

**添加远程库**
远程库的名字就是origin

把本地库的所有内容推送到远程库上

>$ git push -u origin master

把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。

由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

SSH警告
当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了

**从远程库克隆**

>$ git clone git@github.com:michaelliao/gitskills.git

### 分支管理

**创建与合并分支**

在版本回退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。当用git checkout创建一个分支是HEAD指向创建的分支

Git鼓励大量使用分支：

查看分支：git branch

创建分支：git branch <name>

当我们创建新的分支，例如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上

切换分支：git checkout <name>或者git switch <name>

创建+切换分支：git checkout -b <name>或者git switch -c <name>

合并某分支到当前分支：git merge <name>

最简单的方法，就是直接把master指向dev的当前提交，就完成了合并

删除分支：git branch -d <name>

**解决冲突**

我们在master创建一个分支demo但我们完成demo分支的工作时，提交分支，切换为master分支，如果这时master主分支文件发生改变，合并demo分支就会报错合并冲突，这时我们需要保存和提交主分支的改变（也可以手动修复冲突文件），master主分支就会比分支高一个版本，然后合并分支。

我们使用合并的git命令：

>$ git merge <分支名>

用git log --graph命令可以看到分支合并图。

**分支管理策略**

通常，合并分支时，如果可能，Git会用Fast forward(快速合并)模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

下面我们实战一下--no-ff方式的git merge：
```
$ git merge --no-ff -m "merge with no-ff" dev
Merge made by the 'recursive' strategy.
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
```

 因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。

合并后，我们用git log看看分支历史：


```
$ git log --graph --pretty=oneline --abbrev-commit
*   e1e9c68 (HEAD -> master) merge with no-ff
|\  
| * f52c633 (dev) add merge
|/  
*   cf810e4 conflict fixed
```

可以看到，不使用Fast forward模式，merge后就像这样：
![](/img/使用--no--ff合并分支.png)


**封存分支**
我们正在在一个分支上工作，突然我们别要求需要完成别的功能点或修复bug，这时我们可以封存工作区


Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作
>$ git stash

用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。

工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看：

>$ git stash list

Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：

一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

>git stash apply


另一种方式是用git stash pop，恢复的同时把stash内容也删了：
>git stash pop

**多人协作**


查看远程仓库信息
当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。

要查看远程库的信息，用git remote：
```
$ git remote
origin
```

或者，用git remote -v显示更详细的信息：
```
$ git remote -v
origin  git@github.com:michaelliao/learngit.git (fetch)
origin  git@github.com:michaelliao/learngit.git (push)
```

推送分支

推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：

>$ git push origin master

抓取分支

多人协作时，大家都会往master和dev分支上推送各自的修改。
你的小伙伴已经向origin/dev分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送：这时就会报错，合并冲突
```
$ git push origin dev
To github.com:michaelliao/learngit.git
 ! [rejected]        dev -> dev (non-fast-forward)
error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

```

推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：

```
$ git pull
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
```

git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：

```
$ git branch --set-upstream-to=origin/dev dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
```
再pull

```
$ git pull
Auto-merging env.txt
CONFLICT (add/add): Merge conflict in env.txt
Automatic merge failed; fix conflicts and then commit the result.
```

这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：

```
$ git commit -m "fix env conflict"
[dev 57c53ab] fix env conflict

$ git push origin dev
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 621 bytes | 621.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
   7a5e5dd..57c53ab  dev -> dev
```

**小结：**
查看远程库信息，使用git remote -v；

本地新建的分支如果不推送到远程，对其他人就是不可见的；

从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；

在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

**Rebase**
在上一节我们看到了，多人在同一个分支上协作时，很容易出现冲突。即使没有冲突，后push的童鞋不得不先pull，在本地合并，然后才能push成功。

每次合并再push后，分支变成了这样：
```
$ git log --graph --pretty=oneline --abbrev-commit
* d1be385 (HEAD -> master, origin/master) init hello
*   e5e69f1 Merge branch 'dev'
|\  
| *   57c53ab (origin/dev, dev) fix env conflict
| |\  
| | * 7a5e5dd add env
| * | 7bd91f1 add new env
| |/  
* |   12a631b merged bug fix 101
|\ \  
| * | 4c805e2 fix bug 101
|/ /  
* |   e1e9c68 merge with no-ff
|\ \  
| |/  
| * f52c633 add merge
|/  
*   cf810e4 conflict fixed
```

```
$ git log --graph --pretty=oneline --abbrev-commit
* 582d922 (HEAD -> master) add author
* 8875536 add comment
* d1be385 (origin/master) init hello
*   e5e69f1 Merge branch 'dev'
|\  
| *   57c53ab (origin/dev, dev) fix env conflict
| |\  
| | * 7a5e5dd add env
| * | 7bd91f1 add new env
```

注意到Git用(HEAD -> master)和(origin/master)标识出当前分支的HEAD和远程origin的位置分别是582d922 add author和d1be385 init hello，本地分支比远程分支快两个提交。

现在我们尝试推送本地分支：
```
$ git push origin master
To github.com:michaelliao/learngit.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

再多人协作时，向远程仓库提交代码时需要先pull一下

```
$ git pull
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:michaelliao/learngit
   d1be385..f005ed4  master     -> origin/master
 * [new tag]         v1.0       -> v1.0
Auto-merging hello.py
Merge made by the 'recursive' strategy.
 hello.py | 1 +
 1 file changed, 1 insertion(+)
```

加上刚才合并的提交，现在我们本地分支比远程分支超前3个提交。

用git log看看：
```
$ git log --graph --pretty=oneline --abbrev-commit
*   e0ea545 (HEAD -> master) Merge branch 'master' of github.com:michaelliao/learngit
|\  
| * f005ed4 (origin/master) set exit=1
* | 582d922 add author
* | 8875536 add comment
|/  
* d1be385 init hello
```

这个时候，rebase就派上了用场。我们输入命令git rebase试试：

```
$ git rebase
First, rewinding head to replay your work on top of it...
Applying: add comment
Using index info to reconstruct a base tree...
M	hello.py
Falling back to patching base and 3-way merge...
Auto-merging hello.py
Applying: add author
Using index info to reconstruct a base tree...
M	hello.py
Falling back to patching base and 3-way merge...
Auto-merging hello.py
```

输出了一大堆操作，到底是啥效果？再用git log看看：
```
$ git log --graph --pretty=oneline --abbrev-commit
* 7e61ed4 (HEAD -> master) add author
* 3611cfe add comment
* f005ed4 (origin/master) set exit=1
* d1be385 init hello
```

原本分叉的提交现在变成一条直线了！这种神奇的操作是怎么实现的？其实原理非常简单。我们注意观察，发现Git把我们本地的提交“挪动”了位置，放到了f005ed4 (origin/master) set exit=1之后，这样，整个提交历史就成了一条直线。rebase操作前后，最终的提交内容是一致的，但是，我们本地的commit修改内容已经变化了，它们的修改不再基于d1be385 init hello，而是基于f005ed4 (origin/master) set exit=1，但最后的提交7e61ed4内容是一致的。

这就是rebase操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。

最后，通过push操作把本地分支推送到远程:
```
Mac:~/learngit michael$ git push origin master
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 576 bytes | 576.00 KiB/s, done.
Total 6 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To github.com:michaelliao/learngit.git
f005ed4..7e61ed4  master -> master
```
### 标签管理

版本标签：发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。

**创建标签**
在Git中打标签非常简单，首先，切换到需要打标签的分支上：
```
$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'
```

然后，敲命令git tag <name>就可以打一个新标签：
>$ git tag v1.0

可以用命令git tag查看所有标签：
>$ git tag
v1.0

给之前的版本打标签：
方法是找到历史提交的commit id，然后打上就可以了：
```
$ git log --pretty=oneline --abbrev-commit
12a631b (HEAD -> master, tag: v1.0, origin/master) merged bug fix 101
4c805e2 fix bug 101
e1e9c68 merge with no-ff
f52c633 add merge
cf810e4 conflict fixed
5dc6824 & simple
14096d0 AND simple
b17d20e branch test
d46f35e remove test.txt
b84166e add test.txt
519219b git tracks changes
e43a48b understand how stage works
1094adb append GPL
e475afc add distributed
eaadf4e wrote a readme file
```
比方说要对add merge这次提交打标签，它对应的commit id是f52c633，敲入命令：
>$ git tag v0.9 f52c633

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：
>$ git tag -a v0.1 -m "version 0.1 released" 1094adb

**操作标签**
如果标签打错了，也可以删除：

>$ git tag -d v0.1
Deleted tag 'v0.1' (was f15b0dd)

因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令git push origin <tagname>：
>$ git push origin v1.0
Total 0 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
> * [new tag]         v1.0 -> v1.0

或者，一次性推送全部尚未推送到远程的本地标签：
$ git push origin --tags
Total 0 (delta 0), reused 0 (delta 0)
To github.com:michaelliao/learngit.git
> * [new tag]         v0.9 -> v0.9

删除远程标签：
如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
>$ git tag -d v0.9
Deleted tag 'v0.9' (was f52c633)

然后，从远程删除。删除命令也是push，但是格式如下：
>$ git push origin :refs/tags/v0.9
To github.com:michaelliao/learngit.git
> - [deleted]         v0.9

### 自定义git

**忽略特殊文件**

在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。
所有配置文件可以直接在线浏览：https://github.com/github/gitignore

忽略文件的原则是：

1. 忽略操作系统自动生成的文件，比如缩略图等；
2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

小结
忽略某些文件时，需要编写.gitignore；

.gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！

**配置别名**
当然还有别的命令可以简写，很多人都用co表示checkout，ci表示commit，br表示branch：

```
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
```

配置文件
配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

配置文件放哪了？每个仓库的Git配置文件都放在.git/config文件中：
```
$ cat .git/config 
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = git@github.com:michaelliao/learngit.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
[alias]
    last = log -1
```
别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。

### git图形化工具
Git有很多图形界面工具，这里我们推荐SourceTree

现在告诉你Git的官方网站：http://git-scm.com
