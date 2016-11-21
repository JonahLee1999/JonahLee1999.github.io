---
layout: post
title: template page
categories: [cate1, cate2]
description: some word here
keywords: keyword1, keyword2
---

围绕虚函数的UAF

视频来源：[https://www.inforsec.org/wp/?p=1223](https://www.inforsec.org/wp/?p=1223)

一块释放了内存，另外一块还在调用，产生一个悬挂指针。攻击者通过巧妙控制程序，可以控制释放掉这块内存的内容的，将object更改掉进行控制。

面向对象的虚函数调用，面向多态，具体运行时对象自身决定的。从运行时的对象寻找函数，virtual table指针域，指向一个数组，数组的每个表象都是一个指针，指针指向一个虚函数。通过virtual table指针寻找虚函数。

对象寻找虚函数：从对象读出他的virtual table指针，从virtual table指针找出virtual table，再从virtual table找到对应的虚函数。

virtual table指针从对象中读出，对象存在可读写内存段中，所以攻击者可篡改virtual table指针。

攻击：

* virtual table注入攻击。伪造一个virtual table，virtual table的每个表象都是一个get it地址。当虚函数被调用，LP
* 篡改virtual table指针，但不注入新的，而是重用virtual table指针
* 理论上，直接改virtual table，但是现在不行，编译器都把virtual table放在只读内存中。

Protecting Virtual Function Tables' Integrity

二进制层次的防护

virtual table破坏，原理是攻击者篡改virtual table

注入：条件：virtual table指针可改，注入的virtual table是有地方放

重用：指向已存在的virtual table或者数据，如果是数据必须长得特别像virtual table，即都是代码指针。

防御：

前两类要求virtual table是可写的，检查virtual table是否只读，不可写才安全

重用型只能防御一部分，把像的数据部分区分开



 

