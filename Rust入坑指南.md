# Rust入坑指南



## Rust开发环境搭建

### 安装Rust（https://rsproxy.cn/）

```sh
curl --proto '=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh
```

default toolchain选择nightly，profile选择complete



### 配置crates.io源

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



### 下载rust-analyzer二进制

（macOS上找不到rust-analyzer路径，Linux视情况添加二进制环境）

```sh
brew install rust-analyzer
```



### IDE

推荐VS Code + rust-analyzer插件，如果项目中有相当一部分C/CPP，也可用CLion + rust-analyzer插件



## Rust语法快速入门

阅读文章https://fasterthanli.me/articles/a-half-hour-to-learn-rust（此人https://fasterthanli.me/的所有文章都相当值得一看），此文章较为精华简练，是上手Rust语法的好读物。如果不懂的较多可以搭配菜鸟教程https://www.runoob.com/rust/rust-tutorial.html



## Rust入门学习

可以对照[Rust Course](https://course.rs/about-book.html)来入门学习（个人觉得废话较多，而且很多重点跳过或解释不清，但在中文Rust读物中算较好的，可以选择性跳过来学习）



在Rust语法入门和学习一些基础使用后，应该对Rust的常用类型、所有权、生命周期、流程控制、模式匹配、范型、错误处理、自动化测试、迭代器、闭包、智能指针、async/awiat、unsafe Rust、cargo使用等，有初步了解。如果在某个知识点不懂，可以对照[Rust 程序设计语言](https://www.rustwiki.org.cn/zh-CN/book/)来学习



Google出版的[Comprehensive Rust](https://google.github.io/comprehensive-rust/)也是相当好的Rust入门读物，但是没有中文版



[通过例子学 Rust](https://www.rustwiki.org.cn/zh-CN/rust-by-example/)也是较好的Rust入门读物



以上都是无痛入门Rust，要想有痛入门，可以学习[Rust By Practice](https://zh.practice.rs/why-exercise.html)



## Rust资料

### Rust Manual

Rust标准库 https://www.rustwiki.org.cn/zh-CN/std/

Cargo手册 https://rustwiki.org/zh-CN/cargo/



### Rust第三方库

社区crates.io https://crates.io/

非官方crates.io https://lib.rs/

crate 文档 https://docs.rs/

Rust库指南 https://blessed.rs/crates



## Rust进阶学习

Rust生命周期 https://github.com/pretzelhammer/rust-blog/blob/master/posts/translations/zh-hans/common-rust-lifetime-misconceptions.md（相当好！！！）

Rust std traits https://github.com/pretzelhammer/rust-blog/blob/master/posts/translations/zh-hans/tour-of-rusts-standard-library-traits.md（相当好！！！）

Rust宏编程 https://zjp-cn.github.io/tlborm/（https://zhuanlan.zhihu.com/p/106016118，该知乎文章总结提炼的较好，也可直接学习此篇文章）

Rust并发 https://marabos.nl/atomics/preface.html#who-this-book-is-for

Rust源码剖析 https://awesome-kusion.github.io/rust-code-book-zh/



## 个人建议

### 第三方库的上手

很多第三方库的文档没有适配docs.rs，可以直接去GitHub仓库查看是否有文档。如果没有文档或者较为简略，可以查看Crago项目下的examples文件夹或者项目中的testcase（可能在单独的tests文件夹也可能在相应的代码文件中）。Rust生态正处于快速发展中，确实有相当一部分库的的文档较旧，可以直接去看源码。



### 善用ChatGPT

#### ChatGPT辅助学习

ChatGPT可以是Rust学习的最好帮手，没有之一。可以让ChatGPT生成一些Rust片段来更好的学习一些知识点，但只限于Rust std片段，如果生成的代码有第三方库，ChatGPT生成效果较差，一来是第三方库这两年可能早就大变样了，二来是ChatGPT会一本正经地胡说八道。有一些基本算法和数据结构的实现可以问ChatGPT。GPT-4.0生成的Rust代码远优于GPT-3.5生成的，Rust语法方面的规则限制确实较多，GPT-4.0对Rust的支持更好。但是如果碰到异步闭包的代码，GPT-4.0也不能生成较好的代码，Rust的所有权和移动语义在异步闭包场景下确实较为复杂。



#### ChatGPT辅助编程

可以利用它来了解应该在项目中使用哪一些crates，但是在技术选型上不能完全指望它，ChatGPT只有21年之前的数据，而这两年Rust生态快速发展，很多crates已经被淘汰，或者早已无人维护。技术选项应该结合项目本身，尽量去选择一个最小支持的包；如果有多个crates可选择，应该选一个较活跃的。在项目初期，可以利用ChatGPT来生成一些demos。