---
layout: post
title: 纪念我曾经遇到的那些脑洞大的要死的隐写术
categories: [ctf]
description: 隐写术中的一些姿势技巧
keywords: CTF，隐写术
---

### 纪念我曾经遇到的那些脑洞大的要死的隐写术

我的隐写术启蒙篇：[隐写术总结](http://www.jianshu.com/p/67233f607f75)

这篇文章有提过的隐写术我就不细讲了，说一下这篇文章中没提到但是又经常虐我的隐写术们。

题目图片链接：[http://pan.baidu.com/s/1c1VX1wG](http://pan.baidu.com/s/1c1VX1wG) 

密码：7zza

#### 0X00 前言 

很多CTF比赛中会把隐写术作为一道单独的mist考点，当然，也有很多题会把图片隐写术作为题目的一部分。总之叽叽歪歪这么多就是为了说明隐写术很常见，以上皆为废话。以下是我曾经遇到过的一些题目

#### 0X01  2016HCTF你们所知道的隐写就仅此而已吗

图片：shimakaze.bmp

这真的是我遇到的脑洞最大的隐写题，所以第一个想起了它。这道题。。。要不是官方放了tips，谁能想到是用matlab进行傅里叶变换呢？盲水印隐写。由于是频域变换，所以这张图片一定是bmp格式无压缩。

用matlab进行一维傅里叶变换

``` c++
imageA = imread('shimakaze.bmp','bmp');
a = fft(imageA);
imshow(a);
```

flag如下

 ![1](images/ctf/yinxie/1.JPG)



#### 0X02 2016“华山杯”之大可爱

图片：dakeai.png

这张图片查看了图片通道位没啥发现。之后用binwalk查看，发现如下

 ![2](images/ctf/yinxie/2.JPG)

如果是正常的zlib的压缩应该是这样的，给个这种题的链接。[http://www.mamicode.com/info-detail-1294911.html](http://www.mamicode.com/info-detail-1294911.html)

总之这题不是正常的zlib压缩。用binwalk -e提取。然后检查占用空间，居然有东西。所以binwalk继续检查。

 ![3](images/ctf/yinxie/3.JPG)

29里面有东西，继续提取。提取出来继续检查。这次没东西了。

 ![4](images/ctf/yinxie/4.JPG)

那就检查两个文件。28D28D中存在有规律的字符串。

 ![5](images/ctf/yinxie/5.JPG)

如果做得多，会发现这是zip的文件头。然后把这串字符串保存为zip文件。

 ![6](images/ctf/yinxie/6.JPG)

结尾的字符串很像Base64，加上压缩包有密码。把字符串解码，结果是乱码。。。。这串字符串就直接是解压密码。。。。总之解压出来即可得到Flag



#### 0X03 大佬给的一道题（我也不知道出自哪里）

图片：dabai.png

这题刚开始做真是一点头绪都没有。。后来大佬给了工具和提示（基本都是大佬带着做完额）。用tweakpng.exe检查，发现IHDR的crc不对。

 ![6](images/ctf/yinxie/6.JPG)

在这里介绍一下png的格式，如下[http://blog.csdn.net/bisword/article/details/2777121](http://blog.csdn.net/bisword/article/details/2777121)

crc不对，说明IHDR有部分数据错误了，然后爆破得到正确的数据。

代码如下(谢谢大佬)

``` python
# -*- coding:utf-8 -*-

import binascii
def crc32(v):
    return '%x' % (binascii.crc32(v) & 0xffffffff) 

def foo():
    chunk_type="49484452"
    chunk_data_model="000002A7 %s 08 06 00 00 00"
    chunk_crc_raw="6D7C7135"

    for i in xrange(0xffff):
        chunk_data=chunk_data_model %'{:08x}'.format(i)
        chunk_crc=(chunk_type+chunk_data).replace(' ','').decode('hex')
        if crc32(chunk_crc).upper()==chunk_crc_raw:
            print i,'{:08x}'.format(i)
            break
    pass

if __name__ == '__main__':
    foo()
    print 'ok'
```

这里对图片高度进行了爆破，得到正确的高度后改写图片的hex，得到正确高度，然后发现Flag



#### 0X04 后记

暂时我能想起来的隐写就这些了，以后想起了其他的比较好玩的隐写或者做到了比较好玩的隐写再补。