---
title: git学习-背景  
date: 2018-04-20 19:06:20  
tags: git

---

![git_github](https://github.com/shuzang/image/raw/master/git+github.png?raw=true)

## git与github
{% note default %}
github是一个网站，git是一个分布式版本控制系统
{% endnote %}
<!-- more -->
### 版本控制
生活中可能会出现两种情况

1. 你写了一篇文章，过了一天做了一定的修改，但是觉得之前的版本可能有用，于是改了一下名字重新保存，后来又重复修改保存了多次，这样电脑里就可能出现像  
>版本1.doc  
版本2.doc  
最终版本.doc  
最终版本改.doc  
真的是最终版本了.doc

 等等众多重命名文件，头疼不已。
2. 多个人合作写文档，相互发送完自己的版本得校对对方的改动，然后进行合并,会花费大量不必要的精力

而在编程领域，修改命名和合作更加广泛，这个问题也就更加突出  
>版本控制的作用就是记录每次文件的改动


### 集中式和分布式版本控制

- **集中式**就是有一个服务器放所有的东西，要工作的时候下载回来，改动完上传回去，记录和不同人的改动合并都由服务器端完成，然而这种形式极度依赖于服务器性能和网速  
- **分布式**和torrent差不多，每个人的电脑都是服务器，修改完直接把修改的部分推送给所用拥有这个项目的人。分布式版本控制也有服务器，但主要是负责做备份，并方便大家的交换用的，并不是必要

### git与github

- **git**是Linux的开创者为了管理Linux源码写的分布式版本控制软件  
- **github**是为开源项目免费提供git存储的网站，2008年上线
其实现在称呼的话这两个都已经快混了，提到git一般第一反应也是github

<br>
## git安装
一般情况都是在Linux上用的，但后来也移植到了windows，现在windows上甚至有了GUI版本

### Linux安装
查看有没有安装：

	$ git
未安装则在ubuntu和debian系统的命令行直接输入以下命令安装

	$ sudo apt-get install git
安装完成后还要设置自己的名字和Email地址

		$ git config --global  user.name   "your name"
		$ git config --global  user.email  "email@example.com"

`--global`参数的意思是这个名字和邮箱应用于所有git仓库

### windows安装
Windows下已经有GUI版适配了，而且很好用  
下载地址为：https://desktop.github.com/  
**注**：个人看法，不管是下载地址的网页还是软件都做的很舒服
