---
title: Hexo之Next主题
date: 2018-04-17 21:11:00
tags: hexo
---
## 前言
默认的主题不是很好看，之前用了yilia主题，但是遇到问题有的找不到答案，但在搜索过程中发现next主题的用户数量是最多的，相关的问题解决教程也最多，查看了一些别人next主题的博客之后，觉得也挺好看，于是决定转入next
<!-- more -->
## 安装
先克隆到本地相应位置  
```
$ cd blog
$ git clone https://github.com/theme-next/hexo-theme-next themes/next
```
更新到最新版本
```
$ cd themes/next
$ git pull
```

## 启用
启用需要修改`blog/_config.yml`文件
```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
```
将theme的值改为`next`即可，然后部署到网站

		$ hexo d -g
此时查看自己的博客即可发现风格已改变

## 美化
虽然next主题本身很简洁很好看，但我们可能需要根据自身需要做一定的配置修改来美化页面或增删功能    

### Scheme
next提供了三种Scheme，其实就是主题的三种展示方式，在`blog/themes/next/_config.yml`中修改，这也是主题配置文件，很多配置项都在这里修改  
```
# Schemes
#scheme: Muse
scheme: Mist
#scheme: Pisces
#scheme: Gemini
```
我比较喜欢Mist风格

### 菜单
　　菜单配置包括三个部分，第一是菜单项（名称和链接），第二是菜单项的显示文本，第三是菜单项对应的图标。我们主要关心的是菜单项配置。在主题配置文件中菜单项对应的字段是 menu。去掉字段名前面的`#`即可启用
```
menu:
  home: / || home                        # 主页
  about: about/ || user                  # 关于
  tags: tags/ || tags                    # 标签
  archives: archives/ || archive         # 归档
  ```
### 语言
编辑主目录下的站点配置文件，修改language选项为中文

		language: zh-CN

### 头像
头像的修改在主题配置文件的avatar项

### 修改头像为圆形并使其旋转
打开`\themes\next\source\css\_common\components\sidebar\sidebar-author.styl`，在里面添加如下代码：
```
.site-author-image {
  display: block;
  margin: 0 auto;
  padding: $site-author-image-padding;
  max-width: $site-author-image-width;
  height: $site-author-image-height;
  border: $site-author-image-border-width solid $site-author-image-border-color;
  /* 头像圆形 */
  border-radius: 80px;
  -webkit-border-radius: 80px;
  -moz-border-radius: 80px;
  box-shadow: inset 0 -1px 0 #333sf;
  /* 设置循环动画 [animation: (play)动画名称 (2s)动画播放时长单位秒或微秒 (ase-out)动画播放的速度曲线为以低速结束 
    (1s)等待1秒然后开始动画 (1)动画播放次数(infinite为循环播放) ]*/
 
  /* 鼠标经过头像旋转360度 */
  -webkit-transition: -webkit-transform 1.0s ease-out;
  -moz-transition: -moz-transform 1.0s ease-out;
  transition: transform 1.0s ease-out;
}
img:hover {
  /* 鼠标经过停止头像旋转 
  -webkit-animation-play-state:paused;
  animation-play-state:paused;*/
  /* 鼠标经过头像旋转360度 */
  -webkit-transform: rotateZ(360deg);
  -moz-transform: rotateZ(360deg);
  transform: rotateZ(360deg);
}
/* Z 轴旋转动画 */
@-webkit-keyframes play {
  0% {
    -webkit-transform: rotateZ(0deg);
  }
  100% {
    -webkit-transform: rotateZ(-360deg);
  }
}
@-moz-keyframes play {
  0% {
    -moz-transform: rotateZ(0deg);
  }
  100% {
    -moz-transform: rotateZ(-360deg);
  }
}
@keyframes play {
  0% {
    transform: rotateZ(0deg);
  }
  100% {
    transform: rotateZ(-360deg);
  }
}
```

### 侧栏
编辑主题配置文件中的sidebar.display值，设置侧栏显示时机为,四种选项如下
```
    post - 默认行为，在文章页面（拥有目录列表）时显示
    always - 在所有页面中都显示
    hide - 在所有页面中都隐藏（可以手动展开）
    remove - 完全移除
```
设置为hide（我比较喜欢这种）
```
sidebar:
  display: post
```

### 添加标签页面
1. 新建页面  
在终端窗口下，定位到 Hexo 站点目录下。使用 hexo new page 新建一个页面，命名为 tags ：
```
$ cd blog
$ hexo new page tags
```
2. 设置页面类型  
编辑刚新建的页面，位于blog/source/tags,将页面的类型设置为 tags ，主题将自动为这个页面显示标签云。页面内容如下：
```
title: 
date: 2014-12-22 12:39:04
type: "tags"
```
3. 修改菜单
在菜单中添加链接。编辑 主题配置文件 ， 添加 tags 到 menu 中，如下:
```
menu:
  home: /
  archives: archives
  tags: tags
```

### 添加关于页面
添加方式与标签页面相似，只需将步骤中的tags换成about即可  
关于页面的描述在blog/source/about中修改，修改如下
```
---
title: 
date: 2018-04-17 20:30:04  
---
 {% cq %}
## 心之所向  
## 素履以往   
## 生如逆旅  
##  一苇以航
{% endcq %}
```
其中，`{% cq %}`和`{% endcq %}`的作用是使中间四行文字居中，中间的文字可以替换为你喜欢的话

### 侧边栏社交链接
编辑主题配置文件social字段即可，需启用的链接取消行首的`#`
```
social:
  GitHub: https://github.com/shuzang || github
  YouTube: https://www.youtube.com/ || youtube
```

### 友情链接
编辑主题配置文件links部分即可，`links_title`为友链这部分总的名称，links_layout是排版方式，links下添加相应网站即可
```
# Blog rolls
links_icon: link
links_title: 神奇的链接
#links_layout: block
links_layout: inline
links:
  哔哩哔哩: https://www.bilibili.com/ 
  倾城之链: https://nicelinks.site/
  茶杯狐: https://www.cupfox.com/
```

### 站点建立时间
这个时间将在站点的底部显示，编辑主题配置文件，修改字段 since 
```
footer:
  # Specify the date when the site was setup.
  # If not defined, current year will be used.
  since: 2018
```

### 设置[阅读全文]
在文章中使用 `<!-- more -->` 手动进行截断

### 修改文章底部标签样式
原标签样式为`#`  
修改模板`/themes/next/layout/_macro/post.swig`，搜索 `rel="tag">#`，将` # `换成`<i class="fa fa-tag"></i>`  
修改后标签样式为一个书签图标

### 在回到顶部按钮里显示阅读百分比
编辑主题配置文件,修改scrollpercent值为true
```
  # Scroll percent label in b2t button.
  scrollpercent: true
```

### 代码高亮设置
修改主题配置文件highlight_theme值，有五种选择,在下面的Available values中列出来了，具体什么样可以看参考链接[1]的官方使用文档，我喜欢night
```
# Code Highlight theme
# Available values: normal | night | night eighties | night blue | night bright
# https://github.com/chriskempson/tomorrow-theme
highlight_theme: night
```
### 其它有趣的功能
总结一些有趣的功能，但与我来说暂时不需要的
- 在左上角或右上角实现fork me on github
- 添加动态背景
- 在网站底部添加访问量和字数统计
- 设置网站图标Favicon
- 文章加密访问
- 博文置顶
- 开启打赏功能
- 侧边栏推荐阅读
- 鼠标点击效果
- 点击侧栏头像回到主页
- 域名绑定，将github博客和自己的独有域名绑定
- 侧栏加入已运行时间
- 加快网站加载速度

## 参考链接
前三篇是主要参考
- [next官方使用文档](http://theme-next.iissnan.com/getting-started.html)  
- [打造个性超赞博客Hexo+NexT+GithubPages的超深度优化](https://reuixiy.github.io/technology/computer/computer-aided-art/2017/06/09/hexo-next-optimization.html)
- [hexo的next主题个性化教程:打造炫酷网站](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)
- [github的Next项目地址](https://github.com/theme-next/hexo-theme-next)
- [关于HEXO搭建个人博客的点点滴滴](https://juejin.im/post/5a6ee00ef265da3e4b770ac1)
- [适合在Markdown里面使用的emoji](https://www.cnblogs.com/cgzl/p/7635739.html)