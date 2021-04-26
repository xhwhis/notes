---
title: avl_tree
abbrlink: 51743
date: 2021-04-20 10:42:00
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
# avl_tree



## 节点数

在高度为h的avl树中，最少节点数low(h)

low(h) = low(h - 1) + low(h - 2) + 1	low(0) = 1 low(1) = 2

最大节点数max(h)

max(h) = 2^h - 1



## 平衡

LL型 右旋

RR型 左旋

LR型 左旋-->(LL型)-->右旋

RL型 右旋-->(RR型)-->左旋
