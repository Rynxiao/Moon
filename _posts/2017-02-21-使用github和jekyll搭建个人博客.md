---
layout: post
title:  "使用github+jekyll搭建个人博客"
date:   2017-02-31
excerpt: "搭建博客之后的第一篇文章——记录我使用github+jekyll搭建个人博客的经历。"
tag:
- jekyll 
- github
- blog
comments: true
---

## 聊聊起初

每次看到大牛们的博客，都会激起一颗一定要搭建自己博客的心，毕竟有着一颗向大牛们看齐的心。但是一直不知道如何下手，从最初的csdn写写博客到在github上建立仓库写代码分享，虽然也能够记录一些事情，但是总感觉缺少点什么——对，就是像是这东西并不是自己的感觉。后来偶然机会知道了github的gh-pages功能可以搭建个人博客，然后兴致冲冲地去折腾了一番，但是了解到并不能搭建后台，突然间又像浇了一盘冷水一样，知道现在都还存留着这个博客的残骸，看这里[http://rynxiao.github.io/blog/#/](http://rynxiao.github.io/blog/#/)。
之前是想着用react搭建前台页面，后台用bmob，但是放置久了，心也就冷了，索然不做了。最近才发现原来github的gh-pages也可以使用jekyll来搭建，好吧，怪自己孤陋寡闻。然后就试着了解了一下jekyll，也就是这博客由来的结果。

## 经历过程

闲话说了，聊聊经历过程吧，顺便记录自己踩下的坑。本人是在`windows`上进行操作，至于其他平台上的操作，请小伙伴们自行搜索。

### 安装ruby以及ruby相关工具(DevKit)

由于jekyll是基于ruby语言开发的，因此我们需要安装ruby以及ruby相关的工具(DevKit)。具体的ruby可以到[官网](http://www.ruby-lang.org/en/downloads/)上去下载，不过毕竟是国外网站，如果没有好的翻墙工具还是比较慢的。这里我已经准备好了，点[ruby](http://pan.baidu.com/s/1eSNz3iE)和[DevKit](http://pan.baidu.com/s/1csz3uY)下载。点击exe文件进行自定义目录安装。安装完成之后，确保ruby的环境已经配置到了系统的变量中。比如我的DevKit安装目录是：D:\develop\DevKit。进入DevKit目录，输入如下命令：

{% highlight cmd %}
C:\Users> cd D:\develop\DevKit
C:\Users> D:
D:\develop\DevKit> ruby dk.rb init
D:\develop\DevKit> ruby dk.rb install
{% endhighlight %}

可以使用`gem -v` 和 `ruby -v`来确认是否已经安装成功

![Markdown](http://p1.bpimg.com/572179/509e513d9975bf36.png)

### 更改gem sources

使用`gem sources`发现是`https://rubygems.org/`，国外网站的通病就是下载很慢，因此我们需要替换一个国内的源。

{% highlight cmd %}
gem sources -add https://gems.ruby-china.org/ --remove https://rubygems.org/ 替换源
gem sources -u 更新缓存
gem sources 查看替换后的源
{% endhighlight %}

![Markdown](http://p1.bpimg.com/572179/d6344eefc5dd1f10.png)

看到更新之后的源被替换成了`http://gems.ruby-china.org/`，没错，就是`http`，我试了用`https`一直是不成功的。

### 安装jekyll

经过上面两步之后，我们就可以安装jekyll了。调用命令：

{% highlight cmd %}
gem install jekyll
{% endhighlight %}

之后使用`jekyll -v`来查看jekyll版本，可以看到我的版本是3.4.0。记录一下，本人并没有安装3.0.0以前的版本，这是在网上看到的:

> 这里稍微强调一下，这个版本和之前的2.x. x版本有些许不一样，可能在后面_config.yml的写法上可能有差异，不过没关系，这并不影响我继续前进

![Markdown](http://p1.bqimg.com/572179/fdf98aa24a27850f.png)

### 创建博客

至此我们就可以用jekyll来创建博客了，具体命令如下：

{% highlight cmd %}
jekyll new myblog
cd myblog
jekyll server
{% endhighlight %}

然后在`http://127.0.0.1:4000`端口来查看你创建的博客。

### 可能会遇到的坑

* 端口占用

![Markdown](http://p1.bqimg.com/572179/7216ad804c56adb7.png)

看到jekyll启动服务的4000端口已经被占用，我们需要找到占用的程序，然后干掉它。

{% highlight cmd %}
// 1.查看所有的端口使用情况，显示PID
netstat -ano 
// 2.找到端口被占用的PID，比如PID为14325
tasklist /svc /FI "PID eq 14325"
// 3.打开任务管理器，找到相应的程序，杀掉就好
// FoxitProtect.exe 默认会绑定4000端口，因此杀掉这个进程就行
{% endhighlight %}

如下图，正常启动如下：

![Markdown](http://p1.bpimg.com/572179/f2d176e04576a60b.png)

在浏览器中输入`127.0.0.1:4000`就可以看到我们的博客模样：

![Markdown](http://p1.bpimg.com/572179/6f8cece1235e03ea.png)
