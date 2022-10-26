---
title: note1
date: 2022-03-27T22:59:11+08:00
draft: true
---

# DAY01

## 更新源

### 打开终端（Ctrl+Alt+T），执行命令

```
sudo gedit /etc/apt/sources.list
```

### 将文本框的内容删除，粘贴以下内容,保存并退出

```
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
```

·预先加载的应用（apt-get install preload）能识别一个用户最常用的
程序，也能把二进制文件和依赖性预先加载到内存，以提供更快速的访
问。随着安装后的第一次重启，它会自动运行。
·BleachBit（apt-get install bleachbit）释放磁盘空间，通过释放缓
存、删除 cookie、清除上网记录、粉碎临时文件、删除日志，以及丢弃
其他一些非必需的文件来提高隐私性。使用高级技术，包括粉碎文件来
防止恢复，擦除空闲磁盘空间来隐藏没有完全删除的文件的踪迹。

~/.config/deepin/deepin-terminal/config.conf

### 执行命令

```
sudo apt-get update
sudo apt-get upgrade
```

## 配置 VIM

### 打开终端，执行命令

```
sudo gedit /etc/hosts
```

### 将以下两行文本添加到文本框中，保存并退出

```
192.30.255.112 github.com git
185.31.16.184 github.global.ssl.fastly.net
```

### 执行命令

```
sudo wget -qO- https://raw.github.com/ma6174/vim/master/setup.sh | sh -x
```

https://blog.csdn.net/LSG_Down/article/details/89319472

https://www.jianshu.com/p/75cde8a80fd7

## 安装 sshpi 及 scppi

sshpi.sh 参考代码

```
#!/bin/bash

#文件名：sshpi.sh
#用途：远程连接树莓派

function Usage() {
	echo "Usage: sshpi Username@pi"
	echo "Like This：sshpi UserA@pi1"
}
if [[ ! $# -eq 1  ]]; then
	Usage
	exit
fi

echo $1 | grep "@" >/dev/zero 2>&1

if [[ ! $? -eq 0 ]]; then
	echo "argument wrong！"
	Usage
	exit
fi
Username=`echo $1 | cut -d "@" -f 1`
if [[ ${Username}x == x ]]; then
	echo "Please input your username!"
	Usage
	exit
fi
Hostname=`echo $1 | cut -d "@" -f 2`
if [[ ${Hostname}x == x ]]; then
	echo "Please input Hostname of Pi!"
	Usage
	exit
fi
echo $Hostname | grep -w "^pi[1-9][0-9]\?" >/dev/null 2>&1
if [[ ! $? -eq 0 ]]; then
	echo "Hostname is Wrong!"
	Usage
	exit
fi
HostNum=`echo $Hostname | cut -c 3-`
if [[ $HostNum -gt 22 ]]; then
	echo "Hostname is Wrong!"
	Usage
	exit
fi

port=$[6530 + $HostNum]
echo -e "\033[46;30m You Will login\033[0m\033[46;31m $Hostname\033[0m\033[46;30m with Username \033[46;31m$Username\033[0m\033[46;30m, enjoy it!\033[0m"
ssh -p $port ${Username}@zentao.haizeix.tech
```

scppi.sh 参考代码

```
#!/bin/bash

#文件名：scppi.sh
#用途：远程拷贝文件，在树莓派和本机之间

function Usage() {
	echo "Usage: scppi file_or_dir Username@piname:dest_file_or_dir"
	echo "       scppi Username@piname:./file_or_dir  file_or_dir"
	echo "Like This：scppi PiHealth pi@pi1:./new"
}
if [[ ! $# -eq 2  ]]; then
	Usage
	exit
fi
#1.源
#2.目标

echo $1 | grep -q "@"

if [[ $? -eq 0 ]]; then
	remote=$1
	local=$2
else
	remote=$2
	local=$1
fi

echo $remote | grep @ | grep : >/dev/null 2>&1
if [[ ! $? -eq 0 ]]; then
	echo "argument wrong！"
	Usage
	exit
fi
Username=`echo $remote | cut -d "@" -f 1`
if [[ ${Username}x == x ]]; then
	echo "Please input your username!"
	Usage
	exit
fi
Hostname=`echo $remote | cut -d "@" -f 2 | cut -d ":" -f 1`
if [[ ${Hostname}x == x ]]; then
	echo "Please input Hostname of Pi!"
	Usage
	exit
fi
echo $Hostname | grep -w "^pi[1-9][0-9]\?" >/dev/null 2>&1
if [[ ! $? -eq 0 ]]; then
	echo "Hostname is Wrong!"
	Usage
	exit
fi
dir_file=`echo $remote | cut -d "@" -f 2 | cut -d ":" -f 2`
if [[ ${dir_file}x == x ]]; then
	echo "Please input dest_file_or_dir of Pi!"
	Usage
	exit
fi

HostNum=`echo $Hostname | cut -c 3-`

if [[ $HostNum -gt 22 ]]; then
	echo "Hostname is Wrong!"
	Usage
	exit
fi

port=$[6530 + $HostNum]
echo -e "\033[46;30m Coping \033[46;31m$1\033[46;30m to \033[46;31m$dir_file\033[46;30m on \033[46;31m$Hostname\033[46;30m with Username \033[46;31m$Username\033[46;30m, enjoy it!\033[0m"

if [[ $1 = $local ]]; then
	scp -P $port -r $1  ${Username}@zentao.haizeix.tech:$dir_file
else
	scp -P $port -r ${Username}@zentao.haizeix.tech:$dir_file $local
fi
```

### 打开终端，执行命令

```
vim sshpi.sh
```

### 在 VIM 文本框里粘贴 sshpi 脚本的代码，保存并退出（：wq）

### 将 sshpi.sh 重命名为 sshpi,赋予 sshpi 脚本可执行权限

```
mv sshpi.sh sshpi
chmod a+x sshpi
```

### 执行命令

```
echo $PATH
```

### 将 sshpi 复制到 PATH 路径下

```
cp sshpi /bin
```

### 同样的操作生成 scppi 脚本

# DAY02

## 设置免密登录

### 打开终端，执行命令

```
sshpi lws@pi3
```

暂时需要密码（haizei）来连接树莓派

### 在本机生成秘钥

```
ssh-keygen
```

### 将秘钥复制到 authorized_keys 文件中

```
cat .ssh/id_rsa.pub>>.ssh/authorized_keys
```

### 将本机的 authorized_keys 文件复制到树莓派中

```
scppi .ssh/authorized_keys lws@pi3:/.ssh
```

### 再次连接树莓派，验证是否成功

check.c

```
#include <stdio.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>
#include <pwd.h>

int socket_connect(int port, char *host) {
	int sockfd;
	struct sockaddr_in dest_addr;
	if ((sockfd = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
		perror("socket() error");
		return -1;
	}

	memset(&dest_addr, 0, sizeof(dest_addr));
	dest_addr.sin_family = AF_INET;
	dest_addr.sin_port = htons(port);
	dest_addr.sin_addr.s_addr = inet_addr(host);

	if (connect(sockfd, (struct sockaddr *)&dest_addr, sizeof(dest_addr)) < 0) {
		perror("connect() error");
		return -1;
	}
	return sockfd;

}

int main() {
	int  socket_fd;
	struct passwd *pwd;
	pwd = getpwuid(getuid());
	char ip_addr[20] = "192.168.1.40";
	int port = 8888;
	char username[20] = {0};
	strcpy(username, pwd->pw_name);
	socket_fd = socket_connect(port, ip_addr);
	if (socket_fd < 0)
	{
		exit(1);
	}
	if (send(socket_fd, username, strlen(username), 0) > 0) {
		printf("Check Success\n");
	}
	close(socket_fd);
	return 0;
}
```

gcc check.c -o check

## VIM 的简单使用

![img](https://ese3a9b6c5d0ic.prissl.qiqiuyun.net/course-activity-272/20190411093248-lntidnybu9wksckc/53eb89158008bece_img3?e=1563481633&token=ExRD5wolmUnwwITVeSEXDQXizfxTRp7vnaMKJbO-:CAFs0zlzq99uvJ2s6B6SYjVIbcI=)

### VIM 的四种模式

### 普通模式

| 命令                       | 说明                 |
| -------------------------- | -------------------- |
| x d dd ndd dw d$ d^ dG dnG | 删除说明             |
| y yy yG ynG y$ y^          | 复制                 |
| p P                        | 粘贴                 |
| gg GG ngg                  | 移动光标             |
| R cc cG cnG c$ c^          | 替换                 |
| u ctrl+r ctrl+v            | undo redo 可视块操作 |

### 插入模式

| i   | 在光标之前追加                     |
| --- | ---------------------------------- |
| a   | 在光标之后追加                     |
| A   | 在一行的结尾处追加                 |
| I   | 在一行的开头处插入                 |
| o   | 在光标所在位置的下一行打开新行插入 |
| O   | 在光标所在位置的上一行打开新行插入 |

### 命令模式

| 命令                  | 说明                   |
| --------------------- | ---------------------- |
| :w :q :wq :x :wq! :q! | 文件的保存与退出操作   |
| :args                 | 显示文件名称，切换文件 |
| :e foo.txt            | 打开 foo.txt           |
| :saveas ~/foo.txt     | 另存为~/foo.txt        |
| :split :vsplit        | 切分窗口               |
| :set                  | 设置选项               |

### 其他使用技巧

| Ctrl+z      | 挂起     |
| ----------- | -------- |
| fg          | 返回前台 |
| /findstring | 查找     |

## Python 的升级与 tldr 的升级

### 打开终端，执行命令

```
sudo apt-get install python
sudo apt-get install python3
```

### 查看 Python 版本

```
python -V
python3 -V
```

### 获取 Python 路径

```
which python
```

### 查看 Python

```
ls -al /usr/bin/python
```

### 强制删除 Python，将 Python3.5 指向 Python

```
sudo rm /usr/bin/python
sudo ln /usr/bin/python3.5 /usr/bin/python
```

### 安装 pyhton3-pip

```
sudo apt-get insatll python3-pip
```

### 升级 pip

```
pip install --upgrade pip
```

### pip3 list 报错，解决

```
sudo vim /usr/bin/pip3
```

在文本框中 pip 后加上.\_internal

### 安装 tldr

```
sudo pip install tldr
```

## Linux 极简入门

### 软件的安装与卸载

- apt-get update
- apt-get upgrade
- apt-get install xxx
- apt-get --purge remove xxx
- apt-cache search xxx

### 目录

| 命令  | 功能             |
| ----- | ---------------- |
| cd    | 切换当前目录     |
| pwd   | 打印当期目录工作 |
| mkdir | 创建目录         |

### cd 切换工作

- cd /etc 直接切换到/etc 目录

  cd .. 切换到上层目录

  cd . 切换到当前目录

  cd 回到自己的家目录

  cd ~ 回到自己的家目录

  cd - 回到上次工作目录

### pwd 打印当前工作目录

pwd [-LP]

- -L 显示逻辑工作目录
  -P 显示物理工作目录

### mkdir 创建目录

mkdir [-pm] <dir>

- -p 自动创建父目录

  -m 设置权限
