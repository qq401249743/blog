---
title: Hexo进阶配置
date: 2018-04-17 21:00:00
tags: hexo
---
之前我们完成了博客从无到有的搭建，现在，我们来熟悉一下blog文件夹中的各文件，并按自己的想法做一些进阶的配置
<!-- more -->
## blog/package.json  
该文件中是应用程序的相关信息，内容不多，所以可以直接列举如下：  
```
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": "3.7.1"
  },
  "dependencies": {
    "hexo": "^3.2.0",
    "hexo-deployer-git": "^0.3.1",
    "hexo-generator-archive": "^0.1.4",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-index": "^0.2.0",
    "hexo-generator-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.3.0",
    "hexo-renderer-marked": "^0.3.0",
    "hexo-renderer-stylus": "^0.3.1",
    "hexo-server": "^0.2.2"
  }
}
```
我们看到了Hexo的版本，看到了我们亲手安装的`hexo-deployer-git`和`hexo-generator-archive`的版本，以及其他默认安装的组件的版本  

## blog/scaffolds
模板文件夹，新建文章时，Hexo会根据scaffold来建立文件，以后详细讨论模板的问题  

## blog/source
资源文件夹,存放用户资源的地方。除 `_posts` 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。  

## blog/themes
主题文件夹，Hexo会根据主题来生成静态页面，同样，主题的问题我们以后会详细讨论  

## blog/_config.yml
.yml格式的文件是用[YAML](http://www.ruanyifeng.com/blog/2016/07/yaml.html?f=tt)语言写的配置文件，这种语言是专门用来写配置文件的语言，但现在我们不关心其他的事情，只要知道如何修改该文件相应内容即可 

### 网站
```
# Site
title: Hexo             #网站标题
subtitle:               #网站副标题
description:            #网站描述，用于被搜索引擎搜索
keywords:
author: shuzang         #自己的名字，用于显示文章作者
language:               #网站使用的语言
timezone:               #网站时区，默认使用电脑时区
```
### 网址
```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://github.com/shuzang          #网址
root: /blog                              #网站根目录
permalink: :year/:month/:day/:title/     #文章的永久链接格式
permalink_defaults:                      #永久链接中各部分默认值
```

**一些暂时永不的的分类解释忽略，要用时直接官网查询**
### 分页
```
# Pagination
## Set per_page to 0 to disable pagination
per_page: 10            #每页显示的文章数量（0=关闭分页功能）
pagination_dir: page    #分页目录
```
### 扩展
```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: landscape                   #当前主题名称，值为false时禁用主题
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:                            #deploy部分上篇已介绍
  type: git
  repo: git@github.com:shuzang/blog.git
  branch: master
```
## 命令
Hexo中有一些操作的基本命令是需要掌握的  
### new
		$ hexo new [layout] <title>

新建一篇文章。如果没有设置 `layout` 的话，默认使用 `_config.yml` 中的 `default_layout` 参数代替。如果标题包含空格的话，请使用引号括起来。layout是页面布局。

### publish
		$ hexo publish [layout] <filename>
发表草稿，具体的等需要用到草稿功能再看  

### server
		$ hexo server
启动服务器

### generate、deploy
		$ hexo d -g
生成静态文件并部署网站，二合一命令，分开写麻烦

### clean
		$ hexo clean
清除缓存文件 (db.json) 和已生成的静态文件 (public)。  
在某些情况（尤其是更换主题后），如果发现对站点的更改无论如何也不生效，可能需要运行该命令。

### list
		$ hexo list <type>
列出网站资料

**其他的命令诸如出问题后的调试用命令等用到再查**
顺便吐槽，Hexo官方文档前面还可以，后面写的真的烂，太简略了，根本说不清