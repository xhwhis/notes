### Arm Mac Aya/eBPF开发环境配置



#### Linux环境配置

##### 创建vm

使用multipass工具（https://multipass.run/）

安装multipass

```sh
brew install multipass
```

配置vm

```sh
multipass launch --name vm --cpus 4 --disk 40G --memory 4G
```

磁盘空间大小暂定40G



##### 修改Ubuntu软件源（清华源）

编辑/etc/apt/sources.list

```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-security main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-proposed main restricted universe multiverse
```

启用预发布软件源

##### 升级Ubuntu

```sh
sudo apt update
sudo apt upgrade
sudo apt autoremove
```



#### 安装Rust（https://rsproxy.cn/）

```sh
curl --proto '=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh
```

default toolchain选择nightly，profile选择complete

#### 配置crates.io源

编辑~/.cargo/config（[详见](https://github.com/xhwhis/config/blob/master/cargo.toml)）

```toml
[source.crates-io]
replace-with = "rsproxy"

[source.rsproxy]
registry = "https://rsproxy.cn/crates.io-index"
[source.rsproxy-sparse]
registry = "sparse+https://rsproxy.cn/index/"

[registries.rsproxy]
index = "https://rsproxy.cn/crates.io-index"

[net]
git-fetch-with-cli = true
```



#### 安装bpd-linker依赖

安装构建依赖

```sh
sudo apt install build-essential zlib1g-dev
```

Arm Mac上的Linux需要使用LLVM15编译bpf-linker，先安装llvm-15-dev、libclang-15-dev

```sh
sudo apt install llvm-15-dev libclang-15-dev
```

安装bpf-linker

```sh
cargo install --no-default-features --features system-llvm bpf-linker
```



#### 构建Aya程序

安装cargo-generate

```sh
cargo install cargo-generate
```

通过Aya模板生成项目，以 XDP 类型程序为例

```
cargo generate https://github.com/aya-rs/aya-template
```

构建并运行项目

```sh
cargo xtask build-ebpf
RUST_LOG=info cargo xtask run -- --iface lo
```

程序正常输出，配置完成！



#### vscode配置

拷贝主机的~/.ssh/id_rsa.pub，粘贴到vm的~/.ssh/authorized_keys

vscode安装插件Remote - SSH，连接到vm（ssh ubuntu@$ip -A）

vscode安装插件rust-analyzer
