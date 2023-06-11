---
title: 剑指 Offer 38. 字符串的排列
top: false
cover: false
toc: true
mathjax: true
date: 2023-06-10 16:20:03
summary:
tags:
  - 字符串
  - 剑指Offer
categories:
  - 算法
---

## 题目描述

[力扣题目](https://leetcode.cn/problems/zi-fu-chuan-de-pai-lie-lcof/description/)

输入一个字符串，打印出该字符串中字符的所有排列。

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

示例:

输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]

限制：

1 <= s 的长度 <= 8

## 解题思路

1. 思路是采用回溯法，采用深度优先遍历的方法，先固定第一位（n 种选择），再固定第二位（n-1 种选择）......，第 n 位（1 种选择）
2. 需要注意的是不能有重复的字符，有两种方法可以解决，一是使用一个 hash 表记录出现过的字符，如果字符在 hash 表出现过，就执行`减枝`，另外一种办法是把字符串中所有字符进行排序，这样相同的字符都是相邻的，也可以过滤重复字符

## 代码实现

### Hash 表去重

```java

public class Solution {

    List<String> lists = new LinkedList<>();

    public String[] permutation(String s) {
        char[] c = s.toCharArray();
        dfs(c, 0 , s.length());
        return lists.toArray(new String[lists.size()]);
    }

    public void dfs(char[] c, int m, int n) {
        if(m == n) {
            lists.add(new String(c));
        }
        HashSet<Character> set = new HashSet<>();
        for (int i = m; i < n; i++) {
            if (!set.contains(c[i])) {
                set.add(c[i]);
                swap(c, m, i); // 交换后，从m+1开始选择
                dfs(c, m + 1, n);
                swap(c, m, i); // 还原现场
            }
        }
    }

    public void swap(char[] c, int m, int n) {
        char tmp = c[m];
        c[m] = c[n];
        c[n] = tmp;
    }
}
```

- 时间复杂度：$O(n \times n!)$，其中 n 为给定字符串的长度。这些字符的全部排列有$O(n!)$个，每个排列平均需要$O(n)$的时间来生成。

- 空间复杂度：$O(n)$。我们需要 $O(n)$的栈空间进行回溯，注意返回值不计入空间复杂度。

### 排序去重

```java

public class Solution {

    List<String> lists = new LinkedList<>();
    boolean[] vis = new boolean[10]; // 题目限制了s的长度最大为8

    public String[] permutation(String s) {
        char[] c = s.toCharArray();
        Arrays.sort(c);
        dfs(c, 0 , "");
        return lists.toArray(new String[lists.size()]);
    }

    public void dfs(char[] c, int m, String cur) {
        int n = c.length;
        if(m == n) {
            lists.add(cur);
            return;
        }
        for (int i = 0; i < n; i++) {
            if (i > 0 && !vis[i - 1] && c[i-1] == c[i]) {
                continue;
            }
            if (!vis[i]) {
                vis[i] = true;
                dfs(c, m + 1, cur + String.valueOf(c[i]));
                vis[i] = false; // 还原现场
            }
        }
    }

}
```

- 时间复杂度：$O(n \times n!)$，其中 n 为给定字符串的长度。这些字符的全部排列有$O(n!)$个，每个排列平均需要$O(n)$的时间来生成。

- 空间复杂度：$O(n)$。我们需要 $O(n)$的栈空间进行回溯，注意返回值不计入空间复杂度。
