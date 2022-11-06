---
title: "Flarum mac本地化安装配置Guide"
date: 2022-03-28T15:58:59+08:00
draft: false
---

# Mac 本地化安装配置 Flarum

系统: macOS Monterey + Apple M1

前提: [homebrewCN](https://gitee.com/cunkai/HomebrewCN)

## MariaDB 配置

```sh
brew install mariadb
brew services restart mariadb
```

初始化 MariaDB
sudo 下配置

```sh
mysql_secure_installation
```

## Composer

```sh
brew install composer
```

ps. 安装 composer 会连同依赖 php 一同安装，但 flarum 没适配最新的 php

## php@8.0

```sh
brew install php@8.0
brew services restart php@8.0
```

同环境下还有一个 php，指定一下 PHP8.0

```sh
echo 'export PATH="/opt/homebrew/opt/php@8.0/bin:$PATH"' >> ~/.zshrc
echo 'export PATH="/opt/homebrew/opt/php@8.0/sbin:$PATH"' >> ~/.zshrc
```

## Caddy

```sh
brew install caddy
```

URL 重写——配置 Caddy
在/opt/homebrew/etc/Caddyfile 中添加配置，如果没有该文件，则新建

```
127.0.0.1:9090 {
    root * /var/www/flarum/public
    php_fastcgi 127.0.0.1:9000
    header /assets {
        +Cache-Control "public, must-revalidate, proxy-revalidate"
        +Cache-Control "max-age=25000"
        Pragma "public"
    }
    file_server
}
```

其中本地端口可改为其他，root 指向 flarum 的 public 路径，php 配置如未修改过，则 fastcgi 指向 URL 127.0.0.1:9000 即可

启动

```sh
brew services start caddy
```
