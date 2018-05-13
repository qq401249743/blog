---
title: Hexo搭建博客
date: 2018-04-17 20:30:00
tags: hexo
---

模式：HEXO+Github  
HEXO官网：https://hexo.io/  
HEXO原理：[hexo原理浅析](https://segmentfault.com/a/1190000008784436)  
我的博客地址：https://shuzang.github.io/blog/
<!-- more -->
---

## 安装前提  
安装Hexo很简单，但安装之前必须先确保电脑中已安装`Node.js`和`git`两个应用

### node.js安装  
安装Node.js的最佳方式是nvm

1）安装nvm  
nvm的安装可选用下面两种方式  
curl:  

    $ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
wget:

    $ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh

2）安装Node.js  
nvm安装成功后，重启终端并执行下列命令即可安装Node.js

    $ nvm install stable
3）nvm安装成功后，使用nvm命令却提示command not found解决办法  
- 进入nvm安装目录`cd ~/.nvm`  
- 查看目录下文件列表`ls`  
- 若无.bash_profile文件，则创建该文件`touch .bash_profile`  
- 打开该文件，将下列内容粘贴至其中
```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
```
- 上述语句是配置文件，与电脑有关，可运行下列命令得到  

		curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.9/install.sh | bash  
- 保存文件并关闭
- 更新刚配置的环境变量`source .bash_profile`  
- 输入2）中安装命令验证是否成功  

**注**：版本查看命令：

命令 | 解释
---|---
node -v                  | 查看node版本
npm -v 	                 | 查看npm版本


### git安装  

    $ sudo apt-get install git
git的版本查看命令为`git --version`
### 创建github仓库并开启github pages功能
- 创建一个新的公开仓库**blog**  
- 在仓库页面选择

    > Settings——>Options——GitHub Pages——>Source

  在下拉列表中选择**master branch**，选择**Save**，即会生成一个GitHub pages网址,这就是我们的网站域名了

### 安装Hexo  

    $ npm install -g hexo-cli
Hexo的版本查看命令为`hexo -v`

## 建站
安装Hexo完成后，请执行下列命令，Hexo将会在指定文件夹中新建所需要的文件  

```
$ hexo init blog
$ cd blog
$ npm install
```
Hexo 3.0把服务器独立成了个别模块，必须先安装[hexo-server](https://github.com/hexojs/hexo-server)才能使用

    $ npm install hexo-server --save

安装完成后，输入以下命令启动服务器，网站会在 http://localhost:4000/ 下启动。在服务器启动期间，Hexo会监视文件变动并自动更新，您无须重启服务器

    $ hexo server

依提示网址 http://localhost:4000/ 可看到初始界面，但这是本地的

## 关联Hexo和github page
使用`git config`命令配置git个人信息  

		$ git config --global  user.name  "your name"
		$ git config --global user.email "email@example.com"
配置SSH密钥（包括本地和github）
1. 在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开终端，创建SSH Key：

		$ ssh-keygen -t rsa -C  "youremail@example.com"
需要把邮件地址换成自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。
2. 如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人
3. 登陆GitHub，点击右上角头像，打开  
  >Settings——>SSH and GPG Keys——>New SSH Key

填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容,点`Add  SSH  key`就行了  
**部署**  
Hexo 提供了一键部署功能，只需一条命令就能将网站部署到服务器上。  
安装[hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git) 

		$ npm install hexo-deployer-git --save
修改blog目录下_config.yml文件的Deploment
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
    type: git
    repo: git@github.com:shuzang/blog.git
    branch: master
```

此时还要修改`_config.yml`文件中的URL部分，部署完才能看到正确的页面，修改如下
```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://github.com/shuzang
root: /blog
permalink: :year/:month/:day/:title/
permalink_defaults:
```
至此github与本地Hexo就关联起来了，此时可令Hexo生成静态文件并自动部署网站，命令为

		$ hexo d -g

关于其它的配置问题，以及页面改进等可在hexo官网查阅相关信息，或使用搜索引擎直接搜索
