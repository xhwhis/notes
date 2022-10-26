---
title: manjaro kde安装后的配置
date: 2022-03-27T22:59:11+08:00
draft: true
---

# manjaro kde 安装后的配置

## 启动项

```shell
sudo update-grub
```

## 镜像源（选择清华源）

```shell
sudo pacman-mirrors -i -c China -m rank
sudo pacman -Syy
sudo nano /etc/pacman.conf
```

```
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = http://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```

```shell
sudo pacman -S archlinuxcn-keyring
sudo apcman -Syyu
```

## 安装软件

### yay

```bash
sudo pacman -S yay base-devel
```

```shell
yay --save --aururl "https://aur.tuna.tsinghua.edu.cn"
```

### git

```shell
yay -S git
```

```shell
git config --global user.name 'lws597'
git config --global user.email '1320949958@qq.com'
sudo vim /etc/hosts
```

```
52.74.223.119 github.com
151.101.77.194 github.global.ssl.fastly.net
151.101.76.133 raw.githubusercontent.com
```

#### github 密钥导入

```shell
ssh-keygen
cat .ssh/id_rsa.pub
```

### 常用

```shell
yay -S gcc go jdk8-openjdk clang python python2 google-chrome netease-cloud-music typora
```

### pip

```shell
yay -S python-pip python2-pip
```

```shell
mkdir ~/.pip
nano ~/.pip/pip.conf
```

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = https://pypi.tuna.tsinghua.edu.cn
```

### npm

```shell
npm config set registry https://registry.npm.taobao.org
```

```shell
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

### neovim

```shell
yay -Rns vim
yay -S neovim
```

```shell
cd .config
git clone git://github.com/lws597/nvim
```

### zsh

```shell
yay -S zsh
```

```shell
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

#### zsh 插件

```
plugins=(git zsh-autosuggestions zsh-syntax-highlighting autojump web-search extract last-working-dir sudo pip thefuck colored-man-pages colorize safe-paste git-open vi-mode copyfile copydir gitfast command-not-found history)
```

```shell
yay -S autojump thefuck
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/paulirish/git-open.git $ZSH_CUSTOM/plugins/git-open
```

#### zshrc 添加

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

### 输入法（rime）

```shell
yay -S fcitx-im kcm-fcitx fcitx-rime
sudo vim ~/.xprofile
```

```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=""@im=fcitx"
```

### wps

```shell
yay -S wps-office-mui-zh-cn wps-office ttf-wps-fonts
```

### IDE

```shell
yay -S visual-studio-code-bin
```

### 字体

```shell
yay -S nerd-fonts-complete ttf-monaco ttf-hanazono
```

### 美化

```shell
yay -S latte-dock
```

主题 arc

图标 numix papirus

光标 mcmojave

### 其他软件

```shell
yay -S xmind zoom dingtalk electronic-wechat qq-linux
```

### 双系统时间

windows 端管理员下 cmd 或 powershell

```shell
reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_QWORD /f
```
