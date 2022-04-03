---
title: git代理
date: 2022-03-27T22:59:11+08:00
draft: true
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
