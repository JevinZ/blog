---
title: leetcode-573-复数乘法
catalog: true
date: 2021-10-03 22:46:35
subtitle:
header-img:
tags: [刷题,数学专题,medium,新知识]
categories: 刷题
---

### 1.新知识！
#### 1.sscanf固定格式读入字符
```cpp
sscanf(num1.c_str(),"%d+%di",&a1,&b1);//固定格式读入复数
```
#### 2.c++ String 转 c 字符串
```cpp
num1.c_str() //num1字符串转为c中的字符串
```
#### 3.c++ 数字转字符串
```cpp
return string(to_string(aa)+"+"+to_string(bb)+"i");//int aa转化成string 利用to_string函数
```
### 2.题目描述
复数 可以用字符串表示，遵循 "实部+虚部i" 的形式，并满足下述条件：

实部 是一个整数，取值范围是 [-100, 100]
虚部 也是一个整数，取值范围是 [-100, 100]
i2 == -1
给你两个字符串表示的复数 num1 和 num2 ，请你遵循复数表示形式，返回表示它们乘积的字符串。

链接：https://leetcode-cn.com/problems/complex-number-multiplication

### 3.解题思路

解题思路比较简单，主要处理好字符串的读入和输出，运算部分比较简单，这次输入使用sscanf完成固定格式的输入，使用to_string()将数字转化为字符串。

### 4.代码
```cpp
class Solution {
public:
    string complexNumberMultiply(string num1, string num2) {
        int a1,a2,b1,b2;
        sscanf(num1.c_str(),"%d+%di",&a1,&b1);
        sscanf(num2.c_str(),"%d+%di",&a2,&b2);
        int aa = a1*a2-b1*b2;
        int bb = b1*a2+b2*a1;
        return string(to_string(aa)+"+"+to_string(bb)+"i");
    }
};
```
