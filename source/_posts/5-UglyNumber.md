---
title: 5.UglyNumber
top: false
cover: false
toc: true
mathjax: false
date: 2022-11-18 15:30:44
summary:
tags:
- leetcode
categories:
- leetcode
---

## 题目

https://leetcode.com/problems/ugly-number/

## 题目大意

定义了一种数字丑数：只能被2、3、5整除，

## 解题思路

简单的方法是用给定的数字除5、3、2，递归执行，最后剩下1表示能整除

## 代码实现

```
class Solution {
    public boolean isUgly(int n) {
        while (n >0 && n%5 == 0) {
            n = n/5;
        }
        while (n >0 && n%3 == 0) {
            n = n/3;
        }
        while (n >0 && n%2 == 0) {
            n = n/2;
        }
        return n==1;
    }
}
```
