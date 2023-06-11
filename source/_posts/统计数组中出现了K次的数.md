---
title: 统计数组中出现了K次的数
top: false
cover: false
toc: true
mathjax: false
date: 2023-03-20 12:49:47
summary:
tags:
  - leetcode
categories:
  - 算法
  - 位运算
---

## 题目描述

题目：一个数组中一种数出现了 K 次，其他数都出现了 M 次（M > 1，K < M），找出出现了 K 次的数，如果这种数出现的次数不是 K 次，则返回 -1。

要求：额外空间复杂度为 O ( 1 )，时间复杂度为 O ( n )

思路：任何形式的数都能转化成数组形式的二进制，申请一个固定数组 int t[32]，每个数字的二进制位的 1 累加到 t 中，通过 t 中每个元素是否为 M 的整数倍而确定初选了 K 次的数的每个二进制位。

## 代码实现

```java

public int getKTimes(int arr, int k, int m) {
    int[] help = new int[32];
    for (int num : arr) {
        for (int i =0; i < 32; i++) {
            help[i] += (num >> 1) & 1;
        }
    }
    int ans = 0;
    for (int i = 0; i < 32; i++) {
        help[i] %= m;
        if (help[i] != 0) {
            ans |= 1 << i;
        }
    }
    int real = 0;
    for (int num: arr) {
        if (nums == ans) {
            real++;
        }
    }
    return real == k ? ans : -1;
}

```
