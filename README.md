# 我的博客搭建




## 编辑环境
需要安装jekyll，本地浏览器预览主题：`jekyll serve`
参考文档：[using jekyll with pages](https://help.github.com/articles/using-jekyll-with-pages/) & [Upgrading from 2.x to 3.x](http://jekyllrb.com/docs/upgrading/2-to-3/)

##  界面修改
#### get start
通用属性在_config.yml文件中

```
# Site settings
title:              # 博客网站标题
SEOTitle: 		    # 在后面会详细谈到
description: "Cool Blog"    # 随便说点，描述一下

# SNS settings      
github_username:      # github账号
weibo_username:       # 微博账号，底部链接会自动更新的。

# Build settings
# paginate: 10         # 一页准备放几篇文章
```
Jekyll官方网站还有很多的参数可以调：[Jekyll中文](http://jekyllcn.com/).

#### write-posts

要发表的文章一般以markdown的格式放在这里`_posts/`

yaml 头文件长这样:

```
---
layout:     post
title:      "Hello 2015"
subtitle:   "Hello World, Hello Blog"
date:       2015-01-29 12:00:00
author:     ""
header-img: "img/post-bg-2015.jpg"
tags:
    - Life
---

```

#### SideBar

设置是在 `_config.yml`文件里面的`Sidebar settings`那块。
```
# Sidebar settings
sidebar: true  #添加侧边栏
sidebar-about-description: "简单的描述一下你自己"
sidebar-avatar: /img/avatar-hux.jpg     #作者头像，请使用绝对地址.
```

侧边栏是响应式布局的，当屏幕尺寸小于992px的时候，侧边栏就会移动到底部。具体请见bootstrap栅格系统 <http://v3.bootcss.com/css/>


#### Mini About Me

Mini-About-Me 这个模块将在你的头像下面，展示你所有的社交账号。这个也是响应式布局，当屏幕变小时候，会将其移动到页面底部，只不过会稍微有点小变化，具体请看代码。

#### Featured Tags

[Medium](http://medium.com) 
这个模块现在是独立的，可以呈现在所有页面，包括主页和发表的每一篇文章标题的头上。

```
# Featured Tags
featured-tags: true  
featured-condition-size: 1     # A tag will be featured if the size of it is more than this condition value
```

唯一需要注意的是`featured-condition-size`: 如果一个标签的 SIZE，也就是使用该标签的文章数大于上面设定的条件值，这个标签就会在首页上被推荐。
 
内部有一个条件模板 `{% if tag[1].size > {{site.featured-condition-size}} %}` 是用来做筛选过滤的.


#### Friends

好友链接部分。这会在全部页面显示。

设置是在 `_config.yml`文件里面的`Friends`那块，自己加吧。

```
# Friends
friends: [
    {
        title: "Foo Blog",
        href: "http://foo.github.io/"
    },
    {
        title: "Bar Blog",
        href: "http://bar.github.io"
    }
]
```


#### Keynote Layout

HTML5幻灯片的排版：

![](http://huangxuan.me/img/blog-keynote.jpg)

用于占用html格式的幻灯片，一般用到的是 Reveal.js, Impress.js, Slides, Prezi 等等.

其主要原理是添加一个 `iframe`，在里面加入外部链接。

可以直接写到头文件里面去，详情请见下面的yaml头文件的写法。

```
---
layout:     keynote
iframe:     "http://huangxuan.me/js-module-7day/"
---
```

#### Comment
博客不仅支持多说Duoshuo评论系统，也支持Disqus评论系统。

多说开发者文档 http://dev.duoshuo.com/docs/5003ecd94cab3e7250000008 。

yaml头文件设置
```
duoshuo_username: _你的用户名_
或者
disqus_username: _你的用户名_
```
最后多说是支持分享的，如果你不想分享，请这样设置：duoshuo_share: false。


#### 其他可编辑属性
```
Customization

Header Image

SEO Title
```
##### 致谢
This theme forked of [Hux Blog](https://github.com/Huxpro/huxpro.github.io)

原始模板作者：[IronSummitMedia/startbootstrap-clean-blog-jekyll](https://github.com/IronSummitMedia/startbootstrap-clean-blog-jekyll)  

