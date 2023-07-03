# Rust 入坑指南

## Rust 开发环境搭建

### 安装 Rust（https://rsproxy.cn/ ）

```sh
curl --proto '=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh
```

default toolchain 选择 nightly，profile 选择 complete

### 配置 crates.io 源

编辑~/.cargo/config

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

### 下载 rust-analyzer 二进制

（macOS 上找不到 rust-analyzer 路径，Linux 视情况添加二进制环境）

```sh
brew install rust-analyzer
```

### IDE

推荐 VS Code + rust-analyzer 插件，如果项目中有相当一部分 C/CPP，也可用 CLion + rust-analyzer 插件

## Rust 语法快速入门

阅读文章https://fasterthanli.me/articles/a-half-hour-to-learn-rust （此人https://fasterthanli.me/ 的所有文章都相当值得一看），此文章较为精华简练，是上手 Rust 语法的好读物。如果不懂的较多可以搭配菜鸟教程https://www.runoob.com/rust/rust-tutorial.html

## Rust 入门学习

可以对照[Rust Course](https://course.rs/about-book.html)来入门学习（个人觉得废话较多，而且很多重点跳过或解释不清，但在中文 Rust 读物中算较好的，可以选择性跳过来学习）

在 Rust 语法入门和学习一些基础使用后，应该对 Rust 的常用类型、所有权、生命周期、流程控制、模式匹配、范型、错误处理、自动化测试、迭代器、闭包、智能指针、async/awiat、unsafe Rust、cargo 使用等，有初步了解。如果在某个知识点不懂，可以对照[Rust 程序设计语言](https://www.rustwiki.org.cn/zh-CN/book/)来学习

Google 出版的[Comprehensive Rust](https://google.github.io/comprehensive-rust/)也是相当好的 Rust 入门读物，但是没有中文版

[通过例子学 Rust](https://www.rustwiki.org.cn/zh-CN/rust-by-example/)也是较好的 Rust 入门读物

以上都是无痛入门 Rust，要想有痛入门，可以学习[Rust By Practice](https://zh.practice.rs/why-exercise.html)

## Rust 资料

### Rust Manual

Rust 标准库 https://www.rustwiki.org.cn/zh-CN/std/

Cargo 手册 https://rustwiki.org/zh-CN/cargo/

### Rust 第三方库

社区 crates.io https://crates.io/

非官方 crates.io https://lib.rs/

crate 文档 https://docs.rs/

Rust 库指南 https://blessed.rs/crates

## Rust 进阶学习

Rust 生命周期 https://github.com/pretzelhammer/rust-blog/blob/master/posts/translations/zh-hans/common-rust-lifetime-misconceptions.md （相当好！！！）

Rust std traits https://github.com/pretzelhammer/rust-blog/blob/master/posts/translations/zh-hans/tour-of-rusts-standard-library-traits.md （相当好！！！）

Rust 宏编程 https://zjp-cn.github.io/tlborm/ （https://zhuanlan.zhihu.com/p/106016118 ，该文章对声明式宏总结提炼的较好，学习 macro_rules!可以直接看此篇文章）

Rust 编译优化 https://github.com/johnthagen/min-sized-rust

Rust 并发 https://marabos.nl/atomics/preface.html#who-this-book-is-for

Rust 源码剖析 https://awesome-kusion.github.io/rust-code-book-zh/

## 个人建议

### 第三方库的上手

很多第三方库的文档没有适配 docs.rs，可以直接去 GitHub 仓库查看是否有文档。如果没有文档或者较为简略，可以查看 Crago 项目下的 examples 文件夹或者项目中的 testcase（可能在单独的 tests 文件夹也可能在相应的代码文件中）。Rust 生态正处于快速发展中，确实有相当一部分库的的文档较旧，可以直接去看源码。

### 善用 ChatGPT

#### ChatGPT 辅助学习

ChatGPT 可以是 Rust 学习的最好帮手，没有之一。可以让 ChatGPT 生成一些 Rust 片段来更好的学习一些知识点，但只限于 Rust std 片段，如果生成的代码有第三方库，ChatGPT 生成效果较差，一来是第三方库这两年可能早就大变样了，二来是 ChatGPT 会一本正经地胡说八道。有一些基本算法和数据结构的实现可以问 ChatGPT。GPT-4.0 生成的 Rust 代码远优于 GPT-3.5 生成的，Rust 语法方面的规则限制确实较多，GPT-4.0 对 Rust 的支持更好。但是如果碰到异步闭包的代码，GPT-4.0 也不能生成较好的代码，Rust 的所有权和移动语义在异步闭包场景下确实较为复杂。

#### ChatGPT 辅助编程

可以利用它来了解应该在项目中使用哪一些 crates，但是在技术选型上不能完全指望它，ChatGPT 只有 21 年之前的数据，而这两年 Rust 生态快速发展，很多 crates 已经被淘汰，或者早已无人维护。技术选项应该结合项目本身，尽量去选择一个最小支持的包；如果有多个 crates 可选择，应该选一个较活跃的。在项目初期，可以利用 ChatGPT 来生成一些 demos。
