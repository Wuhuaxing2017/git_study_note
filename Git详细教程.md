# Git详细教程





## 一、简介

> git是什么？

为了解决源代码存放问题而开发出来的**分布式版本控制系统**

> 特点

免费、开源、安全、便捷

## 二、安装

Debian或Linux Ubuntu安装Git

```
sudo apt-get install git
```

Windows安装Git

使用git程序，然后Git-->git bash

安装完成后，还需要最后一步设置，在命令行输入：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

## 三、创建版本库

> 什么是版本库呢？

版本库又名仓库，英文名**repository**，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

所以，创建一个版本库非常简单，首先，选择一个合适的地方，



### 1、创建一个空目录：

```bash
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```

如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，**请确保目录名（包括父目录）不包含中文。**



### 2、通过`git init`命令

把这个目录变成Git可以管理的仓库：

```bash
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

*瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个`.git`的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。*

*如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见。*



### 3、把文件添加到版本库

首先这里再明确一下，所有的版本控制系统，其实**只能跟踪文本文件的改动**

*比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。*



使用Windows的童鞋要特别注意：

**千万不要使用Windows自带的记事本编辑任何文本文件**。

*原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。建议你下载[Notepad++](http://notepad-plus-plus.org/)代替记事本，不但功能强大，而且免费！记得把Notepad++的默认编码设置为UTF-8 without BOM即可。*



### 4、编写一个小文件

言归正传，现在我们编写一个`readme.txt`文件，内容如下：

```bash
Git is a version control system.
Git is free software.
```

一定要放到`learngit`目录下（子目录也行），因为这是一个Git仓库，放到其他地方Git再厉害也找不到这个文件。



第一步，用命令`git add`告诉Git，把文件添加到仓库：

```bash
$ git add readme.txt
```

第二步，用命令`git commit`告诉Git，把文件提交到仓库：

```bash
$ git commit -m "wrote a readme file"
[master (root-commit) cb926e7] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```



`git commit`命令执行成功后会告诉你，1个文件被改动（我们新添加的readme.txt文件），插入了两行内容（readme.txt有两行内容）。

为什么Git添加文件需要`add`，`commit`一共两步呢？因为`commit`可以一次提交很多文件，所以你可以多次`add`不同的文件，比如：

```bash
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```



## 四、Git操作

我们已经成功地添加并提交了一个readme.txt文件，现在，是时候继续工作了，于是，我们继续修改readme.txt文件，改成如下内容：

```bash
Git is a distributed version control system.
Git is free software.
```

现在，运行`git status`命令看看结果：

```bash
$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#    modified:   readme.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
```

`git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令告诉我们，readme.txt被修改过了，但还没有准备提交的修改。

虽然Git告诉我们readme.txt被修改了，但如果能看看具体修改了什么内容，自然是很好的。比如你休假两周从国外回来，第一天上班时，已经记不清上次怎么修改的readme.txt，所以，需要用`git diff`这个命令看看：

```bash
$ git diff readme.txt 
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
```

`git diff`顾名思义就是查看difference，显示的格式正是Unix通用的diff格式，可以从上面的命令输出看到，我们在第一行添加了一个“distributed”单词。

知道了对readme.txt作了什么修改后，再把它提交到仓库就放心多了，提交修改和提交新文件是一样的两步，第一步是`git add`：

```bash
$ git add readme.txt
```

同样没有任何输出。在执行第二步`git commit`之前，我们再运行`git status`看看当前仓库的状态：

```bash
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       modified:   readme.txt
#
```

`git status`告诉我们，将要被提交的修改包括readme.txt，下一步，就可以放心地提交了：

```bash
$ git commit -m "add distributed"
[master ea34578] add distributed
 1 file changed, 1 insertion(+), 1 deletion(-)
```

提交后，我们再用`git status`命令看看仓库的当前状态：

```bash
$ git status
# On branch master
nothing to commit (working directory clean)
```

Git告诉我们当前没有需要提交的修改，而且，工作目录是干净（working directory clean）的。



### 1、版本回退

现在，你已经学会了修改文件，然后把修改提交到Git版本库，现在，再练习一次，修改readme.txt文件如下：

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
```

然后尝试提交：

```bash
$ git add readme.txt
$ git commit -m "append GPL"
[master 3628164] append GPL
 1 file changed, 1 insertion(+), 1 deletion(-)
```

像这样，你不断对文件进行修改，然后不断提交修改到版本库里，就好比玩RPG游戏时，每通过一关就会自动把游戏状态存盘，如果某一关没过去，你还可以选择读取前一关的状态。有些时候，在打Boss之前，你会手动存盘，以便万一打Boss失败了，可以从最近的地方重新开始。Git也是一样，每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为`commit`。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个`commit`恢复，然后继续工作，而不是把几个月的工作成果全部丢失。

现在，我们回顾一下readme.txt文件一共有几个版本被提交到Git仓库里了：

版本1：wrote a readme file

```
Git is a version control system.
Git is free software.
```

版本2：add distributed

```
Git is a distributed version control system.
Git is free software.
```

版本3：append GPL

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
```

当然了，在实际工作中，我们脑子里怎么可能记得一个几千行的文件每次都改了什么内容，不然要版本控制系统干什么。版本控制系统肯定有某个命令可以告诉我们历史记录，在Git中，我们用`git log`命令查看：

```bash
$ git log
commit 3628164fb26d48395383f8f31179f24e0882e1e0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 15:11:49 2013 +0800

    append GPL

commit ea34578d5496d7dd233c827ed32a8cd576c5ee85
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 14:53:12 2013 +0800

    add distributed

commit cb926e7ea50ad11b8f9e909c05226233bf755030
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Mon Aug 19 17:51:55 2013 +0800

    wrote a readme file
```

`git log`命令显示从最近到最远的提交日志，我们可以看到3次提交，最近的一次是`append GPL`，上一次是`add distributed`，最早的一次是`wrote a readme file`。如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数：

```bash
$ git log --pretty=oneline
3628164fb26d48395383f8f31179f24e0882e1e0 append GPL
ea34578d5496d7dd233c827ed32a8cd576c5ee85 add distributed
cb926e7ea50ad11b8f9e909c05226233bf755030 wrote a readme file
```

需要友情提示的是，你看到的一大串类似`3628164...882e1e0`的是`commit id`（版本号），和SVN不一样，Git的`commit id`不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的`commit id`和我的肯定不一样，以你自己的为准。为什么`commit id`需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。

每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线：

![git-log-timeline](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907545599be4a60a0b5044447b47c8d8b805a25d2000/0)

好了，现在我们启动时光穿梭机，准备把readme.txt回退到上一个版本，也就是“add distributed”的那个版本，怎么做呢？

首先，Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`3628164...882e1e0`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

现在，我们要把当前版本“append GPL”回退到上一个版本“add distributed”，就可以使用`git reset`命令：

```bash
$ git reset --hard HEAD^
HEAD is now at ea34578 add distributed
```

`--hard`参数有啥意义？这个后面再讲，现在你先放心使用。

看看readme.txt的内容是不是版本`add distributed`：

```bash
$ cat readme.txt
Git is a distributed version control system.
Git is free software.
```

果然。

还可以继续回退到上一个版本`wrote a readme file`，不过且慢，然我们用`git log`再看看现在版本库的状态：

```bash
$ git log
commit ea34578d5496d7dd233c827ed32a8cd576c5ee85
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 14:53:12 2013 +0800

    add distributed

commit cb926e7ea50ad11b8f9e909c05226233bf755030
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Mon Aug 19 17:51:55 2013 +0800

    wrote a readme file
```

最新的那个版本`append GPL`已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？

办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个`append GPL`的`commit id`是`3628164...`，于是就可以指定回到未来的某个版本：

```bash
$ git reset --hard 3628164
HEAD is now at 3628164 append GPL
```

版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。

再小心翼翼地看看readme.txt的内容：

```bash
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
```

果然，我胡汉三又回来了。

Git的版本回退速度非常快，因为Git在内部有个指向当前版本的`HEAD`指针，当你回退版本的时候，Git仅仅是把HEAD从指向`append GPL`：

![git-head](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907584977fc9d4b96c99f4b5f8e448fbd8589d0b2000/0)

改为指向`add distributed`：

![git-head-move](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907594057a873c79f14184b45a1a66b1509f90b7a000/0)

然后顺便把工作区的文件更新了。所以你让`HEAD`指向哪个版本号，你就把当前版本定位在哪。

现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的`commit id`怎么办？

在Git中，总是有后悔药可以吃的。当你用`$ git reset --hard HEAD^`回退到`add distributed`版本时，再想恢复到`append GPL`，就必须找到`append GPL`的commit id。Git提供了一个命令`git reflog`用来记录你的每一次命令：

```bash
$ git reflog
ea34578 HEAD@{0}: reset: moving to HEAD^
3628164 HEAD@{1}: commit: append GPL
ea34578 HEAD@{2}: commit: add distributed
cb926e7 HEAD@{3}: commit (initial): wrote a readme file
```

终于舒了口气，第二行显示`append GPL`的commit id是`3628164`，现在，你又可以乘坐时光机回到未来了。



### 2、工作区和暂存区

> Git和SVN的一个不同之处就是有暂存区的概念

现在我来讲一下工作区、版本库、暂存区都是些什么。

- 工作区就是电脑能看得到的目录，比如当前目录所在这个文件夹就是一个工作区。
- 版本库，我们把git这个目录创建git init的时候，会生成一个`.git`的隐藏目录，那么这个就是git的版本库
- 暂存区是版本库里的一部分，git创建的时候会自动生成一个分支master，以及一个指向master的指针HEAD

![git-repo](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)

其实这个意思很容易理解，就是先把修改的文件放入暂存区，然后一次性提交。



### 3、管理修改

>  其实这里有个概念要弄清楚，Git可以说管理的并不是文件，而是修改

新增、修改、删除都是修改的一部分对不？

也就是说，git的每一次修改都要被add 之后提交才能识别为changes.

commit提交只会提交暂存区的内容，那么暂存区存放的是文件吗？不！刚开始			我以为add之后会有一个类似软链接一样的东西，其实并不是。**暂存区存放的是修改！**所以每次修改，如果不用`git add`到暂存区,那么就不会加入到`commit`中。



### 4、撤销修改

> 如果修改了工作区的内容，需要丢弃更改

可以用`git check -- filename`,那么更改就会全部撤销

> 如果添加到暂存区后，发现修改的内容有不合适的部分，

那么就用`git reset HEAD filename`把暂存区的修改撤销，重新放回工作区。`git reset`既可以回退版本也可以吧暂存区的修改回退到工作区。

> 如果提交commit后，发现修改的内容有不合适的部分，

那么就可以用版本回退的功能回到上一个版本。但要是提交到了远程库就over了

`git reset -- hard HEAD^`就可以回到上一个版本，回到具体版本参考版本回退那一节。

### 5、删除文件

> 首先，之前我们说过，删除也是一个修改操作。

如果提交了一个文件到版本库，然后不需要这个文件了。那么工作区的文件可以直接删除，版本库的文件可以先`git rm filename`,然后提交删除这个修改就可以了1.可以使用`git status`命令查看工作区状态。那么此时工作区和版本库就是一样的。



如果误删了工作区的文件想要恢复，那么就可以`git check -- filename`，同上面一样，相当于还原删除动作这个修改。



## 五、远程仓库

之前我们操作的都是本地git版本库。那么现在我们就要把git仓库分布到不同的机器上。

> 要向本地仓库和github仓库文件传输，先要通过ssh加密，相当于钥匙

- 首先创建ssh key ,后面就是你的git账号

  ```bash
  $ ssh-keygen -t rsa -C "youremail@example.com"
  ```

- 用户主目录`.ssh`里面有`id_rsa`和`id_rsa.pub`两个文件。从文件名可以看出带pub的是公共的的意思。所以前面那个是私钥，后面的是公钥。**私钥不能泄密！**

- 登陆GitHub，打开“Account settings”，“SSH Keys”页面：

  添加公钥文件的内容，标题任意。

> github上面的内容大家都可以看，但只有自己可以修改。大家都可以下载克隆但只有自己可以推送。（私有库除外）



### 1、添加远程库

登陆GitHub，创建一个新的仓库，这个仓库是空的。可以克隆出新的仓库也可以和本地仓库关联然后把本地内容推送到github仓库.

- 首先，在本地关联远程库。远程库默认叫法就是origin

  ```bash
  $ git remote add origin git@github.com:michaelliao/learngit.git
  ```

- 然后，把内容推过去，相当于把master分支推到远程。

  ```bash
  $ git push -u origin master
  ```

  加上`-u`参数是为了

同时推送master分支到远程master分支，同时将两个分支关联起来。以后的推送和拉取就可以简化命令。

这个时候，本地库和远程库就是一样的了。只要本地提交后就可以通过下面的命令推送了。

```bash
$ git push origin master
```



### 2、从github克隆

克隆远程库到本地,只要是正确的地址，用`git://`或`https`两种协议都OK，但是用`git://`可能会更快，择合适的就行。

```bash
$ git clone git@github.com:wuhuaxing2017/test.git
```

如果是多人协作开发，那么各自克隆一份就可以



## 六、分支管理

> 分支就像平行宇宙，一条分支的所有操作就是就是时间线。两个不同的分支之间不会相互干扰。比如你正在开发一个项目可以一个分支保留项目代码，另一个在不同时期提交代码。

### 1、创建与合并分支

git里的主分支就是`master`，`HEAD`指向的就是当前分支，默认是`master`

![git-br-initial](https://cdn.liaoxuefeng.com/cdn/files/attachments/0013849087937492135fbf4bbd24dfcbc18349a8a59d36d000/0)

刚开始`master`是第一个点,每提交一次就多一个。

创建一个分支，就相当于多了一个指向，`HEAD`指向谁，提交就会在谁那里改变，其他分支不会变。留在原来的地方。

![git-br-dev-fd](https://cdn.liaoxuefeng.com/cdn/files/attachments/0013849088235627813efe7649b4f008900e5365bb72323000/0)

如果两个分支要想合并，直接把`master`指向`dev`的当前提交，就完成了合并。很简单！

![git-br-ff-merge](https://cdn.liaoxuefeng.com/cdn/files/attachments/00138490883510324231a837e5d4aee844d3e4692ba50f5000/0)

如果不要`dev`分支了，那么把指向的指针删了就行。

![git-br-rm](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384908867187c83ca970bf0f46efa19badad99c40235000/0)

**那么具体该怎么操作呢？**

- 创建分支(英文是`branch`)

  ```bash
  $ git branch dev  
  ```

- 切换分支

  ```bash
  $ git checkout dev 
  ```

- 其实还有个更好的

  ```bash
  $ git checkout -b dev  # -b参数表示创建同时切换
  ```


- 查看分支，当前分支前面会标一个`*`号

  ```bash
  $ git branch
  ```




> 接下来写一写合并

比如：将`dev`分支的工作成果合并到`master`分支上

![git-br-on-master](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384908892295909f96758654469cad60dc50edfa9abd000/0)

```bash
$ git merge dev
```



> 删除分支

```bash
$git branch -d dev
```



### 2、解决冲突

> 之前那个合并分支只是在一个分支有修改提交，然后把指针指向改变的`快速合并`，但要是两个分支修改内容不同，`merge`合并肯定会有问题。

![git-br-feature1](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384909115478645b93e2b5ae4dc78da049a0d1704a41000/0)

可以用`git status`查看状态，git会将冲突的文件告诉你。

或者你可以直接查看这个文件，Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容。

可以用下面这个带参数的log命令查看分支情况

`$ git log --graph --pretty=oneline --abbrev-commit`

**当分支无法合并时，必须先解决冲突再提交合并！**

**可以用`git log --gragh`命令查看合并图**



### 3、分支管理的策略

> 真的是快气死我了，这个typora太差了，竟然没有保存提醒！做了三个小节的数据竟然没了。那就再写一遍吧。

实际开发中，我们不可能单单只在一个分支上进行开发。一般来讲`master`分支应该是稳定的，仅仅是用来发布版本；另一条分支是为了测试版本。而其他人的分支就可以向测试版本合并。

![git-br-policy](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384909239390d355eb07d9d64305b6322aaf4edac1e3000/0)

> 上一节我讲的是`merge`合并,但那都是快速合并，**但快速合并删除分支后，会丢掉分支信息。**所以，`merge`有个`--no-ff`的参数

**`$ git merge --no-ff -m "merge with no-ff" dev`**

因为这种参数合并的时候会进行一个`commit`提交，所以要加描述

![git-no-ff-mode](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384909222841acf964ec9e6a4629a35a7a30588281bb000/0)

这种普通模式的合并，合并后的历史有分支，可以看出曾经做过合并操作。但是快速合并就没有。



### 4、bug分支

> bug分支，顾名思义就是和bug有关的分支。

现实的一个案例，在某个分支出现了一个bug。那就需要创建分支->修复bug->合并分支->删除分支。但很有可能的情况是，当前进度还没法提交，但bug必须要尽快修复！

这个时候就可以用git的冷藏室功能，这个功能类似于360手机的一个“应用冷藏“功能，将暂时不用但又不能删除的应用冻起来，等到要用的时候解冻。

**在当前分支`git stash`就可以“储藏当前分支”**



### 5、feature分支



### 6、多人协作



### 7、Rebase



## 七、标签管理



### 1、创建标签



### 2、操作标签



## 八、自定义Git

### 1、忽略特殊文件



### 2、配置别名



### 3、搭建Git服务器







