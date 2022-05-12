# Git 项目中常用操作及常规项目版本开发流程简介
[toc]
## Part1 Git简介
### 写在前面
#### **1. 什么是版本控制**
>+ **简介: 
    版本控制系统（Version Control System，简称VCS）是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统.**
>
>+ **作用: 
    版本控制最主要的功能就是追踪文件的变更。它将什么时候、什么人更改了文件的什么内容等信息记录下来。每一次文件的改变，文件的版本号都将增加。除了记录版本变更外，版本控制的另一个重要功能是并行开发。软件开发往往是多人协同作业，版本控制可以有效地解决版本的同步以及不同开发者之间的开发通信问题，提高协同开发的效率。并行开发中最常见的不同版本软件的错误(Bug)修正问题也可以通过版本控制中分支与合并的方法有效地解决.**

#### **2. 集中式版本控制**
> + **集中式版本控制的版本库集中存放在中央服务器，而实际工作用的是自己电脑，所以要先从中央服务器取得最新的版本，然后才能工作干.工作完成，再把工作内容推送到中央服务器.**
> + **集中式版本控制系统最大缺点就是必须联网才能工作，如果在局域网内还好，带宽够大，速度够快，可如果在互联网上，遇到网速慢的话，可能提交一个10M的文件就需要5分钟。低效。**
> 
<img src="./media/集中式1.png" alt="Git常规流程" style="zoom:50%;" />


#### **3. 分布式版本控制**
> + **分布式版本控制系统没有“中央服务器”，每个人的电脑上都有一个完整的版本库，这样，工作的时候，就不需要联网，因为版本库就在自己电脑上。**
> + **多人协作: 你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改**
> 
>
>+ **和集中式版本控制系统相比，分布式版本控制系统的安全性高:因为每个人电脑里都有完整的版本库，某一个人电脑故障，可从其它电脑复制一份。而集中式版本控制系统的中央服务器出问题，所有人都将无法获得版本更新。**
> + **实际使用分布式版本控制系统，很少在两人之间电脑上直接推送版本修改，因为可能相互间不在一个局域网内，互相访问不了,或电脑故障无法开机。因此，分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但仅仅用来方便“交换”修改，没有中央服务器，仍可继续提交版本,只是相互间交换修改不方便而已。**

<img src="./media/分布式1.png" alt="Git常规流程" style="zoom:50%;" />

### Git是什么
**Git是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。可以有效、高速的处理从很小到非常大的项目版本管理。Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。**

### Git特点
> **1.速度快、灵活、离线工作**
> **2.适合分布式开发，强调个体**
> **3.允许上千个并行开发的分支**
> **4. 公共服务器压力和数据量都不会太大**
> **5. 任意两个开发者之间可以很容易的解决冲突**
> **6. 能高效管理类似`Linux`内核一样的超大规模项目**

### Git与Svn的区别
> - **SVN是集中式版本控制系统，Git是分布式版本控制系统**
> - **Git保存的不是文件的变化或者差异，而是一系列不同时刻的文件快照**
> - **Git没有一个全局的版本号，而SVN有：目前为止这是跟SVN相比GIT缺少的最大的一个特征。**
> - **分支在SVN中是一个完整的目录，且目录拥有完整的实际文件.Git分支本质上仅仅是指向提交对象的可变指针**
> - **Git的内容完整性要优于SVN：Git的内容存储使用的是SHA-1哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏**

### Git工作流程
> **常规工作流程:**
> **1. 从远程仓库中克隆 Git 资源作为本地仓库.`git clone <url>`**
> **2. 从本地仓库中checkout代码然后进行代码修改.`git checkout <分支名>`**
> **3. 将工作区的代码提交(add)到暂存区.命令`git add <file>...`**
> **4. 将修改提交(commit)到本地仓库的当前分支;本地仓库中保存各个历史版本的修改.命令`git commit -m comment [file]...`**
> **5. 在需要和团队成员共享代码时,将提交的代码push到远程仓库.`git push`**

<img src="./media/流程1.png" alt="Git常规流程" style="zoom:50%;" />

### Git的几个核心概念
> **工作区、暂存区、版本库、远程仓库**
>> + **Workspace： 工作区，实际操作/存放项目代码的地方**
>> + **Remote： 远程仓库，托管代码的服务器，用作项目组成员间数据交换**
>> + **Repository： 本地仓库区（或本地版本库），本地存放数据的位置，保存提交的所有版本数据**
>> + **Index/Stage： 暂存区,用于临时存放文件的改动.事实上它只是一个文件，保存改动的文件、即将提交的文件列表信息**

<img src="./media/集中式2.png" alt="Git常规流程" style="zoom:50%;" />

> **分支**

> + **每次提交Git都把它们串成一条时间线，这条时间线就是一个分支。所有版本控制项目，都有一条分支，在Git里这个分支叫主分支，即master分支。**
> **Git中,HEAD符指向分支名,如master，分支名(eg.master)指向某一次的提交**
> 
> + **项目初始，master分支是一条线，Git用master指向最新的提交，用HEAD指向master，确定当前分支，以及当前分支的提交点：**
> + **每次提交，master分支都会向前移动一步，多次提交，master分支的线也越来越长。**

<img src="./media/master11.png" alt="Git常规流程" style="zoom:80%;" />

> + **当创建新分支，如dev时，Git新建了一个指针叫dev，指向创建时,master相同的提交,再把HEAD指向dev,表示当前分支在dev上：**

<img src="./media/master22.png" alt="Git常规流程" style="zoom:70%;" />

> + **Git创建一个分支很快: 只需增加一个dev指针，改变HEAD指向，无需操作工作区的文件！**
> + **不过切换到dev分支，对工作区修改和提交就是针对dev分支了，如新提交一次，dev指针就往前移一步，而master指针指向不变**

<img src="./media/master33.png" alt="Git常规流程" style="zoom:70%;" />

> + **假如在dev上的工作完成，可把dev合并到master上:最简单的方法，就是直接把master指向dev的当前提交(master无任何修改)，完成合并：**

<img src="./media/master44.png" alt="Git常规流程" style="zoom:70%;" />

> + **Git合并分支也很快! 就改下指针指向位置,工作区内容不变！合并完分支后，可以删除dev分支:把dev指针给删掉,保留master分支:**

<img src="./media/master55.png" alt="Git常规流程" style="zoom:70%;" />





## Part2 Git安装
+ ### **Linux**
> + **输入git，查看系统是否已安装Git：**
```shell
$ git
The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git
```
> **如上Git没有安装,提示如何安装Git:**
```shell
sudo apt install git
```

+ ### **Mac**
> + **如果尚未安装Git，或者已安装的Git版本过低，可以去Git官网https://git-scm.com进行安装**

<img src="./media/mac1.png" alt="Git常规流程" style="zoom:60%;" />



<img src="./media/mac2.png" alt="Git常规流程" style="zoom:60%;" />



<img src="./media/mac3.png" alt="Git常规流程" style="zoom:60%;" />

> **Homebrew安装完成后，执行brew install git即可安装最新版本Git**


<img src="./media/mac4.png" alt="Git常规流程" style="zoom:60%;" />

> **安装完成后,需配置用户信息**


<img src="./media/mac5.png" alt="Git常规流程" style="zoom:60%;" />

> **Notice:**
> **1. -–global参数，表示这台机器上的所有的git仓库都会使用这个配置，当然也可对某个仓库指定不同的用户名和邮箱，更多参数我们也可以通过git config提示查看，还可以使用git config --list或git config -l来查看已经配置的信息**


## Part3 Git常规操作流程
### 创建版本库
+ **什么是版本库** 
> **版本库又名仓库，英文名repository，可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。**

+ **创建版本库**
> + **1. 创建一个空目录**
```bash
$ mkdir learngit
$ cd learngit
$ pwd    //打印当前所处目录
/Users/hy/learngit
```

> + **2. 通过git init命令把目录变成Git可以管理的仓库**
```sh
$ git init
Initialized empty Git repository in /Users/hy/learngit/.git/
```

> **这样Git仓库就建好,且命令输出提示，所建的是一个空仓库（empty Git repository）.
> 通过 `ls -a`命令,可发现当前目录下多一个.git的目录，这个目录是Git来跟踪管理版本库的，不可手动修改这个目录里面的文件，否则容易把Git仓库破坏。**

> + **3. 文件添加到版本库**

> **在刚创建的learngit目录下,编写一个readme.txt文件，内容如下：**
```
Test: Git is a version control system.
```
> + **把文件添加到版本库**
```sh
git add readme.txt
```

> + **用命令git commit把文件提交到本地仓库：**
```sh
$ git commit -m "commit a readme file"
[master (root-commit) eaadf4e] commit a readme file
 1 file changed, 1 insertions(+)
 create mode 100644 readme.txt
```
> **-m 后面输入的是本次提交的说明，可以输入任意内容，方便从历史记录里找到改动记录**
> **git commit命令执行成功后提示，1 file changed：1个文件被改动（新添加的readme.txt文件）;1 insertions:插入了一行内容**


### 文件操作
> + **1. 修改文件内容**
```
Git is a distributed version control system.
Git is free software.
```
> 运行 `git status`命令查看结果:

<img src="./media/git2.png" alt="Git常规流程" style="zoom:60%;" />

> **git status命令可以掌握仓库当前的状态，上面的命令输出可知:**
> **1. readme.txt被修改过，但还没提交修改**
> **2. 可用 git add <file>...命令,将修改的文件提交到暂存区**
> **3. 可用git restore <file>... 丢弃工作区已做的文件修改**

> + **2. 提交到暂存区**
```sh
$ git add readme.txt
```
> **运行`git status`查看当前仓库的状态**

<img src="./media/git3.png" alt="Git常规流程" style="zoom:60%;" />

> **git status命令可知:**
> **1. readme.txt可被提交**
> **2. 可用git restore --staged <file>...命令,撤销本次文件的暂存操作**

> + **3. 提交到本地仓库**
```
git commit -m 'commit to local repository'
```
<img src="./media/git4.png" alt="Git常规流程" style="zoom:60%;" />

> **运行`git status`查看当前仓库的状态**

<img src="./media/git5.png" alt="Git常规流程" style="zoom:60%;" />

> **git status命令可知:**
> **1. 当前没有需要提交的修改，而且工作目录干净（working tree clean）**

> **Notice**
> `git reset --hard commit-id` **回退到指定的版本**

### 版本回退

> + **1. 查看版本历史记录:`git log`**

<img src="./media/git6.png" alt="Git常规流程" style="zoom:60%;" />

> **git log命令可知:**
> **1. 显示从最近到最远的提交日志,可以看到2次提交，最近的一次是commit to local repository，上一次是commit a readme file**
> **2. 一大串类似d40dd1d77...的是commit id（版本号），和SVN不一样，Git的commit id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示.因为Git是分布式的版本控制系统，多人在同一个版本库里工作，如用1，2，3……作为版本号，则产生冲突**

> + **2. 版本回退**

> **Git中，用HEAD指向当前所在版本,即最新提交d40dd1d77...，上一个版本就是HEAD\^，上上一个版本就是HEAD^^，往上100个版本可写HEAD~100**
> **回退到上一个版本:**

<img src="./media/git7.png" alt="Git常规流程" style="zoom:60%;" />

> **readme.txt的内容回退到 e0b0265...版本**

<img src="./media/git8.png" alt="Git常规流程" style="zoom:60%;" />

> **再查看版本历史记录:`git log`**

<img src="./media/git9.png" alt="Git常规流程" style="zoom:60%;" />

> **d40dd1d77...版本不再显示.可通过`git reflog`查看操作过的历史命令**

<img src="./media/git10.png" alt="Git常规流程" style="zoom:60%;" />

> **可找回回退前的版本的版本号d40dd1d77...,输入 `git reset --hard d40dd1d77`,可回到目标版本**

<img src="./media/git11.png" alt="Git常规流程" style="zoom:60%;" />

> **Git的版本回退速度非常快:HEAD指针重新指向目标版本即可,无需文件内容相关的操作**

<img src="./media/git12.png" alt="Git常规流程" style="zoom:60%;" />



### 删除文件

> **一般情况下,通常直接在文件管理器中把没用的文件删了,或者用rm命令删了：**
```sh
$ rm test.txt
```

> **这时，Git知道文件被删除，工作区和版本库就不一致，`git status`命令会输出哪些文件被删除,及撤销删除操作的命令：**

<img src="./media/git13.png" alt="Git常规流程" style="zoom:60%;" />

> **1.从版本库中删除改文件**
```sh
$ git rm readme.txt
rm 'readme.txt'

$ git add . && git commit -m "remove readme.txt"
[master d46f35e] remove readme.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
```
> **现在，文件就从版本库中被删除**

> **2.另一种情况是误删，因为版本库里存有被删的文件，所以可以把误删的文件恢复到指定版本里的文件：**
```sh
$ git restore readme.txt 
或
$ git checkout -- readme.txt
```


### 推送到远程仓库

> - **代码提交到本地仓库后,可以推送到远程仓库备份,防止因本地主机硬盘损坏,代码丢失.同时,也便于他人从远程仓库克隆/更新代码到本地主机,查看/修改代码,也允许其它开发者推送各自的代码到远程仓库,通过远程仓库协作开发,分享开发经验**

> **1.初始代码从远程仓库克隆**

> **从已有的代码仓库克隆代码到本地,更新/修改后, 暂存(`git add`)、提交(`git commit`)到本地仓库,最后需要推送到远程仓库,可用 `git push [origin] [当前分支]`推送当前分支的修改到远程仓库**


> **2.新建项目代码仓库**

> **创建本地主机的代码仓库后,需要和远程仓库创建关联,才能把本地代码推送到远程仓库备份保存,与其它人协作开发**

> + **在Gitlab/Github/阿里云等代码托管网站建立一个空仓库**

<img src="./media/github1.png" alt="Git常规流程" style="zoom:30%;" />

>---

<img src="./media/github2.png" alt="Git常规流程" style="zoom:30%;" />

> **把一个已有的本地仓库与之关联，然后通过`git remote add origin <远程仓库地址>`，把本地仓库的内容推送到远程(Eg. GitHub)仓库.Eg.:**
```sh
$ git remote add origin git@github.com:test/git_test.git // 需把远程仓库地址换成自有的仓库地址
```
> **远程库的名字是origin，是Git默认的叫法，也可以改成别的(一般不做修改)**
```sh
$ git push -u origin master
```