# Git

https://www.liaoxuefeng.com/wiki/896043488029600/900004111093344



## git init

在需要创建git仓库的项目目录下执行命令git init

```bash
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git init
Initialized empty Git repository in /Users/cds-dn417/GolandProjects/src/quickstart/.git/
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git add readme.txt  #将文件添加到仓库中
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git commit -m "this is a readme.txt file" #-m命令用于为这次提交的文件备注
[master (root-commit) 07ce9d2] this is a readme.txt file
 Committer: CDS-DN417 <cds-dn417@CDS-DN417deMacBook-Pro.local>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 3 insertions(+)
 create mode 100644 readme.txt
```

## git log

命令git log用于版本控制

```bash
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git log
commit e31fe7140cd52dfa091052dc4c14395be84bce68 (HEAD -> master)
Author: CDS-DN417 <cds-dn417@CDS-DN417deMacBook-Pro.local>
Date:   Mon May 9 22:02:36 2022 +0800

    aka chenjianuhi

commit 07ce9d2c92983d067582445353bd96dc35e75843
Author: CDS-DN417 <cds-dn417@CDS-DN417deMacBook-Pro.local>
Date:   Mon May 9 22:00:05 2022 +0800

    this is a readme.txt file
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git log --pretty=oneline # 简化log
e31fe7140cd52dfa091052dc4c14395be84bce68 (HEAD -> master) aka chenjianuhi
07ce9d2c92983d067582445353bd96dc35e75843 this is a readme.txt file
```

## git reset 

* 命令git reset 可用于暂存区回退，也可用于对具体版本的回溯

HEAD^代表回退到上一个版本

HEAD^^代表回退到上上一个版本

```bash
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git log --pretty=oneline
e31fe7140cd52dfa091052dc4c14395be84bce68 (HEAD -> master) aka chenjianuhi
07ce9d2c92983d067582445353bd96dc35e75843 this is a readme.txt file
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git reset --hard HEAD^ #回退到上一个版本
HEAD is now at 07ce9d2 this is a readme.txt file
```

* 对具体版本的回溯

```bash
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git reset --hard e31fe #回退到版本号以e31fe开头的版本
HEAD is now at e31fe71 aka chenjianuhi
```

## git status

查看当前分支状态

```bash
ds-dn417@CDS-DN417deMacBook-Pro quickstart % git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.idea/
	conf/
	controllers/
	go.mod
	go.sum
	main.go
	quickstart
	routers/
	static/
	tests/
	views/

nothing added to commit but untracked files present (use "git add" to track)
```

## git reflog

命令git reflog用来记录每一次命令

```bash
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git reflog
e31fe71 (HEAD -> master) HEAD@{0}: reset: moving to e31fe
07ce9d2 HEAD@{1}: reset: moving to HEAD^
e31fe71 (HEAD -> master) HEAD@{2}: commit: aka chenjianuhi
07ce9d2 HEAD@{3}: commit (initial): this is a readme.txt file
```

## git diff

命令git diff用来比较当前未提交文件与已提交文件的区别

```bash
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git diff head -- readme.txt 
diff --git a/readme.txt b/readme.txt
index 936f0a9..0d7ab86 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,3 +1,4 @@
 Git is a version control system.
 This is aka chenjianhui
-aka chenjianhui
+aka cenjianhui
+aka liaoyuanbao
```

## git checkout

git checkout -- 用于放弃工作区的文件修改

git checkout [分支名] 用于切换分支

```
git checkout -- [file]
```

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

可以用git checkout -- [文件名]，将工作区已经被删掉的文件但在版本库的暂存区中存在的文件，恢复到工作区

## git rm

```bash
git rm [文件] 
```

从版本库中删除文件

# 工作区和暂存区

工作区就是指一开始git init的目录

工作区里有一个隐藏目录.git，这个是Git的版本库

版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的**暂存区**，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)

git版本库里添加的步骤

第一步：用git add把文件添加进去，实际上就是把文件添加修改到暂存区

第二步：用git commit提交更改，实际上就是把暂存区中的文件提交到当前分支

# 分支管理

git用master指向最新的提交，再用head指向master，就能够确定当前分支以及分支的提交点

git创建dev分支的底层：

1、增加一个指向dev分支的指针

2、将head指向新分支的指针

从现在开始，对工作区的修改和提交针对dev分支，比如提交一次后，dev指针往前走一步，master指针不变

合并：如果dev上的操作完成了，可以把dev合并到master上，底层方法就是把master指针指向dev指针的当前提交

git上对分支的操作实际上就是指针的操作

首先，我们创建`dev`分支，然后切换到`dev`分支：

* git checkout -b [分支名]

```bash
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git checkout -b dev
Switched to a new branch 'dev'
```

`git checkout`命令加上`-b`参数表示创建并切换，相当于以下两条命令：

```bash
$ git branch dev
$ git checkout dev
```

* git branch -d [分支名] 删分支
* git branch 查看当前分支

```bash
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git branch
* dev
  master
```

* `git merge`命令用于合并指定分支到当前分支

git merge [分支名]

* git switch [-c] [分支] 转移到该分支，如果加了-c表明创建一个新的分支，并且转移到该分支上

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

* git stash 命令用于贮藏工作区被修改的文件

```bash
cds-dn417@CDS-DN417deMacBook-Pro quickstart % git stash
Saved working directory and index state WIP on master: 36d01cf before stash
git stash list#用于查看被贮藏文件的列表
#恢复stash文件至工作区的两种方式
#方式一：
git stash apply # 恢复stash，但是不清楚stash内容
git stash drop # 将stash内容彻底删除
#方式二：
git stash pop # 恢复的同时把stash内容删除

#精准恢复stash中的文件
git stash apply stash@{0}
#将某一特定的提交精准的复制到当前分支
cherry-pick命令，让我们能复制一个特定的提交到当前分支
git cherry-pick 4c805e2 #4c805e2是版本号
```

一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；

另一种方式是用`git stash pop`，恢复的同时把stash内容也删了：

> 如何修复bug？git上的流程？

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

> 如何增加新功能？git上的流程？

每添加一个新功能，最好新建一个feature分支，开发完成并且合并之后，最后删除feature分支

# 推送分支

## git push

git push [接收分支名] [待传送分支名]

> 分支是否需要推送到远程？

* `master`分支是主分支，因此要时刻与远程同步；
* `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
* bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
* feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

## git pull

把最新的提交从远程抓取下来

先把最新的提交从远程pull下来，然后在本地merge，解决冲突，然后再push推送

## 多人协作工作模式

因此，多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`

## git rebase

变基操作

如果git log -graph的线很复杂，可以使用git rebase来简化

把分叉的提交历史“整理”成一条直线，看上去更直观。

缺点是本地的分叉提交已经被修改过了。



# 标签管理

## git tag

首先，切换到需要打标签的分支上，然后设置标签

```bash
git tag [标签名]
```

如果忘记打标签，可以在commit id，然后打上标签就可以

```bash
git log --pretty=oneline --abbrev-commit # 查找commit id
git tag [标签名] [commit id] # 根据对应的id设置标签,标签名不区分大小写
git show <tagname> # 展示标签，标签排序按照字母顺序不按照时间顺序
git tag -a v0.1 -m "version 0.1 released" 1094adb #还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字
git tag -d v0.1 # 删除标签v0.1，创建的标签都只存储在本地，不会自动推送到远程
git push origin --tags # 一次性把本地的所有标签都推到远程
#如果标签已经被推到远程，如果要删除，需要先把本地的删除，再删除远程的
git tag -d v0.9 # 删除本地
git push origin :refs/tags/v0.9 # 删除远程
```

标签和每个commit有关，如果同一个commit既出现在dev也出现在master，则两边查看标签都能查看得到