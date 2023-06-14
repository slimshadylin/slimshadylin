---
title: 剑指 Offer 29. 顺时针打印矩阵
top: false
cover: false
toc: true
mathjax: false
date: 2023-06-11 22:05:06
summary:
tags:
categories:
---

## 题目描述

[力扣题目](https://leetcode.cn/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

示例 1：

输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
示例 2：

输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]

限制：

0 <= matrix.length <= 100
0 <= matrix[i].length <= 100

## 解题思路

1. 模拟循环，根据顺序`从左到右`，`从上到下`，`从右到左`，`从下到上`进行遍历，重复操作，直到所有的字符都被遍历过即可

## 代码实现

```java

public class Solution {

}

```
