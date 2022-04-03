---
title: cpp_stl
date: 2022-03-27T22:59:11+08:00
draft: true
---
# c++ stl



## queue-类说明

queue类：队列

- 头文件：queue
- 命名空间：std
- 声明：queue<data_type> q;

| q.fornt() | 查看队首元素 |
| :-------- | ------------ |
| q.empty() | 队列判空     |
| q.push()  | 入队         |
| q.pop()   | 出队         |
| q.size()  | 队列元素数量 |



## stack-类说明

stack类：栈

- 头文件：stack
- 命名空间：std
- 声明：stack<data_type> s;

| s.top()   | 查看栈顶元素 |
| --------- | ------------ |
| s.empty() | 栈判空       |
| s.push()  | 入栈         |
| s.pop()类 | 出栈         |
| s.size()  | 栈元素数量   |



## string-类说明

string类：字符串

- 头文件：string
- 命名空间：std
- 声明：string str1, str2;

| str1 == str2  | 字符串判等 |
| ------------- | ---------- |
| str1 < str2   | 字典序小于 |
| str1 > str2   | 字典序大于 |
| str1 += str2  | 字符串连接 |
| str1.length() | 字符串长度 |



### string (hzoj-166)

```c++
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1, str2;
    int n;
    cin >> str1 >> n >> str2;
    cout << min(str1.length(), (size_t)100) << endl;
    str1.insert(n - 1, str2);
    cout << str1 << endl;
    cout << str1.length() - str1.rfind('x') << endl;
    return 0;
}
```



## hash_map-类说明

hash_map类：字符串

- 头文件：<hash_map> / <ext/hash_map>
- 命名空间：__gnu_cxx
- 声明：hash_map<key_type, value_type, hash_func> h;

| h.find(key)    | 判断某个key值是否在hash_map中 |
| -------------- | ----------------------------- |
| h[key] = value | 将value存储在key位上          |
| h[key]         | 房屋key值对应的value          |
| h.begin()      | 哈希表的起始位置              |
| h.end()        | 哈希表的结束位置              |



## unordered_map-类说明（c++11标准）

unordered_map-类：字符串

- 头文件：unordered_map
- 命名空间：std
- 声明：unordered_map<key_type, value_type, hash_func> h;

| h.find(key)    | 判断某个key值是否在unordered_map中 |
| -------------- | ---------------------------------- |
| h[key] = value | 将value存储在key位上               |
| h[key]         | 访问key值对应的value               |
| h.begin()      | 哈希表的起始位置                   |
| h.end()        | 哈希表的结束位置                   |



### sort (hzoj-245)

```c++
#include <iostream>
#include <algorithm>
#define max_n 100000
using namespace std;

int a[max_n + 5];

int main() {
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }
    sort(a, a + n);
    int p = a[n >> 1], ans = 0;
    for (int i = 0; i < n; i++) {
        ans += abs(p - a[i]);
    }
    cout << ans << endl;
    return 0;
}
```



### nth_element (hzoj-245)

nth_element是部分排序算法，它重排[first, last)中元素，使得：

- nth所指向的元素被更改为假如[first, last)已排序则该位置会出现的元素。
- 这个新的nth元素前的所有元素小于或等于新的 nth 元素后的所有元素。

更正式而言，nth_element以升序部分排序范围[first, last)，使得对于任何范围[first, nth)中的i和任何范围[nth, last)中的j，都满足条件!(*j < i)。置于nth位置的元素则准确地是假如完全排序范围则应出现于此位置的元素。

```c++
#include <iostream>
#include <algorithm>
#define max_n 100000
using namespace std;

int a[max_n + 5], ind[max_n + 5];

int main() {
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }
    nth_element(a, a + (n >> 1), a + n);
    int p = a[n >> 1], ans = 0;
    for (int i = 0; i < n; i++) {
        ans += abs(p - a[i]);
    }
    cout << ans << endl;
    return 0;
}
```



### map

```c++
#include <iostream>
#include <set>
#include <map>
using namespace std;

int main() {
    string name;
    int n, age;
    set<int> s;
    s.insert(3);
    s.insert(5);
    s.insert(2);
    s.insert(3);
    cout << *s.begin() << endl;
    s.erase(s.begin());
    for (auto iter = s.begin(); iter != s.end(); iter++) {
        cout << *iter << " ";
    }
    cout << endl;
    map<int, string> arr;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> age >> name;
        arr[age] = name;
    }
    for (auto iter = arr.begin(); iter != arr.end(); iter++) {
        cout << iter->second << endl; 
    }
    return 0;
}
```



### 存储任意类型的数组 (vector->array)

```c++
#include <iostream>
#include <vector>
using namespace std;

template<typename T>
class Array {
public :
    Array() {
        this->__size = 10;
        this->__cnt  = 0;
        this->data = new T[this->__size];
    }
    Array(int n) {
        this->__size = 2 * n;
        this->__cnt  = n;
        this->data = new T[this->__size];
    }
    void push_back(const T &a) {
        new(this->data + ((this->__cnt)++)) T(a);
    }
    int size() {
        return this->__cnt;
    }
    T &operator[](int ind) {
        return this->data[ind];
    }

private:
    T *data;
    int __size, __cnt;
};

int main() {
    vector<int> arr(10);
    Array<int> arr2(10);
    cout << arr.size() << endl;
    arr.push_back(123);
    cout << arr[0] << endl;
    cout << arr.size() << endl; 
    cout << arr2.size() << endl;
    arr2.push_back(123);
    cout << arr2[0] << endl;
    cout << arr2.size() << endl;
    return 0;
}
```
