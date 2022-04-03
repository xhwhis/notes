---
title: javascript学习note
date: 2022-03-27T22:59:11+08:00
draft: true
---

## js语法

### js语法学习[demo](https://github.com/lws597/web/tree/master/js)

js作为一个脚本语言，语法学习简单。其中typeof操作符较为有意思，无类型语言竟然还有类型检查机制，回头给[自制语言](https://github.com/lws597/xlang)添加一个typeof关键字。js的null和true/false为保留关键字，[自制语言](https://github.com/lws597/xlang)的null和true/false也可设置为关键字，直接解析成0/1



### var & let & const

let 声明的变量只在 let 命令所在的代码块内有效
const 声明一个只读的常量，一旦声明，常量的值就不能改变

for循环{}中多用let



### for...in & for...of

在循环对象属性的时候，使用for…in，for…in循环得到的是key
在遍历数组的时候的时候使用for…of，for…of循环得到的是value

```javascript
for(let index in aArray) {
    console.log(aArray[index]);
}

for(let value of aArray) {
    console.log(value);
}
```



### >> & >>>

运算符>>>执行无符号右移位运算。它把无符号的32位整数所有数位整体右移。对于无符号数或正数右移运算，无符号右移与有符号右移运算的结果是相同的

```javascript
console.log(1000 >> 8);  //返回值3
console.log(1000 >>> 8);  //返回值3
```

对于负数来说，无符号右移将使用0来填充所有的空位，同时会把负数作为正数来处理，所得结果会非常大

```javascript
console.log(-1000 >> 8);  //返回值 -4
console.log(-1000 >>> 8);  //返回值 16777212
```



## js刷题

### [leetcode1189](https://leetcode-cn.com/problems/maximum-number-of-balloons)

```javascript
/*
 * @lc app=leetcode.cn id=1189 lang=javascript
 *
 * [1189] “气球” 的最大数量
 */

// @lc code=start
/**
 * @param {string} text
 * @return {number}
 */
var maxNumberOfBalloons = function(text) {
    let map = {'a' : 0, 'b' : 0, 'o' : 0, 'l' : 0, 'n' : 0};
    for (let ch of text) {
        map[ch]++;
    }
    return Math.min(map['a'], map['b'], map['o'] >> 1, map['l'] >> 1, map['n']);
};
// @lc code=end


```



### [leetcode944](https://leetcode-cn.com/problems/delete-columns-to-make-sorted)

```javascript
/*
 * @lc app=leetcode.cn id=944 lang=javascript
 *
 * [944] 删列造序
 */

// @lc code=start
/**
 * @param {string[]} strs
 * @return {number}
 */
var minDeletionSize = function(strs) {
    var ans = 0;
    for (let i = 0; i < strs[0].length; i++) {
        for (let j = 0; j < strs.length - 1; j++) {
            if (strs[j][i] > strs[j + 1][i]) {
                ans++;
                break;
            }
        }
    }
    return ans;
};
// @lc code=end


```



### [leetcode908](https://leetcode-cn.com/problems/smallest-range-i)

```javascript
/*
 * @lc app=leetcode.cn id=908 lang=javascript
 *
 * [908] 最小差值 I
 */

// @lc code=start
/**
 * @param {number[]} A
 * @param {number} K
 * @return {number}
 */
var smallestRangeI = function(A, K) {
    if (A.length == 1) {
        return 0;
    }
    var delta = Math.max.apply(null, A) - Math.min.apply(null, A) - (K << 1);
    return delta < 0 ? 0 : delta;
};
// @lc code=end


```



### [leetcode38](https://leetcode-cn.com/problems/count-and-say)

```javascript
/*
 * @lc app=leetcode.cn id=38 lang=javascript
 *
 * [38] 外观数列
 */

// @lc code=start
/**
 * @param {number} n
 * @return {string}
 */
var countAndSay = function(n) {
    var pre = "1", cur = "1";
    for (let i = 1; i < n; i++) {
        pre = cur;
        cur = "";
        let l = 0, r = 0;
        while (r < pre.length) {
            while (pre[l] === pre[r] && r < pre.length) {
                r++;
            }
            cur += (r - l).toString() + pre[l];
            l = r;
        }
    }
    return cur;
};
// @lc code=end


```
