---
title: 使用七牛来储存博客图片
date: 2016-05-21 13:54:34
category: 建立博客
tags: 技术
---

# [七牛](http://www.qiniu.com/)
![](http://o7i9sckjd.bkt.clouddn.com/static/images/Use-Qiniu-to-store-image/qiniu.png)
七牛提供10g的永久免费存储空间以及每月10GB的下载流量，完全够一个小小的个人博客使用了。
而且，就我个人注册和配置过程来看，七牛操作起来很简便，很省事

# 如何配置

## 在七牛上建立自己的空间
![](http://o7i9sckjd.bkt.clouddn.com/static/images/Use-Qiniu-to-store-image/qiniu-space.png)
选择第一项 **对象存储**，设置自己的空间名称，找到外链默认域名，我的是o7i9sckjd.bkt.clouddn.com。

上传一张图片到七牛上，比如me.png，则可以通过以下链接来进行访问

```
http://o7i9sckjd.bkt.clouddn.com/me.png 
```

## 在hexo中安装[hexo-qiniu-sync](https://github.com/gyk001/hexo-qiniu-sync)插件

这是一个hexo插件， 可以让你在文档中入嵌存储在七牛上的图片、JS、CSS类型的静态文件。

你可以不用手动上传文件到七牛，插件会自动帮你将本地目录的文件同步到七牛。

## 安装
在本地的hexo主目录下运行以下命令进行安装：

```
npm install hexo-qiniu-sync --save
```

添加插件配置信息到 `_config.yml` 文件中:

```
plugins:
  - hexo-qiniu-sync

#七牛云存储设置
##offline       是否离线. 离线状态将使用本地地址渲染
##sync          是否同步
##bucket        空间名称.
##access_key    上传密钥AccessKey
##secret_key    上传密钥SecretKey
##dirPrefix     上传的资源子目录前缀.如设置，需与urlPrefix同步 
##urlPrefix     外链前缀. 
##local_dir     本地目录.
##update_exist  是否更新已经上传过的文件(仅文件大小不同或在上次上传后进行更新的才会重新上传)
##image/js/css  子参数folder为不同静态资源种类的目录名称，一般不需要改动
##image.extend  这是个特殊参数，用于生成缩略图或加水印等操作。具体请参考http://developer.qiniu.com/docs/v6/api/reference/fop/image/ 
##              可使用基本图片处理、高级图片处理、图片水印处理这3个接口。例如 ?imageView2/2/w/500 即生成宽度最多500px的缩略图
qiniu:
  offline: false
  sync: true
  bucket: bucket_name
  access_key: AccessKey
  secret_key: SecretKey
  dirPrefix: static
  urlPrefix: http://bucket_name.qiniudn.com/static
  local_dir: static
  update_exist: true
  image: 
    folder: images
    extend: 
  js:
    folder: js
  css:
    folder: css
```

## 注意

1. 一定要注意缩进的问题。不能用tab来缩进，要用两个空格。
2. access_key和secret_key可以从七牛的“个人面板－密钥管理”里面找就可以了；
3. local_dir一定要写static文件夹的准确路径，这个文件夹可以放在任何位置，设置好之后，在static里面存储你要同步到七牛的文件即可；

配置完成后，使用 `hexo generate` 生成即可。

生成后，会在static的文件夹里生成三个文件夹：image，js，css；
可以按照单独的博客名来建立文件夹，给图片分类。
例如本文的title是Use-Qiniu-to-store-image，我会在image文件夹里再建一个Use-Qiniu-to-store-image的文件夹，再把本文的图片放到这个文件夹里就好了。

## 同步图片到七牛
放好图片后，在hexo中输入

```
hexo qiniu sync
``` 

就可以同步图片到七牛了

## 获取图片外链

![](http://o7i9sckjd.bkt.clouddn.com/static/images/Use-Qiniu-to-store-image/outchain.png)

1. 在高级设置里面把访问控制改为公共空间；
2. 把原文件保护关闭，则可以进入个人空间－内容管理了；
3. 在图片列表里面获取文件的外链即可，如下图所示

![](http://o7i9sckjd.bkt.clouddn.com/static/images/Use-Qiniu-to-store-image/outside-chain.png)

使用hexo写博客的时候，在七牛上找到对应图片的外链，再用 `![]()` 的方式使用图片即可。

