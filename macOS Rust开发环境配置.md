macOS Rust开发环境配置

安装Rust（<https://rsproxy.cn/）>

```sh
curl --proto '=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh
```

default toolchain选择nightly，profile选择complete

配置crates.io源

编辑~/.cargo/config（[详见](https://github.com/xhwhis/config/blob/master/cargo.toml)）

```toml
[source.crates-io]
replace-with = "rsproxy-sparse"

[source.rsproxy]
registry = "https://rsproxy.cn/crates.io-index"
[source.rsproxy-sparse]
registry = "sparse+https://rsproxy.cn/index/"

[registries.rsproxy]
index = "https://rsproxy.cn/crates.io-index"

[net]
git-fetch-with-cli = true
```

下载rust-analyzer二进制

```sh
brew install rust-analyzer
```
