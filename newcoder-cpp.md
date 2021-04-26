---
title: newcoder_cpp
abbrlink: 22684
date: 2021-04-20 10:58:13
updated:
tags:
categories:
keywords:
description:
top_img:
comments:
cover:
toc:
toc_number:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---
# niuke interview



## 基本语言



### 请说一下C/C++ 中指针和引用的区别？

参考回答：

1. 指针有自己的一块空间，而引用只是一个别名；
2. 使用sizeof看一个指针的大小是4，而引用则是被引用对象的大小；
3. 指针可以被初始化为NULL，而引用必须被初始化且必须是一个已有对象 的引用；

4. 作为参数传递时，指针需要被解引用才可以对对象进行操作，而直接对引 用的修改都会改变引用所指向的对象；

5. 可以有const指针，但是没有const引用；

6. 指针在使用中可以指向其它对象，但是引用只能是一个对象的引用，不能 被改变；

7. 指针可以有多级指针（**p），而引用至于一级；

8. 指针和引用使用++运算符的意义不一样；

9. 如果返回动态内存分配的对象或者内存，必须使用指针，引用可能引起内存泄露。



### 请你回答一下野指针是什么？

参考回答：

野指针就是指向一个已删除的对象或者未申请访问受限内存区域的指针
