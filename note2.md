---
title: note2
date: 2022-03-27T22:59:11+08:00
draft: false
---

# DAY03

## Linux 极简入门

### 文件与目录的管理

| 命令 | 功能               |
| ---- | ------------------ |
| ls   | 显示文件及目录信息 |
| cp   | 拷贝               |
| rm   | 删除               |
| mv   | 移动               |

### cp 拷贝

cp [irapdslu] <sour> <dest>

选项

- -i 若文件存在，询问用户
- -r 递归复制
- -a pdr 的集合
- -p 连同文件属性一起拷贝
- -d 若源文件为连接文件的属性，则复制连接文件的属性
- -s 拷贝为软连接
- -l 拷贝为硬连接
- -u 源文件比目的文件新才拷贝

### rm 删除

rm [irf] <dir_or_file>

选项

- -i 互动模式
- -r 递归删除
- -f force

### mv 移动

mv [ifu] <source...> <dest>

- mv source1 source2 souce3 dir

选项

- -i 互动模式
- -f force
- -u 源文件更新才会移动

### 文件内容的查阅

| 命令 | 功能                           |
| ---- | ------------------------------ |
| cat  | 正向连接读                     |
| tac  | 反向连接读                     |
| nl   | 输出行号显示文件               |
| more | 一页一页的显示文件内容         |
| less | 与 more 相似，但是可以上下翻看 |
| head | 只看头几行                     |
| tail | 只看末尾几行                   |

### cat 正向连续读

cat [-AbEnTv] <file>

选项:

- -A:相当于-vET
- -v:列出看不出的字符
- -E:显示断行符为$
- -T:显示 TAB 为^T
- -b:列出行号
- -n:列出行号,连同空行也编号

### tac 反向连续读

刚好与 cat 相反,从最后一行开始打印

### nl 输出行号显示文件

nl [-bnw] <file>

选项

- -b:行号指定的方式
- - -b a:相当于 cat -n
  - -b t:相当于 cat -b
- -n:列出行号的表示方法
- - -n ln:行号在屏幕最左边显示
  - -n rn:行号在自己字段的最右边显示
  - -n rz:行号在自己字段的最右边显示,前面自动补全 0
- -w <num>:行号所占位数

### more 按页查看

more file

- /string 向下查找 string 关键字
- :f 显示文件名称和当前显示的行数
- q 离开

### less 按页查看

less file

- /string 向下查找 n:继续向下查找
- /?string 反向查找 N:继续反向查询

### head 查看头几行

head [-n num] <file>

- -n num:显示前 num 行

### tail 查看末尾几行

tail [-n num] <file>

- -n num:显示文件后 num 行
- -f:force

如何查看一个文件的 101 行到 120 行?

man ls | nl -b a -w 5 -n rz | head -n 120 | tail -n 20

### man 手册

1. man 手册页分为下面几个部分:
2. 普通命令
3. 内核提供的系统调用
4. 库调用(C 库函数)
5. 特殊文件(大多数在/dev 目录下)和设备
6. 文件格式规范
7. 游戏
8. 杂项(及其规范)
9. 系统管理命令(通常需要 root 权限)和守护进程

## 配置 wifi

### 打开终端,执行命令

```
sudo service NetworkManager stop	#关闭NetworkManager
sudo service NetworkManager start	#开启NetworkManager
```

### 执行命令,查看网卡命名

```
ifcongif -a
```

### 更改 interfaces 配置

```
sudo vim /etc/network/interfaces
```

在文本框中输入,保存并退出

```
auto wlp3s0
allow-hotplug wlp3s0
iface wlp3s0 inet dhcp
pre-up wpa_supplicant -Dwext -i wlp3s0 -c /etc/wpa_supplicant/wpa_supplicant.conf -B
```

### 编辑 wpa_supplicant.conf

```
sudo vim /etc/wpa_supplicant/wpa_supplicant.conf
```

在文本框中输入,保存并退出

```
country=CN
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
    ssid="HaiZei_Tech"
    psk="HaiZei731."
    scan_ssid=1
    priority=3
}
```

### 更改 DNS

```
sudo vim /etc/resolv.conf
```

nameserver 8.8.8.8
