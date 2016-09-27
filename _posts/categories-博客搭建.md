---
layout: post
title: 博客搭建相关
description: 一个超级小白的个人网站搭建之路
date: 2016-07-07 02:46:04 +08:00
categories:博客搭建
---
# 博客搭建相关
***
## 搭建想法
其实一开始是不准备搭自己的博客的，但是耐不住某人的怂恿以及域名实在太便宜了以及CDNS实在太丑，开始搭建这个博客。有了它，希望自己能做到每天写一点东西来学习吧，对，只是希望而已。
***
## 相关工具
* 一个域名

* github账号

* git bash的基本操作

* markdown的基本操作

该博客使用了gitHub pages+Jekyll，整个网站托管在github上，使用GitHub提供的静态页面生成技术以及免费的300Mb空间。
***
## 时间轴
* 购买域名
* 学习和设置github账号
* fork Jekyll模板
* 学习git bash操作
* fork Jekyll模板
* 学习配置文件更改
* github生成CNAME文件绑定域名
* 万网上解析域名
* 撰写此篇博文
* 推送至github上

接下来尽量写出我遇到的所有问题，按照时间轴顺序。

可参考[这篇博客](http://chiahao.top/2016/06/28/Blog)与[另一个博客](http://www.jianshu.com/p/05289a4bc8b2/).
***
## 域名购买
我是在[万网](https://wanwang.aliyun.com/?utm_medium=text&utm_source=bdbrandww&utm_campaign=bdbrand&utm_content=se_103066)上购买的域名，万网在阿里云旗下，可用淘宝账号登录，万网还提供新手解析服务,并且现在top域名首年只要4元还支持支付宝，不信你不心动，此步没有困难

## 学习和设置github账号
身为一个程序猿，我心中有愧，我才申请的github账号，我自我反思三秒钟。

先是对github的理解，也就是了解github到底是什么，且看[这篇知乎](https://www.zhihu.com/question/20070065),其中珊珊是个小太阳介绍的生动有趣，深的我心。可以看着[这里](http://jingyan.baidu.com/article/455a9950abe0ada167277864.html)来注册github账号，这里可以更改个人信息（[看这](http://jingyan.baidu.com/article/ff42efa93b2ed6c19e22021c.html)），一开始我因为忘记注册邮箱后来查不出问题那叫一个心累啊。

简言之，github就是一个仓库，你可以把别人家的东西快速复制下来并更改推送。

## git bash相关
这就是一个简单的把你本地文件与github上的文件联系起来的工具，基本操作[看这](https://wuyuans.com/2012/05/github-simple-tutorial/)

之后要把你的git bash与你的github账号绑定，[看这](http://www.cnblogs.com/zichi/p/4703999.html)。当然可以参考[官方介绍](https://help.github.com/articles/set-up-git/).

首先使用git bash是要设置用户名以及绑定邮箱的，之后使用公钥SSH将你的git bash与github绑定，然后学习一下git bash的基本操作。

然后记着一下三条操作，就可以先应付简单的文件上传了。还有这篇boss级总介绍——[Git参考手册](http://gitref.org/zh/index.html)。以下三条操作是直接复制[这里](http://chiahao.top/2016/06/28/Blog)的，懒得自己写了。

* *添加更改信息*：git add .此处是为GitHub添加更改信息，方便版本管理
* *添加提交信息*：git commit -m 'balabala'其中balabala为你需要进行的对此次更改的描述
* *推送到远程仓库*：git push origin master
* *查看仓库*：git remote.起码会有一个origin仓库
* 
如果远程仓库发生更改但本地仓库未发生更改，则会导致推送失败。此时应先用git pull命令保证同步，或者如果有足够的理由，可以使用git push -f origin master进行强制推送，此时远程仓库会被本地仓库所覆盖。 推送完成后，等几分钟刷新一下，新的博文就会出来了。

## fork Jekyll模板
在刚刚的github的介绍里，我们已经看到了github的作用，现在，我们就去[Jekyll](http://jekyllthemes.org/)的模板上挑选一套自己喜欢的fork下来。当然，也可以使用github自己生成页面自己搭建也是很好的，为了漂亮，使用了模板。

fork下来的第一件事，就是改名。在你的github账户下将项目名字改为**username.github.io**（username是你的名字啦，不要太傻~），很重要，千万要记得改，不然会不识别的。

然后就可以把网站下到本地来啦，用git bash就可以了，或者使用GitHub Desktop都可以。

## 配置文件
这里搞得我真是头大啊。。。。

* _includes：默认的在模板中可以引用的文件的位置，后面会提到
* _layouts：默认的公共页面的位置，后面会提到
* _posts：博客文章默认的存放位置
* .gitignore：git将忽略这个文件中列出的匹配的文件或文件夹，不将这些纳入源码管理
* _config.yml：关于jekyll模板引擎的配置文件
* index.html：默认的主页
我fork的模板内很贴心的给了提示
参考以下的文章，[知乎问答](https://www.zhihu.com/question/30018945),以及[这里](http://www.jianshu.com/p/609e1197754c)，还有[这](http://wenku.baidu.com/link?url=EPw34MKdp0A2diuScToIdx9lBEAXPl7jrNdQvy-fzISeJyy80HBTma0p103jvfgQytuRPA2ZJ_OyIDf1pHos1az7nI1wO2um99_8rqi2l9y)。


##github生成CNAME文件绑定域名
如果没有CNAME文件，那就自己创建一个，有的话直接将里面的域名修改为你自己的域名即可。参考[这里](http://jingyan.baidu.com/article/dca1fa6fa1e403f1a5405262.html)。

很奇怪的是我的项目并没有被github认为是自己的个人主页，正在努力。
* 即使是fork也建议学一下Jeyll的搭建，了解每个文件的作用。[看这](http://www.ezlippi.com/blog/2015/03/github-pages-blog.html)。
* 被人fork之后自己的*username.github.io*的ip是会改变的，所以建议全部搞定之后再去ping自己*username.github.io*的ip，再解析至万网上。

## 万网上解析域名
万网上提供解析域名服务，进域名管理那即可，十分友好。可以直接选择旁边的新手一键解析，但是要自己提供IP地址。用cmd ping一下你在github上的pages即可，像我就是`ping -t celery-gu.github.io`。其他的高级设置反正我也看不懂，不管了。

## 撰写此篇博文
此篇博文采用的是markdown语言撰写，该语言简单易懂，十分好用，可参考[这里](http://www.jianshu.com/p/1e402922ee32)。

本人采用的软件是作业部落，长得十分美好，对于我这种软件颜控来说是福利。而且提供了JEKYLL PAGE的开头，直接修改就好，十分美好。

## 推送至github上
直接把博文放到`_posts`文件夹内，然后打开git mash发送`git push origin master`回车，如果又出现`hint: 'git pull ...') before pushing again.`，那就先发送`git pull origin master`，表示先合并内容，再接着push自己的内容上去，还可以强制使用`git push -f origin master`发送。（这就是上面讲的配置文件那里。)

有一点小注意，看此时操作的地方是否为主页所在的地方。我之前没注意的时候是在对C盘尽心操作，实际上我的blog放在了E盘，如果无法操作先观察一下，可以用`cd E:/blog/gubiqin.github.io`跳转到我需要操作的文件夹内，才能继续操作。

[git bash](http://my.oschina.net/chinacion/blog/655718)的相关操作。

 - 须把文件放在`master`分支下，[分支合并](https://git-scm.com/book/zh/v2/Git-%E5%91%BD%E4%BB%A4-%E5%88%86%E6%94%AF%E4%B8%8E%E5%90%88%E5%B9%B6)。
 - 我这里合并时还出了点问题，吐槽里说
***
## 点点吐槽
* 为了搞这个我熬夜了。。。这样不好
* 蚊子很厉害，我今晚打了不下十次，一只也没打中，也亏它们我都没能打个瞌睡。
* 英语很重要，看github的时候宛如看天书，操作也是全英的，虽然命令都很简单，但是。。。。总之，信息安全中的英语基础大课堂开课啦。
* 这个做了好久啊，被怼了好多次
* 一开始申请的github账号说我不是人，发邮件认证也没有。后来一想，反正也没有多少东西，就重新申请一个账号，结果git bash绑定的是前一个账号，所以老是push没有用，为这个错误几个月都没查出来。。。当然我也没仔细查。。。后来重新绑定了git bash和账号。。。唉。。。





















