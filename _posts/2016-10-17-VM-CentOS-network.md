---
layout: post
title: VMware虚拟机下的CentOS7.0网络设置
categories: Linux
description: 虚拟机中CentOS的网络设置
keywords: 虚拟机、CentOS
---

说起来我觉得CentOS7.0满坑的诶╭(╯^╰)╮，真是满屏荒唐言，一把辛酸泪。



### 虚拟机连接方式介绍

虚拟机三种网络连接方式介绍：http://lilinji.blog.51cto.com/5441000/1264307




### CentOS7的一些坑

今天用才知道，CentOS7.0的网卡不叫eth0叫eno16XXXX（不记得具体了），然后CentOS默认开机时网卡是不启动的。真是遍地找坑。

如果有人看不惯网卡名字的话，可以看[这里](http://5323197.blog.51cto.com/5313197/1813868更改，但是我没试过，不清楚会怎样)

但是我三种方法都没有连接成功，最后采取了bridge的连接还更改了enoxxxx的文件再重启网络服务才成功的，这里只写更改文件的过程。



###操作过程 

参考文章：http://www.centoscn.com/CentOS/config/2015/0426/5285.html

http://www.dedecms.com/knowledge/servers/linux-bsd/2012/0822/12185.html




进入配置文件

```shell
vim /etc/sysconfig/network-scripts/ifcfg-eno16777736
```

如下图

 ![1](/images/blog/1.PNG)

中间一大串IPV4和IPV6是啥意思我都没弄懂的，另外在做图查资料的途中，发现如果我要固定IP的话其实 BOOTPROTO=static才是固定IP的协议，打错了又重新懒得做图的某只偷偷爬走。



改完确认设置的网卡信息(RHEL7/CentOS7默认安装,前提需要开启NetworkManager.service才可以使用)

```shell
nmtui-edit enoxxxxxxx
```

如图查验

 ![2](/images/blog/2.PNG)



连接一下

```shell
nmtui-connect enoxxxxxxxx
```

如图成功

 ![3](/images/blog/3.PNG)



最后重启网络服务

```shell
systemctl restart network
```

有时候会出现

```
Job for network.service failed because the control process exited with error code. See "systemctl status network.service" and "journalctl -xe" for details.
```

那就继续去更改文件，总之文件肯定没改对。。。有可能是配置文件中的MAC地址参数与ifconfig中的不一样造成的，将ifconfig中打印出来IPv4的地址写入网卡配置文件即可。

艾玛，我发现自从改对一次后就怎么改都不错了，想弄出之前的错误情况都不行。。。我之前那个错的是啥样来着？喵喵喵喵喵？？？？？



### 最后一点想说的

我发现本来我虚拟机里的kali用NAT模式是可以成功上网的，当时CentOS还不能上网，自从改好了CentOS的文件，Kali的NAT模式ping主机就显示了` connect: Network is unreachable`，但是把Kali的网络连接方式改成bridge模式就可以了，可能是我连接的网卡问题吧，留坑待填。
