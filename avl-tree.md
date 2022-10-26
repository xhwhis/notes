---
title: avl_tree
date: 2022-03-27T22:59:11+08:00
draft: true
---

# avl_tree

## 节点数

在高度为 h 的 avl 树中，最少节点数 low(h)

low(h) = low(h - 1) + low(h - 2) + 1 low(0) = 1 low(1) = 2

最大节点数 max(h)

max(h) = 2^h - 1

## 平衡

LL 型 右旋

RR 型 左旋

LR 型 左旋-->(LL 型)-->右旋

RL 型 右旋-->(RR 型)-->左旋
