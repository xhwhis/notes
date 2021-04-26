---
title: git代理
abbrlink: 39017
date: 2021-04-20 10:54:04
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
# git设置和取消代理



## 设置如下：

```bash
git config --global https.proxy http://127.0.0.1:1080
```

```bash
git config --global https.proxy https://127.0.0.1:1080
```

```bash
git config --global http.proxy 'socks5://127.0.0.1:1080' 
```

```bash
git config --global https.proxy 'socks5://127.0.0.1:1080'
```



### 取消

```bash
git config --global --unset http.proxy
```

```bash
git config --global --unset https.proxy
```
