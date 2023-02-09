### macOS自用配置2.0

#### 开发环境

最先安装完成Xcode，然后

```sh
xcode-select --install
```



#### 安装初始软件

浏览器——Google Chrome

终端——iTerm2



#### 安装homebrew（清华源）

设置环境变量

```sh
export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles"
```

初次安装使用jsDelivr CDN下载

```sh
/bin/bash -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/Homebrew/install@HEAD/install.sh)"
```

#### brew安装常用软件

clashx、visual-studio-code、clion、docker、multipass、typora、notion、obsidian、telegram

#### brew安装常用工具

node、yarn、ccls、fzf、fd、ranger、autojump、thefuck、neovim、bash-language-server、bat、cmake、cocoapods、exa、go、gopls、hugo、ripgrep、rust-analyzer、shfmt、starship、yaml-language-server、taplo、helix、git-delta、gitui、just、navi、prettier、cbindgen、tldr、tokei、typescript、vhs、flutter、marksman



#### 升级 pip（python使用Xcode中的）

```sh
/Applications/Xcode.app/Contents/Developer/usr/bin/python3 -m pip install --upgrade pip
```

升级后会在当前用户下生成pip PATH，将PATH加入到系统PATH中

#### 配置pip源（清华源）

```sh
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

#### 安装pygments、pynvim

```sh
pip install pygments
pip install pynvim
```



#### 配置npm、yarn源（阿里源）

```sh
npm config set registry http://registry.npmmirror.com
yarn config set registry http://registry.npmmirror.com
```



#### 安装字体

```sh
brew tap homebrew/cask-fonts
brew install --cask font-sauce-code-pro-nerd-font
```



#### 配置git

```sh
git config --global user.name "xhwhis"
git config --global user.email "hi@whis.me"
```

编辑~/.gitconfig（[详见](https://github.com/xhwhis/config/blob/master/gitconfig)）

编辑~/.gitigrone_global（[详见](https://github.com/xhwhis/config/blob/master/gitigrone_global)）

#### 配置git-commit

##### commitizen

```sh
yarn global add commitizen
```

##### commitlint、cz-conventional-changelog

```sh
yarn global add @commitlint/cli @commitlint/config-conventional
yarn global add cz-conventional-changelog
```

编辑~/.commitlintrc.js（[详见](https://github.com/xhwhis/config/blob/master/commitlintrc.js)）

```js
module.exports = { extends: ["@commitlint/config-conventional"] };
```

编辑~/.czrc（[详见](https://github.com/xhwhis/config/blob/master/czrc)）

```
{ "path": "cz-conventional-changelog" }
```

##### lint-staged

```sh
yarn global add lint-staged
```

编辑~/.lintstagedrc.json（[详见](https://github.com/xhwhis/config/blob/master/lintstagedrc.json)）

```json
{ "*.{md, yml, yaml, json, xml}": "prettier --ignore-unknown --write" }
```

##### husky

```sh
yarn global add husky
```



#### 下载rust（https://rsproxy.cn/）

```sh
curl --proto '=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh
```

#### 配置cargo config

编辑~/.cargo/config（[详见](https://github.com/xhwhis/config/blob/master/cargo.toml)）



#### 配置starship

编辑~/.config/starship.toml（[详见](https://github.com/xhwhis/config/blob/master/starship.toml)）

```toml
# Get editor completions based on the config schema
"$schema" = 'https://starship.rs/config-schema.json'

command_timeout = 4000

# Disable the package module, hiding it from the prompt completely
[package]
disabled = true
```



#### 配置helix

构建tree-sitter

```sh
hx --grammar fetch
hx --grammar build
```

配置helix config

编辑~/.config/helix/config.toml（[详见]()）



#### 配置zsh

##### 安装ohmyzsh

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

##### 下载ohmyzsh plugin

```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/paulirish/git-open.git $ZSH_CUSTOM/plugins/git-open
```

##### 配置zshrc（[详见](https://github.com/xhwhis/config/blob/master/zshrc)）

###### 自用主题（[dracula](https://draculatheme.com/zsh)）

###### 自用插件

```
plugins=(git zsh-autosuggestions zsh-syntax-highlighting autojump web-search extract last-working-dir sudo pip thefuck colored-man-pages colorize safe-paste git-open vi-mode copyfile copypath gitfast command-not-found history)
```

###### aliases

```
alias vim="nvim"
alias vi="nvim"
alias python="python3"
alias pip="pip3"
alias rm="rm -i"
alias cp="cp -i"
alias cls="clear"
alias ls="exa --git"
alias tree="exa --tree"
alias cat="bat --theme=Dracula"
alias find="fd"
alias ra="ranger"
alias cd..="cd .."
alias proxy="export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890"
alias unproxy="unset https_proxy http_proxy all_proxy"
alias -s c=copyfile
alias -s cpp=copyfile
```

###### homebrew环境参数

```
export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles"
export HOMEBREW_NO_ENV_HINTS=true
```

###### rustup环境参数

```
export RUSTUP_DIST_SERVER="https://rsproxy.cn"
export RUSTUP_UPDATE_ROOT="https://rsproxy.cn/rustup"
```

###### flutter环境参数

```
export PUB_HOSTED_URL="https://pub.flutter-io.cn"
export FLUTTER_STORAGE_BASE_URL="https://storage.flutter-io.cn"
```

###### 其他配置参数

```
[ -f /opt/homebrew/etc/profile.d/autojump.sh ] && . /opt/homebrew/etc/profile.d/autojump.sh
eval $(thefuck --alias)
eval $(starship init zsh)
export FZF_DEFAULT_OPTS="--color=fg:#f8f8f2,bg:#282a36,hl:#bd93f9 --color=fg+:#f8f8f2,bg+:#44475a,hl+:#bd93f9 --color=info:#ffb86c,prompt:#50fa7b,pointer:#ff79c6 --color=marker:#ff79c6,spinner:#ffb86c,header:#6272a4"
```



#### dracula主题（https://draculatheme.com/）

iTerm2（https://draculatheme.com/iterm）