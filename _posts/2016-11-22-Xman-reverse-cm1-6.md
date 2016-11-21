---
layout: post
title: Xman的reverse题入门篇课堂练习1-6
categories: [CTF, reverse]
description: 基础的reverse题
keywords: CTF, reverse
---

ida一时爽，看代码火葬场。

题目地址：[XCTF实训平台](http://xman.xctf.org.cn/task/3/8/)

使用工具：ida

### cm1

最基础的题目了，把程序拖入ida中分析，按F5出来主程序

![1-1](/images/Xman-reverse/1-1.JPG)

整体程序的逻辑是输入Str1字符串，然后用strncmp()将Str1与Str2比较，然后双击Str2跳转如下。

![1-2](/images/Xman-reverse/2-2.JPG)

可得Str2字符串内容为`Thi5_i5_T0o_E4sy`，将此字符串输入exe中，得到flag为`xman{Thi5_i5_T0o_E4sy}`



### cm2

同样拖入ida分析，得主程序如下

![2-1](/images/Xman-reverse/2-1.JPG)

可看到主要的加密部分如下，是基础异或加密

![2-1](/images/Xman-reverse/2-2.JPG)

这个函数\*和&很多。先科普一下，\*表示指针，&是取地址，这个函数解释一下，v12和v5是两个字符数组的首地址，v3为偏移量。所以就相当于把v5这个字符串每一位都与v3进行异或得到v12的每一位，然后得到最终的v12与unk_403010字符串进行比较。

双击unk_403010跳转查看字符串

![2-3](/images/Xman-reverse/2-3.JPG)

我一开始是直接采用了数字表示的char值进行转换（弄清原理，自己写个C的小程序就可以进行异或运算了，很简单），也就是`X1p\5vYi8}Uc8Mj`，但其实倒数第二位不是M而是delete（长这么像谁分的清啊。。。），所以建议不要用char来转换而是使用`5831705C765969387D5563387F6A`，转换为二进制再进行异或。

最后得到v5为`X0r_1s_n0t_h4rd`，flag为`xman{X0r_1s_n0t_h4rd}`。



### cm3

来来来，老套路，打开ida，拖入exe，得主函数如下

![3-1](/images/Xman-reverse/3-1.JPG)

有函数的跳转，看起来挺麻烦的。不过先看比较函数memcmp()比较的字符串，跳转。

![3-2](/images/Xman-reverse/3-2.JPG)

![3-3](/images/Xman-reverse/3-3.JPG)

熟悉的字符串结尾==，Base64加密妥妥的。之前那个函数可以不看了，百分百是进行Base64加密，然后线上Base64解码`QjRzZTY0X2k1X2MwbW1vbg==`，解码得`B4se64_i5_c0mmon`，输入此字符串，得flag为`xman{B4se64_i5_c0mmon}`

顺便看一下被我忽略的函数吧，感觉也怪可怜的

![3-4](/images/Xman-reverse/3-3.JPG)

下次不困了再分析这个函数



### cm4

老套路，先拖入ida去看一眼，得主函数如下

![4-1](/images/Xman-reverse/4-1.JPG)

两个函数的跳转，更心累了。看比较的字符串，几乎看不出什么。

![4-4](/images/Xman-reverse/4-4.JPG)

那就只能乖乖分析函数咯，第一个函数。

![4-2](/images/Xman-reverse/4-2.JPG)

出现了256的混码，有可能是rc4，但是我这个搞的不是很明白，最后看了别人的题解还没弄懂，留坑待填。



### cm5

先上主函数

![5-1](/images/Xman-reverse/5-1.JPG)

三个函数，真让人头大。习惯，先看比较函数字符串是否有提示和输出是否有提示。

![5-3](/images/Xman-reverse/5-3.JPG)

OK，md5，看样子本题为md5加密。那就直接看最后比较字符串。

![5-4](/images/Xman-reverse/5-4.JPG)

有些是ASCII没有的，直接取`7FEF6171469E80D32C0559F88B377245`去md5解密，得结果`admin888`，输入exe中，得flag为`xman{admin888}`，中间复杂的想死的三个函数跳过，欧啦。



### cm6

上图先

![6-1](/images/Xman-reverse/6-1.JPG)

程序很简单，来分析下中间的函数。

易知，输入的v7字符串长度为22。v5为v7字符串中的每一个字符，v4为v7字符串距离首地址的偏移量。v3用`aXmanS`初始化指向`aXmanS`的首地址，跳转到`aXmanS`字符串查看。

![6-2](/images/Xman-reverse/6-2.JPG)

发现此字符串为`* #`组成。回到主函数，理一下逻辑。中间通过if确定长度，然后v5取出v7字符串中的每一位，v3本身为地址，\*v3表示这个地址的内容，看输出flag的比较函数为`if(*v3==35)`,通过查ASCII码表得35为`#`的ASCII值，则此时v3指向字符串的`#`地址，即第27位。所以整体的逻辑就是用中间的switch函数来控制v3的跳转，使一开始的v3偏移为0到偏移27位。

看循环结束条件

![6-3](/images/Xman-reverse/6-2.JPG)

可以猜测前两个条件是防止v3越界，而`*v3==42`表示v3的值为`*`号，所以需要跳过所有\*所在位置（写个程序判断吧，不要傻兮兮的自己数），得到所有*位置，再通过switch中的跳转条件。最后得到控制跳转字符串为`dddddrrrrruuuuullldddr`，输入得flag为`xman{dddddrrrrruuuuullldddr}`。

