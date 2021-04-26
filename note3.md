---
title: note3
abbrlink: 17758
date: 2021-04-20 11:01:06
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
# DAY04

## 使用github管理代码

### 创建一个空目录

```
mkdir hzoj
cd hzoj
pwd
```

### 把目录变成git仓库

```
git init
```

### 把文件添加到仓库

```
git add *
```

### 把文件提交到仓库

```
git commit *
```

### 查看结果

```
git status
```

### 把本地库的所有内容推送到远程库上

```
git remote add origin git@github.com:lws597/HZOJ.git
git push -u origin master
```
