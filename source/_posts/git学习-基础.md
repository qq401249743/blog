---
title: git学习-基础  
date: 2018-04-21 22:14:50   
tags: git

---

## 仓库和文件
repository，中文名叫仓库，我的理解就是一个文件夹，里面放了同属一个项目的所有文件

### 创建一个仓库
1. 在本地其实就是创建目录的命令,我在`/home/shuzang`目录下创建`gittest`文件夹

		$ mkdir gittest

2. 进入创建的文件夹，使用 `git init` 命令把该目录变成git的仓库

		$ cd gittest
        $ git init
提示  
>初始化空的Git仓库于/home/shuzang/gittest/.git/

3. 然后仓库就建好了，该目录下会多一个`.git`文件夹，默认是隐藏的，用来跟踪管理仓库。使用`ls -a`命令可以看到该文件夹，默认隐藏说明它很重要，里面的文件改动的话很容易导致仓库损坏
<!-- more -->

### 在仓库中添加文件

1. 文件类型  
 - 对txt文档、代码等文件类型，版本控制系统可记录每次的改动
 - 对图片、视频等文件类型，版本控制系统只能管理，不能记录改动，最多只能记录大小变化  

 **注**：word实质是二进制格式，所以同样没法跟踪改动

2. 首先新建一个txt文件并放在gittest目录下

		$ cd gittest
        $ touch hellogit.txt
  打开该文件并对其进行编辑
  
  		$ vim hellogit.txt

3. 编辑完成后，用`git add`命令将该文件添加到仓库

		$ git add  hellogit.txt
   用git  commit命令将文件提交到仓库

		$ git commit -m "message"
   message为备注信息，是该次提交的说明，一般情况是描述此次修改的

 命令执行完后的提示说：  
   1）提交到了主分支（master)，备注信息为“wrote a txt document"  
   2）改动了一个文件（hellogit.txt），加了三行内容(注意那个+号)  
   3）最后一行中100代表regular file，644代表文件权限，具体解释我也找不到官方文档了，自己搜吧  

4. 另外执行分add和commit两步的原因是commit可以将之前add的所有文件一起提交，如

		$ git add file1.txt
		$ git add file2.txt file3.txt
		$ git commit -m "add 3 files"
   另外，可以使用如下命令一次性将所有修改添加到暂存区
   		
        $ git add .
   更多关于`git add`命令的说明参见[git add命令说明](https://www.yiibai.com/git/git_add.html)

### 对文件进行修改
还记得我们的初衷吗，所以，对文件修改再提交是一个会经常重复的工作  
首先我们将hellogit.txt文件的内容进行第二次修改  
用 git status 命令查看仓库当前状态

		$ git status
提示内容包括
- 位于哪个分支
- 修改了哪个文件
- “修改尚未加入提交”

如果我们还想看到具体做了哪些修改，用`git  diff`命令，diff就是diffenence，所以`git diff`的意思就是查看不同
 
		$ git diff hellogit.txt
提示中说明了我们在第一行加了一个"distributed"单词，把第三行两个单词中间的空格和最后的叹号去掉了
此时我们确认了做的修改是我们心里所想的，就可以再次提交了

		$ git add hellogit.txt
        $ git status
        $ git commit -m "第二次修改"
        $ git status
提交过程中可以每一步都使用`git status`命令查看当前状态，最后commit提交完的状态提示为：
>位于分支master  
>无文件要提交，干净的工作区

此时就放心了，每次修改完或者要离开工作岗位的时候提交一次，就像游戏存档，离开之前或者重要关卡前存档，失败的时候就能读档重来，这里修改出错也可以从上一次的commit重来

<br>
## 历史版本

修改的次数会逐渐变多，随着时间的流逝，我们完全不会记得每次修改了哪些内容，当然，git的出现就是为了帮我们解决这个问题，所以理所当然的会有查看历史版本的能力，以及回退到某个版本的能力


### 查看历史版本

使用 `git log` 命令可以查看历史改动

		$ git log

提示内容是按从近到远的顺序把所有改动列举一遍，包括用户名、邮箱、修改日期，当时添加的message信息，不想看名称、邮箱和日期可以使用参数简化显示，如下：

		$ git log --pretty=oneline

也可以用以下命令查看参数使用方式

		$  git  log --help
提示内容中每次修改最前面的一串长字符是版本号（commit  id），用十六进制表示，用来代表我们每次修改的版本

### 回退（读档）
首先，在git中，用`HEAD`表示当前版本，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上版本数多的时候写`^`写不过来，所以写成`HEAD~number`，如往上100个版本就是`HEAD-100`  
回退命令为`git reset`，比如，回退到上一个版本

	$ git  reset --hard HEAD^

然后我们就看到真的变回去了，如果记下了版本号，我们还可以再跳回最后一个修改版本，也就是说，我们突然不想回退了，或者退多了

	$ git reset  --hard  2fee
`2fee`为其版本号，但版本号没必要写全，因为它的作用是为了区分各版本，所以只要找到第一个不相同的那位，写到那里就行了，查看文件，果然回来了  
版本跳转快速的原因是`HEAD`只是一个指向当前版本的指针，跳转版本的时候也仅仅移动指针  
同样存在还有忘了版本号的情况，但git同样提供了`git reflog`命令记录每次`HEAD`指针移动

	$ git reflog
该命令会显示每次修改版本的版本号

<br>
## 暂存区和工作区
工作区就是电脑里能看到的目录，比如我们的gittest文件夹  
该文件夹里的隐藏目录.git则不属于工作区，它是版本库  
版本库里有暂存区，还有自动创建的第一个分支master，以及指向master的一个指针叫HEAD
![暂存区和工作区](https://github.com/shuzang/image/raw/master/git%E6%9A%82%E5%AD%98%E5%8C%BA%E5%92%8C%E5%B7%A5%E4%BD%9C%E5%8C%BA%E8%AF%B4%E6%98%8E.png?raw=true)  
`git add`实际上是把文件修改添加到暂存区；
`git commit`实际上是把暂存区的所有内容提交到当前分支

### 丢弃修改
**场景1**：当改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，使用命令

	$ git checkout -- file。
**场景2**：当不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令

	$ git reset HEAD file
回到场景1，第二步按场景1操作。

已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库

### 删除文件
一般情况，是直接在文件夹中用rm命令删除，但这样工作区和版本库就不一致了

	$ rm hellogit.txt
    $ git status

此时有两种情况，一种是删错了，可以直接用命令恢复

	$ git checkout --gittest
另一种情况是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`

	$ git rm hellogit.txt
    $ git commit -m "remove hellogit.txt"
    $ git status

<br>
## 远程仓库
使用github提供的免费远程仓库，由于本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：

### 创建SSH Key
在用户主目录下，看看有没有`.ssh`(默认隐藏)目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开终端，创建SSH Key：

	$ ssh-keygen -t rsa -C "youremail@example.com"
需要把邮件地址换成自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

### 登陆GitHub，
点击右上角头像，打开
>Settings——>SSH and GPG Keys——>New SSH Key

填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容
然后点击`Add SSH key`就行了

GitHub需要SSH Key识别出你推送的提交确实是你推送的，而不是别人冒充的。当然，GitHub允许添加多个Key。假定有若干电脑，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

<br>
## 添加远程仓库
首先在github创建一个**同名仓库**,创建完成后跳转界面给我们提供了三个选择
- ...or create a new repository on the command line
- ...or push an existing repository from the command line
- ...or import code from another repository

现在要做的当然是把本地已存在的gittest仓库关联到github喽，关联其实是有SSH和https两种方式的，这里我们用SSH，我第一次因为没注意用了一次https，但可以使用下面的命令删除，再重新关联

	$ git remote rm origin
正式的关联和推送到远程仓库的命令如下

	$ git remote add origin git@github.com:DestinyJLD/gittest.git
	$ git push -u origin master
提示
>分支master设置为跟踪来自origin的远程分支master

转到网页github可以看到gittest仓库和本地仓库里的文件一样了

以后再把本地推送到远程仓库，就可以直接用如下命令

	$ git push origin master

<br>
## 从远程仓库克隆到本地
`git  clone`命令，如果是下载某个指定分支的内容，命令为

	$ git clone -b 分支名 仓库地址


