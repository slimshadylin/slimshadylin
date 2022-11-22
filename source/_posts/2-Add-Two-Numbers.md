---
title: 2.Add Two Numbers
top: false
cover: false
toc: true
mathjax: true
date: 2021-01-05 16:08:14
password:
summary:
tags:
- leetcode
categories:
- 算法
---

# 题目

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example 1:

![Example 1](http://rlf7zdk5v.hn-bkt.clouddn.com/1.jpg)

Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]
Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]

Constraints:

The number of nodes in each linked list is in the range [1, 100].
0 <= Node.val <= 9
It is guaranteed that the list represents a number that does not have leading zeros.

### 题目大意

1. 两个链表表示两个数字，但是数字的值需要反转链表后得到.

2. 两个数相加之后再反转链表就能得到结果.

3. 题目会保证数据链表的头节点不会为零.

## 解体思路

1. 两个数字长度不相等时，短的链表末尾补零.

2. 需要处理进位的问题，极端情况可能需要新加一个节点，比如999+1=1000.

## 代码实现

``` java
public class Solution {
    public static class ListNode {
        int val;
        ListNode next;
        public ListNode(int val) {
            this.val = val;
        }
        public ListNode(int val, ListNode next) {
            this.val = val;
            this.next = next;
        }
    }

    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(0);
        ListNode cur = head;
        int carry = 0, x1 = 0, x2 = 0, sum = 0;
        while (l1 != null || l2 != null) {
            x1 = l1 == null ? 0 : l1.val;
            x2 = l2 == null ? 0 : l2.val;
            sum = l1 + l2 + carry;
            // 两个数相加最多等于18，所以进位只能是0或者1
            carry = sum > 9 ? 1 : 0 ;
            sum = sum % 10;
            cur.next = new ListNode(sum);
            cur = cur.next;
            if (l1 != null) {
                l1 = l1.next;
            }
            if (l2 != null) {
                l2 = l2.next;
            }
        }
        // 如果l1和l2都没有节点了，但是有进位，需要补一个节点
        if (carry == 1) {
            cur.next = new ListNode(1);
        }
        return head.next;
    }
}

```

![运行结果](result.png)
