---
title: printf
date: 2022-03-27T22:59:11+08:00
draft: true
---
printf输出颜色和ANSI控制码(高亮,下划线,闪烁,光标位置,清屏等)

颜色：

#define NONE "/033[m"

#define RED "/033[0;32;31m"

#define LIGHT_RED "/033[1;31m"

#define GREEN "/033[0;32;32m"

#define LIGHT_GREEN "/033[1;32m"

#define BLUE "/033[0;32;34m"

#define LIGHT_BLUE "/033[1;34m"

#define DARY_GRAY "/033[1;30m"

#define CYAN "/033[0;36m"

#define LIGHT_CYAN "/033[1;36m"

#define PURPLE "/033[0;35m"

#define LIGHT_PURPLE "/033[1;35m"

#define BROWN "/033[0;33m"

#define YELLOW "/033[1;33m"

#define LIGHT_GRAY "/033[0;37m"

#define WHITE "/033[1;37m"

比如：

printf("/033[31m ####-----&gt;&gt; /033[32m" "hello/n" "/033[m")

int main()

{

printf( CYAN "current function is %s " GREEN " file line is %d/n" NONE,

__FUNCTION__, __LINE__ );

fprintf(stderr, RED "current function is %s " BLUE " file line is %d/n" NONE,

__FUNCTION__, __LINE__ );

return 0;

}

颜色分为背景色和字体色，30~39用来设置字体色，40~49设置背景：

背景色 字体色

40: 黑 30: 黑

41: 红 31: 红

42: 绿 32: 绿

43: 黄 33: 黄

44: 蓝 34: 蓝

45: 紫 35: 紫

46: 深绿 36: 深绿

47: 白色 37: 白色

记得在打印完之后，把颜色恢复成NONE，不然再后面的打印都会跟着变色。

另外，还可以加一些ANSI控制码。加颜色只是以下控制码中的一种：

/033[0m 关闭所有属性

/033[1m 设置高亮度

/033[4m 下划线

/033[5m 闪烁

/033[7m 反显

/033[8m 消隐

/033[30m -- /033[37m 设置前景色

/033[40m -- /033[47m 设置背景色

/033[nA 光标上移n行

/033[nB 光标下移n行

/033[nC 光标右移n行

/033[nD 光标左移n行

/033[y;xH设置光标位置

/033[2J 清屏

/033[K 清除从光标到行尾的内容

/033[s 保存光标位置

/033[u 恢复光标位置

/033[?25l 隐藏光标

/033[?25h 显示光标
