---
title: note4
date: 2022-03-27T22:59:11+08:00
draft: true
---

# DAY05

## 输出函数说明

printf 函数

- 头文件:stdio.h
- 原型:int printf(const char \*format,...);
- format:格式控制字符串
- ...:可变参数列表
- 返回值:输出字符类型

## 输出函数说明

scanf 函数

- 头文件:stdio.h
- 原型:int scanf(const char \*format,...);
- format:格式控制字符
- ...:可变参数列表
- 返回值:成功读入列表

请使用 printf 函数,求解一个数字 n 的十进制表示的数字位数

```
#include<stdio.h>
int main(){
    int n;
    while(scanf("%d",&n)!=EOF){
        printf(" has %d digits\n",printf("%d",n));
    }
    return 0;
}
```

请写一个程序,读入一个行字符串(可能包含空格),输出这个字符串中字符的数量

```
#include<stdio.h>
int main(){
    char str[100];
    while(scanf("%[^\n]s",str)!=EOF) {
        getchar();
        printf(" has %d chars\n",printf("%s",str));
    }
    return 0;
}
```

## sprintf 和 fprintf 代码演示

```
#include <stdio.h>
#define swap(a, b) { \
    __typeof(a) temp = a;\
    a = b, b = temp; \
}

int main() {
    printf("%c\n", 97);
    int n;
    scanf("%d", &n);
    printf("%04d\n", n);
    char str[100], buff[100], *p = str, *q = buff;
    sprintf(str, "%d.%d.%d.%d", 192,168,1,10);
    printf("str=%s\n", str);
    if (n & 1) {
        sprintf(q, "(%s)", p);
        swap(p, q);
    }
    if (n & 2) {
        sprintf(q, "[%s]", p);
        swap(p, q);
    }
    if (n & 4) {
        sprintf(q, "{%s}", p);
        swap(p, q);
    }
    FILE *fout = fopen("output", "w");
    fprintf(stdout, "stdout = %s\n", p);
    fprintf(stderr, "stderr = %s\n", p);
    return 0;
}
```
