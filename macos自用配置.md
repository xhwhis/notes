---
title: macos自用配置
date: 2021-07-03 01:50:29
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

### macos自用配置

浏览器——google chrome

翻墙——v2rayU

终端——iterm2

笔记——typora

git tool——sourcetree



#### 开发环境

最先安装完成Xcode，然后

```sh
xcode-select --install
```

配置常用开发环境（其中python3 version 3.8，需brew install python@3.9）



#### 安装homebrewcn

```sh
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```



#### 安装常用工具

python、node、yarn、ccls、fzf、ranger、typora、sourcetree、qt-creator、autojump、thefuck、visual-studio-code、neovim、microsoft-remote-desktop，只需要分别

```sh
brew install #+ 以上包名
```

安装过程中部分包会提示在.zshrc中添加配置，自行添加



#### 修改pip源

```sh
mkdir ~/.pip
vim ~/.pip/pip.conf
```

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = https://pypi.tuna.tsinghua.edu.cn
```

#### 升级pip

```sh
pip3 install --upgrade pip
```

#### 安装pygments、pynvim

```sh
pip install -g pygments
pip install -g pynvim
```



#### 修改npm、yarn源

```sh
npm config set registry https://registry.npm.taobao.org
yarn config set registry https://registry.npm.taobao.org
```



#### iterm2配置

##### 先安装ohmyzsh

```sh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

##### 下载ohmyzsh plugin

```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/paulirish/git-open.git $ZSH_CUSTOM/plugins/git-open
```

##### .zshrc修改

自用插件，`plugin=(git)`括号里面添加

```
plugins=(git zsh-autosuggestions zsh-syntax-highlighting autojump web-search extract last-working-dir sudo pip thefuck colored-man-pages colorize safe-paste git-open vi-mode copyfile copydir gitfast command-not-found history)
```

##### alias添加

```
alias vim="nvim"
alias vi="nvim"
alias rm="rm -i"
alias cp="cp -i"
alias cls="clear"
alias cat="ccat"
alias ra="ranger"
alias -s c=copyfile
alias -s cpp=copyfile
```

终端里`zsh`即可加载配置



#### 安装字体

```sh
brew tap homebrew/cask-fonts
brew install --cask font-sauce-code-pro-nerd-font
```

补充一些缺失的符号



#### nvim+spacevim配置

##### 安装spacevim

```sh
curl -sLf https://spacevim.org/cn/install.sh | bash
```

##### 自用配置

```sh
git clone https://github.com/lws597/SpaceVim.git .SpaceVim.d
```

终端里nvim即可下载插件



#### 配色主题

Xcode、vscode、iterm2、zsh自用配色主题为`dracula`

https://draculatheme.com/

https://github.com/dracula/dracula-theme
