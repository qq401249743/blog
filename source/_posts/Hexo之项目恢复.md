---
title: Hexo之项目恢复
date: 2018-04-17 21:47:18
tags: hexo
---
## 问题
hexo+github模式的个人博客部署好了之后，blog文件夹中存在大量的文件，不仅仅是各种配置，还有我们所写的文章。在操作过程中，可能面对两种情况：
- 系统崩溃，所有文件丢失
- 要换电脑了

所以我们应未雨绸缪，经多方查找，终于找到了一种比较简单而有效的方法
<!-- more -->
## 备份方案
blog仓库master分支用来存放生成的静态网页，新建hexo分支用来存放Hexo生成的网站原始文件
1. 在本地blog文件夹下创建文件.gitignore,这个文件是没有后缀的，编辑该文件内容如下
``` 
db.json   
node_modules/ 
public/  
.deploy_git/
...
```
其中，包括deploy_git文件夹，这是`hexo d`渲染并上传到github发布出去的文件夹，每次`hexo d`都会全部覆盖；/node_modules就是`npm install`生成的插件等，没必要上传，而且也上传不了
2. 在blog文件夹下执行  
```
#git初始化  
git init  
#创建hexo分支，用来存放源码  
git checkout -b hexo  
#git 文件添加  
git add .  
#git 提交  
git commit -m "Hexo备份"  
#添加远程仓库  
git remote add origin git@github.com:shuzang/blog.git  
#push到hexo分支  
git push origin hexo  
```
这样一来，在GitHub上的blog仓库就有两个分支，一个hexo分支用来存放网站的原始文件，一个master分支用来存放生成的静态网页。

## 恢复
当重装电脑之后，或者想在其他电脑上修改博客，可以使用下列步骤：
1. 先执行安装Hexo及之前的所有安装步骤  
2. 执行`hexo init blog`
3. 将github上blog仓库的hexo分支`git clone`下来   
4. blog文件夹下npm 

		cd blog 
        npm install –no-bin-links 
		$ npm install hexo-deployer-git
5. 重新配置github和coding的公钥
6. 安装服务器模块

## 更新
- 每次写作之后，先执行`hexo d`，部署完之后，再去备份  
