# Git 项目中常用操作及项目版本开发常规流程简介
[toc]
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

## Part1 Git简介
### 写在前面
#### **1. 什么是版本控制**
>+ **简介: 
    版本控制系统(Version Control System,简称VCS)是一种记录一个或若干文件内容变化,以便将来查阅特定版本修改情况的系统.**
>
>+ **作用: 
    版本控制最主要的功能就是追踪文件的变更.它将什么时候、什么人更改了文件的什么内容等信息记录下来.每一次文件的改变,文件的版本号都将增加.
    除了记录版本变更外,版本控制的另一个重要功能是并行开发.软件开发往往是多人协同作业,版本控制可以有效地解决版本的同步以及不同开发者之间的开发通信问题,提高协同开发的效率.并行开发中最常见的不同版本软件的错误(Bug)修正问题也可以通过版本控制中分支与合并的方法有效地解决.**

#### **2. 集中式版本控制**
> + **集中式版本控制的版本库集中存放在中央服务器,而实际工作用的是自己电脑,所以要先从中央服务器取得最新的版本,然后才能工作.工作完成,再把工作内容推送到中央服务器.**
> + **集中式版本控制系统最大缺点就是必须联网才能工作,如果在局域网内还好,带宽够大,速度够快,可如果在互联网上,遇到网速慢的话,可能提交一个10M的文件就需要5分钟.低效.**
> 
<img src="./media/centre.png" alt="Git常规流程" style="zoom:50%;" />


#### **3. 分布式版本控制**
> + **分布式版本控制系统没有“中央服务器”,每个人的电脑上都有一个完整的版本库,这样,工作的时候,就不需要联网,因为版本库就在自己电脑上.**
> + **多人协作: 你在自己电脑上改了文件A,你的同事也在他的电脑上改了文件A,这时,你们俩之间只需把各自的修改推送给对方,就可以互相看到对方的修改.**
> 
>
>+ **和集中式版本控制系统相比,分布式版本控制系统的安全性高:因为每个人电脑里都有完整的版本库,某一个人电脑故障,可从其它电脑复制一份.而集中式版本控制系统的中央服务器出问题,所有人都将无法获得版本更新.**
> + **实际使用分布式版本控制系统,很少在两人之间电脑上直接推送版本修改,因为可能相互间不在一个局域网内,互相访问不了,或电脑故障无法开机.因此,分布式版本控制系统通常也有一台充当“中央服务器”的电脑,但仅仅用来方便“交换”修改,没有中央服务器,仍可继续提交版本,只是相互间交换修改不方便而已.**

<img src="./media/distribute.png" alt="Git常规流程" style="zoom:35%;" />

### Git是什么
**Git是一款免费、开源的分布式版本控制系统,用于敏捷高效地处理任何或小或大的项目.可以有效、高速的处理从很小到非常大的项目版本管理.Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件.**

### Git特点
> **1.速度快、灵活、离线工作**
> **2.适合分布式开发,强调个体**
> **3.允许上千个并行开发的分支**
> **4. 公共服务器压力和数据量都不会太大**
> **5. 任意两个开发者之间可以很容易的解决冲突**
> **6. 能高效管理类似`Linux`内核一样的超大规模项目**

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

### Git与Svn的区别
> - **SVN是集中式版本控制系统,Git是分布式版本控制系统**
> - **Git保存的不是文件的变化或者差异,而是一系列不同时刻的文件快照**
> - **分支在SVN中是一个完整的目录,且目录拥有完整的实际文件.Git分支本质上仅仅是指向提交对象的可变指针**
> - **Git的内容完整性要优于SVN:Git的内容存储使用的是SHA-1哈希算法.这能确保代码内容的完整性,确保在遇到磁盘故障和网络问题时降低对版本库的破坏**
> - **分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在,没有联网也可以正常工作,当有网络的时候,Git再把本地提交推送一下就完成同步！而SVN在没有联网的时候是无法操作.**

### Git工作流程
> **常规工作流程:**
> **1. 从远程仓库中克隆 Git 资源作为本地仓库.`git clone <url>`**
> **2. 从本地仓库中创建新分支或切换到指定分支,然后进行代码修改.`git switch -c <新分知名> 或 git switch <已有分支名>`**
> **3. 将工作区的代码提交(add)到暂存区.`git add <file>...`**
> **4. 将修改提交(commit)到本地仓库的当前分支;本地仓库中保存各个历史版本的修改记录.`git commit -m 'comment' [file]...`**
> **5. 在需要和团队成员共享代码时,将提交到本地仓库的代码push到远程仓库.`git push origin <要推送的本地分支名>`**

<img src="./media/distribute2.png" alt="Git常规流程" style="zoom:50%;" />


<br/>
<br/>
<br/>
<br/>
<br>

### Git的几个核心概念
> **工作区、暂存区、版本库、远程仓库**
>> + **Workspace: 工作区,实际操作/存放项目代码的地方**
>> + **Remote: 远程仓库,托管代码的服务器,用作项目组成员间数据交换**
>> + **Repository: 本地仓库区(或本地版本库),本地存放数据的位置,保存提交的所有历史版本数据**
>> + **Index/Stage:暂存区,用于临时存放文件的改动.事实上它只是一个文件,保存改动的文件、即将提交的文件列表信息**

<img src="./media/distribute3.png" alt="Git常规流程" style="zoom:50%;" />


<br>

> **常规分支操作流程**
>> + **每次提交Git都把它们串成一条时间线,这条时间线就是一个分支.所有版本控制项目,都有一条分支,在Git里这个分支叫主分支,即master分支.**
>> **Git中,HEAD标识符指向分支名,如master,分支名指向某一次的提交**
>> 
>> + **项目初始,master分支是一条线,Git用master指向最新的提交,用HEAD指向master,确定当前分支,以及当前分支的提交点**
>> + **每次提交,master分支都会向前移动一步,多次提交,master分支的线也越来越长.**

<img src="./media/branch2.png" alt="Git常规流程" style="zoom:80%;" />

<br/>
<br/>
<br/>

> + **当创建新分支,如dev时,Git新建了一个指针叫dev,指向创建时刻master的提交,再把HEAD指向dev,表示当前分支在dev上:**

<img src="./media/branch3.png" alt="Git常规流程" style="zoom:70%;" />

> + **Git创建一个分支很快: 只需增加一个dev指针,改变HEAD指向,无需操作工作区的文件！**
> + **不过切换到dev分支后,对工作区修改和提交就是针对dev分支了,如新提交一次,dev指针就往前移一步,而master指针指向不变**

<img src="./media/branch4.png" alt="Git常规流程" style="zoom:70%;" />

> + **假如在dev上的工作完成,可把dev合并到master上:最简单的方法,就是直接把master指向dev的当前提交(即Fast-Forward合并策略),完成合并:**

<img src="./media/branch5.png" alt="Git常规流程" style="zoom:70%;" />

> + **Git合并分支很快! 只需改下指针指向位置,工作区内容不变.合并完分支后,可以删除dev分支:把dev指针给删掉,保留master分支:**

<img src="./media/branch6.png" alt="Git常规流程" style="zoom:70%;" />



<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>




## Part2 Git安装
+ ### **Linux**
> + **输入git,查看系统是否已安装Git:**
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
> + **如果尚未安装Git,或者已安装的Git版本过低,可以去Git官网https://git-scm.com进行安装**

<img src="./media/mac1.png" alt="Git常规流程" style="zoom:60%;" />

<br/>
<br/>


<img src="./media/mac2.png" alt="Git常规流程" style="zoom:60%;" />



<img src="./media/mac3.png" alt="Git常规流程" style="zoom:60%;" />

> **Homebrew安装完成后,执行brew install git即可安装最新版本Git**


<img src="./media/mac4.png" alt="Git常规流程" style="zoom:60%;" />

<br/>

> **安装完成后,需配置用户信息**


<img src="./media/mac5.png" alt="Git常规流程" style="zoom:60%;" />

<br/>

> **Notice:**
> **1. -–global参数,表示这台机器上的所有的git仓库都会使用这个配置,当然也可对某个仓库指定不同的用户名和邮箱,更多参数我们也可以通过git config提示查看,还可以使用git config --list或git config -l来查看已经配置的信息**


<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>



## Part3 Git常规操作流程
### 创建版本库
+ **什么是版本库** 
> **版本库(repository),可以简单理解成一个目录,这个目录里面的所有文件都可以被Git管理起来,每个文件的修改、删除,Git都能跟踪,以便任何时刻都可以追踪历史,或者在将来某个时刻可'还原'到某一历史版本.**

+ **创建版本库**
> + **1. 创建一个空目录**
```bash
$ mkdir learngit  // 创建learning目录
$ cd learngit // 进入learingit目录
$ pwd    // 打印当前所处目录
/Users/hy/learngit
```

> + **2. 通过git init初始化一个本地仓库:把当前目录变成Git可以管理的仓库**
```sh
$ git init
Initialized empty Git repository in /Users/hy/learngit/.git/
```

> **这样Git仓库就建好,且命令输出提示:所建的是一个空仓库(empty Git repository).
> 通过 `ls -a`命令,可发现当前目录下多一个.git的目录,这个目录是Git来跟踪管理版本库的,不可手动修改这个目录里面的文件,否则容易把Git仓库破坏.**

<img src="./media/repository1.png" alt="Git常规流程" style="zoom:60%;" />

<br>

> + **3. 文件添加到版本库**

> **在刚创建的learngit目录下,编写一个readme.txt文件,内容如下:**
```
Test: Git is a version control system.
```
> + **把文件添加到暂存区**
```sh
git add readme.txt
```

<br>


> + **用命令git commit把文件提交到本地仓库:**
```sh
$ git commit -m "commit a readme file"
[master (root-commit) eaadf4e] commit a readme file
 1 file changed, 1 insertions(+)
 create mode 100644 readme.txt
```
> **-m 后面输入的是本次提交的说明,可以输入任意内容,方便从历史记录里快速定位需要的历史版本**


> **git commit命令执行成功后提示:**
>> + **1 insertions:插入了一行内容**
>> + **1 file changed:1个文件被改动(新添加的readme.txt文件)**


### 文件操作
> + **1. 修改文件内容**
```
Git is a distributed version control system.
Git is free software.
```
> **运行 `git status`命令查看结果:**

<img src="./media/repository2.png" alt="Git常规流程" style="zoom:60%;" />

<br>

> **git status命令可以掌握仓库当前的状态,上面的命令输出可知:**
>> **1. readme.txt被修改过,但还没提交修改**
> **2. 可用 git add <file>...命令,将修改的文件提交到暂存区**
> **3. 可用git restore <file>... 丢弃工作区已做的文件修改**

> + **2. 提交到暂存区**
```sh
$ git add readme.txt
```
<br>
<br>

> **运行`git status`查看当前仓库的状态**

<img src="./media/repository3.png" alt="Git常规流程" style="zoom:60%;" />

<br>

> **git status命令可知:**
>>  **readme.txt可被提交**
>>  **可用git restore --staged <file>...命令,撤销本次文件的暂存操作**

> + **3. 提交到本地仓库**
```
git commit -m 'commit to local repository'
```
<img src="./media/repository4.png" alt="Git常规流程" style="zoom:60%;" />

<br>

> **运行`git status`查看当前仓库的状态**

<img src="./media/repository5.png" alt="Git常规流程" style="zoom:60%;" />

<br>

> **git status命令可知:**
> **1. 当前没有需要提交的修改,而且工作目录干净(working tree clean)**

### 版本回退

> + **1. 查看版本历史记录:`git log`**

<img src="./media/callback2.png" alt="Git常规流程" style="zoom:60%;" />

<br>

> **git log命令可知:**
>> **1. 显示从最近到最远的提交日志,可以看到2次提交,最近的一次是commit to local repository**
>> **2. 一大串类似42c8835a...的是commit id(版本号),和SVN不一样,Git的commit id不是1,2,3……递增的数字,而是一个SHA1计算出来的一个非常大的数字,用十六进制表示.因为Git是分布式的版本控制系统,多人在同一个版本库里工作,如用1,2,3……作为版本号,则产生冲突**

> + **2. 版本回退**

> **Git中,用HEAD指向当前所在版本,即最新提交42c8835a.....,上一个版本就是HEAD\^,上上一个版本就是HEAD^^,往上100个版本可写HEAD~100**
> **回退到上一个版本:**

<img src="./media/callback3.png" alt="Git常规流程" style="zoom:60%;" />

<br>

> **readme.txt的内容回退到 e6e140ac046...版本**

<img src="./media/callback5.png" alt="Git常规流程" style="zoom:60%;" />

<br>

> **再查看版本历史记录:`git log`**

<img src="./media/callback4.png" alt="Git常规流程" style="zoom:60%;" />

<br>

> **42c8835a...版本不再显示.可通过`git reflog`查看操作过的历史命令**

<img src="./media/callback6.png" alt="Git常规流程" style="zoom:60%;" />

<br>

> **可找回回退前的版本的版本号42c8835a...,输入 `git reset --hard 42c8835a`,可回到目标版本.这里相当于撤销刚刚回退操作.**

<img src="./media/callback7.png" alt="Git常规流程" style="zoom:60%;" />

<br>
<br>
<br>

> **Git的版本回退速度非常快:HEAD指针重新指向目标版本即可,无需涉及文件内容相关的操作**

<img src="./media/callback8.png" alt="Git常规流程" style="zoom:70%;" />

<br>

> **回退到commit_1**

<br>

<img src="./media/callback9.png" alt="Git常规流程" style="zoom:70%;" />


### 删除文件

> **一般情况下,通常直接在文件管理器中把没用的文件删除,或者用rm命令删:**
```sh
$ rm test.txt
```

> **这时,Git知道文件被删除,工作区和版本库内容不一致,`git status`命令会输出哪些文件被删除,及撤销删除操作的命令:**

<img src="./media/callback10.png" alt="Git常规流程" style="zoom:60%;" />

<br>
<br>
<br>
<br>

> **1.从版本库中删除改文件**
```sh
$ git rm readme.txt
rm 'readme.txt'

$ git add . && git commit -m "remove readme.txt"
[master d46f35e] remove readme.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
```
> **现在,文件就从版本库中被删除**

> **2.另一种情况是误删,因为版本库里存有被删的文件,所以可以把误删的文件恢复到指定版本里的文件:**
```sh
$ git restore readme.txt 
或
$ git checkout -- readme.txt // 最新一次保存到暂存区的readme.txt
```


### 推送到远程仓库

> - **代码提交到本地仓库后,可以推送到远程仓库备份,防止因本地主机硬盘损坏,代码丢失.同时,也便于他人从远程仓库克隆/更新代码到本地主机,查看/修改代码,也允许其它开发者推送各自的代码到远程仓库,通过远程仓库协作开发,分享开发经验**

> **1.初始代码从远程仓库克隆**

> **从已有的代码仓库克隆代码到本地,更新/修改后, 暂存(`git add`)、提交(`git commit`)到本地仓库,最后需要推送到远程仓库,可用 `git push [origin] [当前分支]`推送当前分支的修改到远程仓库**
```sh
$ git clone git@github.com:xxxxxx/git_test.git
。。。。。// 代码新增/修改
git add . // 暂存
git commit -m 'comment' // 提交本地仓库
git push origin <待提交的分支名>
```
> **git支持多种协议,默认的git://使用ssh,也可以使用https等其他协议.使用https除了速度慢以外,还有个最大的麻烦是每次推送都必须输入口令.一般使用ssh协议同步代码**

<br>
<br>

> **2.新建项目代码仓库**

> **创建本地主机的代码仓库后,需要和远程仓库创建关联,才能把本地代码推送到远程仓库备份保存,与其它人协作开发**

> + **在Gitlab/Github/阿里云等代码托管网站建立一个空仓库**

<img src="./media/new1.png" alt="Git常规流程" style="zoom:20%;" />

<br>

<img src="./media/new2.png" alt="Git常规流程" style="zoom:20%;" />

> **通过`git remote add origin <远程仓库地址>`把一个已有的本地仓库与之关联,然后通过`git push origin master`,把本地仓库的内容推送到远程(Eg. GitHub)仓库.Eg.:**
```sh
$ git remote add origin git@github.com:XXXXXX/git_test.git // 把远程仓库地址换成自有的仓库地址
```
> **远程库的名字是origin,是Git默认的叫法,也可以改成别的(一般不做修改)**
```sh
$ git push -u origin master
```

> **Notice:**
> **首次推送,由于远程库是空的,第一次推送master分支时,需加-u参数,Git不但会把本地的master分支内容推送到远程的master分支,还会把本地的master分支和远程的master分支进行关联,以后的推送或者拉取时就可以简化命令,无需-u参数.**

> **推送成功,GitHub页面可看到远程库内容和本地仓库一样**

<img src="./media/new3.png" alt="Git常规流程" style="zoom:20%;" />


## Part4 分支管理
### **1. 分支简介**

> + **分支指从主线上分离出来进行另外操作,解决临时需求,而又不影响主线,主线可以继续开发,类比父子线程.最后分支合并到主线上,而分支的任务完成后可以删除.**
> 
> + **几乎所有的版本控制系统都以某种形式支持分支.在很多版本控制系统中,这是一个略微低效的过程,常常需要完全创建一个源代码目录的副本.对于大项目来说,这样的过程会耗费很多时间.**
> + **git的分支功能强大,不需要将所有数据进行复制,创建目录副本,只要重新创建一个分支的指针,指向你需要的某一提交commit点,,那么新分支的指针就会指向你最新提交的这个commit对象.原先分支的指针则指向原先开发位置.**
> + **在哪个分支开发,HEAD就指向那个分支的最新提交对象commit.**


### **2. 创建与合并分支**
> **1. 创建分支————整体流程**


> **前文叙述可知,每次提交,Git都串成一条时间线,这条时间线就是一个分支.截止目前,只有一条时间线,在Git里,这个分支叫主分支,即master分支.**
> **标识符HEAD严格来说不是指向提交,而是指向master,master指向提交.**
> **一开始,master分支是一条线,Git用master指向最新的提交,再用HEAD指向master,确定当前分支,以及当前分支的提交点.**
> **每次提交,master分支都会向前移动一步.随着持续提交,master分支的线越来越长.**

<br>


> **当创建新分支,如dev时,Git新建一个指针叫dev,指向master相同的提交,再把HEAD指向dev,表示当前分支在dev上:**
> **Git创建一个分支很快:除了增加一个dev指针,改变HEAD指向,工作区的文件没有任何变化**

> **创建并切换分支后,对工作区的修改和提交就是针对dev分支,新提交一次,dev指针就往前移一步,而master指针指向位置不变:**


<img src="./media/branch2.png" alt="Git常规流程" style="zoom:55%;" />
<img src="./media/branch3.png" alt="Git常规流程" style="zoom:55%;" />

> **合并分支**
> **假如在dev上的工作完成,可以把dev合并到master上.最简单的情形,就是直接把master指向dev的当前提交,就完成了合并(在master没有新提交的情况下,直接移动指针).**
> **可见Git合并分支也很快:改变指针指向,工作区内容不变！**

<img src="./media/branch4.png" alt="Git常规流程" style="zoom:35%;" />

<br>

<img src="./media/branch5.png" alt="Git常规流程" style="zoom:35%;" />

> **合并完分支,dev分支可以删除.删除dev分支就是把dev指针给删掉,剩下一条master分支:**

<img src="./media/branch2.png" alt="Git常规流程" style="zoom:55%;" />

<br>

> **2. 创建分支————实际操作**


> **创建dev分支,同时切换到dev分支.**
```sh
$ git switch -c dev
Switched to a new branch 'dev'
```

>**`git switch`命令加上-c参数表示创建并切换,相当于以下两条命令:**
```sh
$ git branch dev
$ git switch dev
Switched to branch 'dev'
```
> **用`git branch`命令查看当前分支.命令会列出本地所有分支,当前分支前面会标一个*号.**
```sh
$ git branch
* dev
  master
```
> **可以在dev分支上正常提交,比如对readme.txt做个修改,加上一行:'Creating a new branch is quick.'然后提交:**
```sh
$ git add readme.txt 
$ git commit -m "branch test"
[dev b17d20e] branch test
 1 file changed, 1 insertion(+)
```
> **dev分支完成提交,可以切换回master分支:**
```sh
$ git switch master
Switched to branch 'master'
```
> **切换回master分支后,再查看readme.txt文件,刚才添加的内容不见！因为那个提交是在dev分支上,而master分支此刻的提交点并没有变:**

<img src="./media/branch4.png" alt="Git常规流程" style="zoom:55%;" />

<br>
<br>
<br>
<br>
<br>
<br>

> **把dev分支的代码合并到master分支上:**
```sh
$ git merge dev
Updating d46f35e..b17d20e
Fast-forward
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
```

> **git merge命令用于合并指定分支到当前分支.合并后查看readme.txt内容,和dev分支的最新提交是完全一样的.**
> **合并完成后,可以删除dev分支:**
```sh
$ git branch -d dev
Deleted branch dev (was b17d20e).
```
> **删除后,查看branch,只剩下master分支:**
```sh
$ git branch
* master
```

> **3. 推送分支**

> **查看远程仓库信息:**

<img src="./media/branch1.png" alt="Git常规流程" style="zoom:85%;" />

<br>

> **输出可以抓取和推送的origin的地址.如果没有推送权限,就看不到push的地址.**


> **推送分支,就是把该分支上的所有本地提交推送到远程库.推送时,指定本地分支,Git就把该分支推送到远程库对应的远程分支上:**
```sh
$ git push origin <待推送分支名>    
```

<br>
<br>
<br>
<br>
<br>
<br>

### **3.解决冲突**
> **合并冲突,简单来说,就是项目中同时有多人在协作开发,针对其中一部分文件同时有多人进行了修改,此时git不能执行快速合并,就会发生合并冲突,这时需要手动解决有冲突的文件**

> **新建并切换到dev分支**

<img src="./media/conflictd1.png" alt="Git常规流程" style="zoom:85%;" />

<br>

> **修改readme.txt最后一行,改为: "Creating a new branch is quick AND simple.".在dev分支上提交**

<img src="./media/conflict2.png" alt="Git常规流程" style="zoom:85%;" />

<br>


> **切换到master分支:**

<img src="./media/conflict3.png" alt="Git常规流程" style="zoom:85%;" />

<br>

> **在master分支上把readme.txt文件最后一行改为:"Creating a new branch is quick & simple.".提交:**

<img src="./media/conflict4.png" alt="Git常规流程" style="zoom:55%;" />

<br>

> **现在,master分支和dev分支各自都分别有新的提交:**

<img src="./media/conflict5.png" alt="Git常规流程" style="zoom:55%;" />

> **修改到同一行的情况下,Git无法执行“快速合并”,只能试图把各自的修改合并起来,产生合并冲突.**
> **Git提示,readme.txt文件存在冲突,必须手动解决冲突后再提交.git status也可以告诉我们冲突的文件**


<img src="./media/conflict6.png" alt="Git常规流程" style="zoom:75%;" />

<br>

<img src="./media/conflict8.png" alt="Git常规流程" style="zoom:65%;" />

<br>

> **查看readme.txt文件内容:**

<img src="./media/conflict7.png" alt="Git常规流程" style="zoom:65%;" />

<br>

> **Git用**<<<<<<<,=======,>>>>>>>**标记出不同分支的内容,我们修改如下,保存,提交:**
> **Creating a new branch is quick and simple.**

<img src="./media/conflict9.png" alt="Git常规流程" style="zoom:65%;" />

<br>

> **现在,master分支和dev分支版本线变成了下图所示:**

<img src="./media/conflict10.png" alt="Git常规流程" style="zoom:55%;" />

<br>
<br>


> **用带参数的git log也可以看到分支的合并情况:**

<img src="./media/conflict11.png" alt="Git常规流程" style="zoom:65%;" />

<br>

> **Notice:**
>> + **Git无法自动合并分支时,就必须手动解决冲突.解决冲突后,再提交,完成合并**.
>> + **解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容,再提交.**
>> + **用git log --graph命令可以看到分支合并图,--pretty 可选择输出格式,--abbrev-commit 简化commit-id输出**

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


### **4.分支开发注意事项**
> **1.紧急修复生产环境(线上的bug)**
>> **1.切换到master分支(git switch master)**
>> **2. 拉取master分支最新的代码(git pull).这步一定要记得执行,否则将基于本地仓库的旧master代码修复Bug,可能错上加错.**
>> **3.创建临时分支,在临时分支上修复生产Bug.注意分支命名规范:分支名需以hotfix或fix为前缀.项目中统一标准.**
>> **4.修复Bug,提交Bug分支代码到远程仓库**
>> **5.公司项目代码托管在GitLab,分支代码合并到master需要有相关权限(一般项目组长有合并权限),需到项目代码的GitLab上提交合并请求(即合并到master的请求),然后将产生的'合并请求链接'发送给权限相关人员,进行代码review、合并操作.**

<img src="./media/merge1.png" alt="Git常规流程" style="zoom:20%;" />

<br>

<img src="./media/merge2.png" alt="Git常规流程" style="zoom:20%;" />

<br>

<img src="./media/merge3.png" alt="Git常规流程" style="zoom:10%;" />

<br>
<br>
<br>


> **2.功能分支名**
> **开发新需求的分支称做功能分支,分支名需以dev或feature为前缀.项目中统一标准.**

> **3.Bug修复分支名**
> **新创建的Bug修复分支名,一般以fix为前缀.项目中统一标准.**

> **4.其它分支名**
> **临时需求,需开辟新分支开发的,分支名要做到简明扼要,见名知义.如导出功能需求:一般以export为前缀.**


> **5.前端对接/测试测试代码**
> **在功能开发分支开发好后,需将代码合并到测试分支(Eg.:dev.以项目统一为准),以便前端人员对接,测试同事进行测试.**
>> **1. 提交功能分支代码到远程仓库**
>> **2. 切换到dev分支,更新dev代码到最新(git pull).这步一定要记得执行,否则将基于本地仓库的旧dev代码进行合并,导致异常**
>> **3. 合并新功能分支到测试分支,并将合并代码推送到远程代码仓库.**


> **6.开发分支合并最新master代码**
> **在功能分支中开发新需求功能时,有时需要将master代码重新合并回开发分支:**
> + **在有新需求时,往往需要拉取最新的master线上生产代码,然后以最新的master代码为基础,新开一条功能需求分支,进行新需求的开发.**
> 
> + **在开发过程中,如碰到线上紧急Bug,需紧急修复,并推送到生产环境(即合并到master)后,往往可以将修复后最新的master代码'重新'合并回正在开发的功能分支,修复功能分支代码中相同Bug.**

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## 附 项目中常用的Git操作命令
> **git log 查看提交历史
git reflog 查看历史操作命令
git branch 查看当前所处分支
git clone \<url\> 克隆远程仓库
git pull 拉取当前分支的最新代码
git branch -a 查看本地仓库所有分支
git push 推送修改/新增的代码到远程仓库
git branch -D <分支名> 强制删除指定分支
git branch -d <分支名> 删除已合并过代码的分支
git add .  提交所有修改/新增的代码到本地暂存区
git switch branch_name 切换到branch_name分支
git restore  \<file\>... 撤销本地工作区文件的修改内容 
git reset --soft \<commit_id\> 回退版本,保留版本差异文件
git reset --hard \<commit_id\> 回退版本,丢弃版本差异文件
git restore  --staged  \<file\>... 撤销提交到本地暂存区的文件 
git commit -m '说明字符串'  提交修改/新增的代码到本地仓库
git switch -c branch_name 以当前分支为基础，新开一条分支，并切换到新的分支上
git push -u origin \<new_branch\> 新开的分支，'第一次' 推送到远端仓库(origin: 字符串常量,指向远程仓库).后续推送可缩简成 `git push`,即推送当前分支修改到远端.**