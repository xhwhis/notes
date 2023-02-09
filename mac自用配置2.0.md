mac 自用配置 2.0

开发环境

最先安装完成 Xcode，然后

```sh
xcode-select --install
```

配置常用开发环境

浏览器 —— google chrome

终端——iterm2

安装 homebrew（清华源 ）

设置环境变量

```sh
export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles"
```

初次安装使用 jsDelivr CDN 下载

```sh
/bin/bash -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/Homebrew/install@HEAD/install.sh)"
```

安装常用软件

clashx,visual-studio-code, clion, docker, multipass,、typora、notion、obsidian,telegram

安装常用工具

node,yarn,ccls,fzf,fd,ranger,autojump,thefuck,neovim,bash-language-server,bat,cmake,cocoapods,exa,go,gopls,hugo,ripgrep,rust-analyzer,shfmt,starship,yaml-language-server,taplo,helix,git-delta,gitui,just,navi,prettier,cbindgen,tldr,tokei,typescript,vhs

升级 pip

安装字体

```sh
brew tap homebrew/cask-fonts
brew install --cask font-sauce-code-pro-nerd-font
```
