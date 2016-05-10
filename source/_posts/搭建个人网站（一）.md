---
title: 在Mac上github＋hexo搭建博客（一）
date: 2016-05-09 09:35:06
tags: 技术
---

本文是在 Mac 上 github＋hexo 搭建博客第一部分，解决的问题是将本地搭建的博客在Github上跑起来。

## github 、hexo简介
- github：开源代码库以及版本控制系统，其中githubpages提供300M的免费空间，拿来做博客够用了。
- hexo：是一个快速、简洁且高速的静态页面发布框架，使用Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页

本人搭建的各人博客采用gitHub ＋ hexo来搭建。

## 需要下载的软件
- [Homebrew](http://brew.sh/)
Homebrew是Mac的软件管理工具，使用起来十分方便。虽然并不是建站的必备软件，但还是可以先下载一个，事半功倍。
按照 http://brew.sh/ 里面提示的方法一步步进行安装即可。    
问题：我安装Homebrew的时候总是安装不成功，目测是我先安装了Xcode，但是Xcode的路径有问题，按照默认路径寻找相关的文件总是找不到，于是安装不成功。大家如果也遇到安装不成功的问题，可以仔细看一下提示，再做后续操作。

- Xcode
Xcode是运行在操作系统Mac OS X上的集成开发工具（IDE），预先下载一个，免得编译的时候出现问题。可以在App Store进行下载。

- [node.js](https://nodejs.org/en/)
hexo的官方文档给的最佳下载方式是使用 [nvm](https://github.com/creationix/nvm)。    
具体操作命令参考[hexo](https://hexo.io/zh-cn/) 安装 node.js 即可。
我在这里使用的是直接下载[安装包](https://nodejs.org/en/)。    
node.js 下载完成后 安装到电脑上就可以了。安装成功后显示出来安装路径，可以看到 安装node.js 的时候 npm 也安装了。
如图所示：
![node.js](http://upload-images.jianshu.io/upload_images/326377-5868656ecedf7e76.png?imageMogr2/auto-orient/strip%7CimageView2/2)

- 安装[git](https://sourceforge.net/projects/git-osx-installer/)
可以使用Homebrew进行安装，也可以直接使用[安装程序](https://sourceforge.net/projects/git-osx-installer/)。

- [hexo](https://hexo.io/zh-cn/) 
成功安装 node.js 和 git 之后，就可以安装hexo了。

```
$ npm install -g hexo-cli
```

**使用命令行装软件的时候 ，当前在哪个路径下，就会装到哪个路径下。 系统的软件除外。 hexo 和 npm 安装的时候有默认路径因此我们不用特意去创建安装文件夹。**    
注意： hexo的时候可能会出现这样的错误

```
{ [Error: Cannot find module './build/Release/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/default/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/Debug/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
```

原因是 我国防火墙网络墙的问题，导致安装的时候少装了几个库。 解决方法，换一个源重新装:

```
$ npm install hexo --no-optional
```

hexo 下载完成后 运行一下 看是否安装成功

```bash
$ hexo -v
```

hexo 安装成功后，我们开始使用 hexo 建站。

## 建立本地站点
安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

新建完成后，指定文件夹的目录如下：


.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes



**\_config.yml**
网站的配置信息，您可以在此配置大部分的参数。

本地站点建立成功后，可以cd 进入站点文件夹，然后 执行 hexo server 启动站点

```bash
$ hexo server
```

站点默认端口为 http://0.0.0.0:4000
在浏览器中 输入 http://0.0.0.0:4000 就可以看到 站点了。

## github上创建GitHubPages仓库
git 官方参考地址: https://pages.github.com

*注意:创建仓库的时候仓库名一定严格按照 git用户名.github.io 来命名*

## 部署
把public 文件里面的文件，推送到我们 的github仓库里。
注意： 不要包含 public 文件夹，只推送 文件里面的文件即可。

**方法如下:**

```bash
$ hexo deploy
```

在开始之前，您必须先在 _config.yml 中修改参数，一个正确的部署配置中至少要有 type 参数，例如：

```config
deploy:
－ type: git
```

**Git**
安装 hexo-deployer-git

``` bash
$ npm install hexo-deployer-git --save
```

修改配置。
在上面提到的 _config.yml 文件中修改 deploy 的参数，包括 

```config
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
  message: [message]
```


参数 | 描述
--------- | -------------
repo | 库（Repository）地址
branch | 分支名称。如果您使用的是 GitHub 或 GitCafe 的话，程序会尝试自动检测。
message | 自定义提交信息 (默认为 Site updated: &lbrace;&lbrace; now('YYYY-MM-DD HH:mm:ss') &rbrace;&rbrace;)

配置完之后就可以用

```bash
$ hexo deploy
```
来进行github的同步了。
同步完之后，在浏览器中输入：http://bilove.github.io/ 就可以看到搭建的静态网站了。


## 使用github保存源码

- 在github中建立一个新的repository，我将其命名为 mysite.src ，意味这里保存的是我的个人博客的源码。 
- 进入hexo所建立的本地站点对应的文件夹，源码所包含的文件上面的文章中有描述
- 使用git进行源码上传
- git status ：查看状态
- git init ： 首次上传时进行初始化
- git add 文件／文件夹 ： 添加需要上传的文件
- git commit “更新备注”
- git log 查看日志
- git push 放到git上
- git pull 把远程修改合并到本地

## 新建一篇文章

你可以执行下列命令来创建一篇新文章。

```bash
$ hexo new [layout] <title>
```

接着用MWeb打开进行编辑即可。
Markdown的语法在网上进行学习即可。

## 发布写完的文章

**生成文件**
使用 Hexo 生成静态文件快速而且简单。

```bash
$ hexo generate
```

**监视文件变动**
Hexo 能够监视文件变动并立即重新生成静态文件，在生成时会比对文件的 SHA1 checksum，只有变动的文件才会写入。

```bash
$ hexo generate --watch
```

**完成后部署**
您可执行下列的其中一个命令，让 Hexo 在生成完毕后自动部署网站，两个命令的作用是相同的。

```bash
$ hexo generate --deploy
$ hexo deploy --generate
```

