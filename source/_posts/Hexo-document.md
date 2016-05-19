---
title: ［转载］Hexo 配置文档
date: 2016-05-19 10:36:20
category: 建立博客
tags: hexo
---

# 开始
## 安装

```bash
$ cd my-blog
$ git clone git@github.com:forsigner/fexo.git themes/fexo
```

## 启用

打开博客根目录的  `_config.yml`  设为  `theme: fexo`
## 升级

```bash
$ cd themes/fexo
$ git commit -am 'update'
$ git pull
```

# 配置主题
主题配置全部在 `theme/fexo` 里面完成，所里下面所有配置指的是配置`theme/fexo/_config.yml。`

## 设置基本信息

```yml
blog_name: Forsigner
slogan: Find the bug of the world
```

## 设置头像

```yml
# relative url
avatar: /images/avatar.jpg
# or absolute url
avatar: https://avatars0.githubusercontent.com/u/2668081?v=3&s=460
```

## 设置favicon

```yml
favicon: /favicon.ico
```

## 设置关键词
关键词主要作用是优化SEO

```yml
keywords: forsigner,前端,设计,Hexo主题,前端开发,用户体验,设计,frontend,design,nodejs,JavaScript
```

## 设置首页内容
你可以设置是否在首页直接显示文章

```yml
init_page_content: HOME_NAV  # HOME_NAV | POST
```

## 设置首页导航

```yml
home_nav:
  - name: Blog
    url: /archives
  - name: Github
    url: https://github.com/forsigner
    target: _blank
  - name: Douban
    url: http://www.douban.com/people/forsigner/
    target: _blank
  - name: Twitter
    url: https://twitter.com/forsigner
    target: _blank
```

## 设置页面导航

```yml
page_nav:
  - 博客: /archives/
  - 分类: /category/
  - 标签: /tag/
  - 友链: /link/
  - 关于: /about/
  - RSS: /atom.xml
```

## 设置页面导航样式

```yml
page_nav_style: CIRCLE  # CIRCLE|ROUND_RECT
```

## 设置面包屑

```yml
breadcrumb:
  isShow: true # true|fase
```

## 设置盒子
你可设置盒子是否显示和其显示的文字

```yml
toolbox:
  isShow: true # true|fase
  text: 盒子
```

## 搜索页面 Slogan

```yml
search_slogan:
  isShow: true # true|fase
  text: Can you find the bug of world ~
```

## 友链页面 Slogan

```yml
link_slogan:
  isShow: true # true|fase
  text: 交换友链可以邮件 forsigner@gmail.com
```

## 设置文章标题对齐方式

```yml
post:
  header_align: center # left|center
```


# 启用页面
你可以启用你想要的页面，在开启关于、友链、项目的页面后，你可以对这些设置这些页面的内容

## 启用分类页面
在博客根目录执行 `hexo new page category`
修改 `my-blog/source/category/index.md` 里面的内容:

```md
---
title: category
layout: category
comments: false
---
```

## 启用标签页面
在博客根目录执行 `hexo new page tag`
修改 `my-blog/source/tag/index.md` 里面的内容:

```md
---
title: tag
layout: tag
comments: false
---
```

## 启用友链页面
在博客根目录执行 `hexo new page link`
修改 `my-blog/source/link/index.md` 里面的内容:

```md
---
title: link
layout: link
comments: false
---
```

启用友链页面后，可以设置类似以下格式的内容

```yml
link:
  - name: 织网
    info: 身体和灵魂，总有一个在路上
    url: http://zheng-ji.info/
    avatar: https://avatars3.githubusercontent.com/u/1414745?v=3&s=460
  - name: Dongyado
    info: 生命不止，折腾不息
    url: http://dongyado.com/
    avatar: https://avatars0.githubusercontent.com/u/6274940?v=3&s=460
  - name: OrangeCoder
    info: android ffmpeg nodejs gradle
    url: http://orangecoder.com/
    avatar: https://avatars0.githubusercontent.com/u/2263785?v=3&s=460
  - name: EverET
    info: 好记性不如烂笔头
    url: http://everet.org/about-me/
    avatar: https://avatars1.githubusercontent.com/u/1559563?v=3&s=460
```

## 启用关于页面
在博客根目录执行 `hexo new page about` 
修改 `my-blog/source/about/index.md` 里面的内容:

```md
---
title: about
layout: about
comments: false
---
```

启用关于页面后，可以设置类似以下格式的内容:

```yml
about:
  - type: me
    icon: icon-user
    text_value:
    - "Scut，1991，Spring."
    - "喜欢设计，擅长编程，喜欢睡懒觉."
    - "前端开发工程师，常用 HTML / CSS / JavaScript."
  - type: Github
    icon: icon-github
    text_key: Github
    text_value: "@forsigner"
    text_value_url: https://github.com/forsigner
  - type: weibo
    icon: icon-weibo
    text_key: 微博
    text_value: "@forsigner"
    text_value_url: http://weibo.com/u/1847075964
  - type: mail
    icon: icon-mail
    text_key: Gmail
    text_value: "forsigner@gmail.com"
  - type: location
    icon: icon-location
    text_value: 珠海
```

## 启用项目页面
在博客根目录执行 `hexo new page project`
修改 `my-blog/source/project/index.md` 里面的内容:

```md
---
title: project
layout: project
comments: false
---
```

启用项目页面后，可以设置类似以下格式的内容


```yml
project:
  - type: personal
    name: fexo
    url: https://github.com/forsigner/fexo
    intro: A minimalist design theme for hexo
  # - type: company
  #   name: Fexo
  #   url: https://github.com/forsigner/fexo
  #   intro: A minimalist design theme for hexo
  - type: personal
    name: beside
    url: https://github.com/forsigner/beside
    intro: I need you beside me
  - type: personal
    name: web-fontmin
    url: https://github.com/forsigner/web-fontmin
    intro: 字体子集化，在线提取你需要的字体
  - type: personal
    name: magic-check
    url: https://github.com/forsigner/magic-check
    intro: Beautify Radio and Checkbox with pure CSS
  - type: personal
    name: nice-bar
    url: https://github.com/forsigner/nice-bar
    intro: A nice and lightweight scrollbar
  - type: personal
    name: angular-nice-bar
    url: https://github.com/forsigner/angular-nice-bar
    intro: A nice and lightweight scrollbar in Angular
```


## 启用搜索页面
在博客根目录执行 `hexo new page search`
修改 `my-blog/source/search/index.md` 里面的内容:

```md
---
title: search
layout: search
comments: false
---
```

然后安装 Hexo 插件 hexo-search (重要)

先进入 blog 的根目录

```bash
$ cd my-blog
$ npm install hexo-search --save
```

个性化设置的部分见原文链接

原文链接：[Fexo 文档](http://forsigner.com/2016/03/10/fexo-doc-zh-cn/)

