---
title: 独立域名配置
date: 2016-05-19 15:22:07
tags: domain
---

本文是github+hexo搭建博客的第二部分，解决域名解析的问题。

## 购买域名

我选择使用的域名服务商是GoDaddy，可以使用支付宝，价格也不贵，我购买的价钱大概是60元一年。    
细节就不赘述了，GoDaddy的网站做的很简单，购买流程很顺畅。

## 将个人域名与Github Pages的空间绑定

我的本地站点名称是 hexo-site ，详细的建立过程见 [在Mac上github＋hexo搭建博客（一）](http://lilyalove.com/2016/05/09/%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99%EF%BC%88%E4%B8%80%EF%BC%89/)
在 `hexo-site\source` 文件夹里新建一个名为 `CNAME` 的文件，用`sublime` 编辑器打开，或者本地编辑器也行，添加内容 `lilyalove.com`，也就是你购买的域名，保存。
部署博客即可。

部署的方式： 
1、生成文件，用 `hexo generate` 命令
2、部署，用 `hexo deploy` 命令即可
3、记得将 `_config` 文件里面的 `url` 改为你的个人域名。

如果编译的过程都顺利的话，就部署成功了。

## DNS设置

经过朋友的推荐，我选择 DNSpod 来设置DNS，速度快、免费、且稳定。
注册过程不详谈了。

## 添加域名

如下图设置：
![add domain](http://7xnuu7.com1.z0.glb.clouddn.com/blogdnspod1.png)

方法一：
如上图所示，其中两条A记录指向的IP地址是GitHub Pages的提供的IP：
192.30.252.153
192.30.252.154

如果博客不能访问，有可能是GitHub更改了空间服务的ip地址，及时到GitHub Pages查看最新的IP即可。
www指定的记录是你在GitHub托管博客的仓库。

方法二：
不使用A记录，直接使用CNAME，记录值为 `lilyalove.com`，也就是你自己的域名即可。

## 去GoDaddy修改DNS地址

更改GoDaddy的Nameservers为DNSpod的NameServers,点击域名管理

![domain](http://7xnuu7.com1.z0.glb.clouddn.com/blogdnspod3.png)

将GoDaddy的Nameservers更改成f1g1ns1.dnspod.net和f1g1ns2.dnspod.net

![custom](http://7xnuu7.com1.z0.glb.clouddn.com/blogdnspod2.png)

最后修改成下图所示即可：

![details](http://7xnuu7.com1.z0.glb.clouddn.com/blogdnspod4.png)

有疑问可以看DNSpod提供的官方帮助。
提示：设置DNS之后短时间内可能无法访问你的个人博客，因为要等待全球递归DNS服务器刷新（最多72小时），不过没问题的话几小时内就可以访问了。


注：编写这篇文章时遇到了一个诡异的问题，如上所示，我写完文章进行 `hexo generate`时，总是提醒我有语法问题，提示如下：

```
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Template render error: (unknown path)
  SyntaxError: Unexpected token ILLEGAL
    at Object.exports.prettifyError (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/nunjucks/src/lib.js:34:15)
    at Obj.extend.render (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/nunjucks/src/environment.js:468:27)
    at Obj.extend.renderString (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/nunjucks/src/environment.js:326:21)
    at /Users/baoli/Desktop/hexo-site/node_modules/hexo/lib/extend/tag.js:66:9
    at Promise._execute (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/debuggability.js:272:9)
    at Promise._resolveFromExecutor (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:473:18)
    at new Promise (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:77:14)
    at Tag.render (/Users/baoli/Desktop/hexo-site/node_modules/hexo/lib/extend/tag.js:64:10)
    at Object.tagFilter [as onRenderEnd] (/Users/baoli/Desktop/hexo-site/node_modules/hexo/lib/hexo/post.js:253:16)
    at /Users/baoli/Desktop/hexo-site/node_modules/hexo/lib/hexo/render.js:63:19
    at tryCatcher (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:502:31)
    at Promise._settlePromise (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:559:18)
    at Promise._settlePromise0 (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:604:10)
    at Promise._settlePromises (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:683:18)
    at Async._drainQueue (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/async.js:138:16)
    at Async._drainQueues (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/async.js:148:10)
    at Immediate.Async.drainQueues [as _onImmediate] (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/async.js:17:14)
    at processImmediate [as _immediateCallback] (timers.js:383:17)
FATAL (unknown path)
  SyntaxError: Unexpected token ILLEGAL
Template render error: (unknown path)
  SyntaxError: Unexpected token ILLEGAL
    at Object.exports.prettifyError (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/nunjucks/src/lib.js:34:15)
    at Obj.extend.render (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/nunjucks/src/environment.js:468:27)
    at Obj.extend.renderString (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/nunjucks/src/environment.js:326:21)
    at /Users/baoli/Desktop/hexo-site/node_modules/hexo/lib/extend/tag.js:66:9
    at Promise._execute (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/debuggability.js:272:9)
    at Promise._resolveFromExecutor (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:473:18)
    at new Promise (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:77:14)
    at Tag.render (/Users/baoli/Desktop/hexo-site/node_modules/hexo/lib/extend/tag.js:64:10)
    at Object.tagFilter [as onRenderEnd] (/Users/baoli/Desktop/hexo-site/node_modules/hexo/lib/hexo/post.js:253:16)
    at /Users/baoli/Desktop/hexo-site/node_modules/hexo/lib/hexo/render.js:63:19
    at tryCatcher (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:502:31)
    at Promise._settlePromise (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:559:18)
    at Promise._settlePromise0 (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:604:10)
    at Promise._settlePromises (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/promise.js:683:18)
    at Async._drainQueue (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/async.js:138:16)
    at Async._drainQueues (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/async.js:148:10)
    at Immediate.Async.drainQueues [as _onImmediate] (/Users/baoli/Desktop/hexo-site/node_modules/hexo/node_modules/bluebird/js/release/async.js:17:14)
    at processImmediate [as _immediateCallback] (timers.js:383:17)
```

这个问题我查了半天，都没有合理的解答，而且我逐字逐句的检查了一遍文章的语法，也没有发现问题。
于是我用了一个蠢办法，我把整篇文章一点一点地复制粘贴，然后生成。想看看到底哪句话有语法问题。
结果整篇文章生成成功了。。。
表示心真累。
现状就是我成功生成了文章，但并不知道之前到底出了什么问题。。。hexo不会是看心情编译吧。。。求看到问题的大神给我一个解答，多谢。


