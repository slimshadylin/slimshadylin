---
title: 4.Median of Two Sorted Arrays
top: false
cover: false
toc: true
mathjax: true
date: 2021-01-05 10:51:23
password:
summary:
tags:
- leetcode
categories:
- leetcode
---

## 题目

Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

Follow up: The overall run time complexity should be O(log (m+n)).

Example 1:

Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
Example 2:

Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
Example 3:

Input: nums1 = [0,0], nums2 = [0,0]
Output: 0.00000
Example 4:

Input: nums1 = [], nums2 = [1]
Output: 1.00000
Example 5:

Input: nums1 = [2], nums2 = []
Output: 2.00000

Constraints:

nums1.length == m
nums2.length == n
0 <= m <= 1000
0 <= n <= 1000
1 <= m + n <= 2000
-106 <= nums1[i], nums2[i] <= 106

## 题目大意

给定两个有序的数组nums1和nums2.
请找出这两个有序数组的中位数，且时间复杂度需要达到$O\left(\log(m+n)\right)$.

## 解题思路

[leetcode最高赞评论的中文翻译](https://zhuanlan.zhihu.com/p/70654378)

1. 首先看到时间复杂度，必然会想到要使用二分.

2. 由于数组是有序的，那么二分过后左半部分必然会小于右半部分(假设从小到大排序).

3. 比较麻烦的就是二分中点的问题，如果是奇数就是中间的数值，如果是偶数个，那么是中间两个值的平均值.

4. 

## 代码实现
