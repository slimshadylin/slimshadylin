---
title: Algorithm-链表
top: false
cover: false
toc: true
mathjax: false
date: 2020-12-18 19:54:28
password:
summary: 链表相关的基本操作
tags:
  - 链表
categories:
  - 算法
---

## 单链表

1. 定义：包含节点的值和指向下一个节点的指针

   ```java
   public class Node {
       public int value;
       public Node next;

       public Node(int value) {
           this.value = value;
       }
   }
   ```

2. 单链表的反转

   - 遍历法，在对链表每个节点进行遍历的过程中进行指针的反转
     ![反转流程](NodeReverse.png)

   - java 代码

   ```java
   public class NodeReverse {
       public static class Node {
           public int value;
           public Node next;

           public Node(int value) {
               this.value = value;
           }

           public static Node reverseNode(Node head) {
               if (head == null) {
                   return null;
               }
               Node pre = null;
               Node next = null;
               while (head != null) {
                   next = head.next;
                   head.next = pre;
                   pre = head;
                   head = next;
               }
               return pre;
           }

           public static void main(String[] args) {
               Node head = new Node(1);
               head.next = new Node(2);
               head.next.next = new Node(3);
               head.next.next.next = new Node(4);
               Node newNode = reverseNode(head);
               System.out.println(newNode.value);
               System.out.println(newNode.next.value);
               System.out.println(newNode.next.next.value);
               System.out.println(newNode.next.next.next.value);
           }
       }
   }
   ```

3. 单链表删除指定数值

   - 需要注意删除的数值是头节点时，而且可能是连续的

   - 删除时，需要删除所有的值，而不是删除第一个

   java 代码：

   ```java
   public class DeleteNode {
       public static class Node {
           public int value;
           public Node next;

           public Node(int value) {
               this.value = value
           }
       }

       public static Node deleteNode(Node head, int value) {
           // 首先删除头节点=value的所有节点，可能会有连续多个，全部删除
           while (head != null) {
               if (head.value != value) {
                   break;
               }
               head = head.next;
           }
           // 来到第一个不需要删除的节点，这个节点是返回的头节点
           Node pre = head;
           Node cur = head;
           while (cur != null) {
               if (cur.value == value) {
                   pre.next = cur.next;
               } else {
                   pre = cur;
               }
               cur = cur.next;
           }
           return head;
       }
   }
   ```

## 双向链表

1. 定义

   ```java
   public class DoubleNode {
       public int value;
       public DoubleNode last;
       public DoubleNode next;

       public DoubleNode(int value) {
           this.value = value;
       }
   }
   ```

2. 链表反转

   ```java
   public class ReverseDoubleNode {
       public static class DoubleNode {
           public int value;
           public DoubleNode last;
           public DoubleNode next;

           public DoubleNode(int value) {
               this.value = value;
           }
       }

       public static DoubleNode reverseDoubleNode(DoubleNode head) {
           if (head == null) {
               return null;
           }
           DoubleNode pre = null;
           DoubleNode next;
           while (head != null) {
               next = head.next;
               head.last = next;
               head.next = pre;
               pre = head;
               head = next;
           }
           return pre;
       }

       // for test
       public static void main(String[] args) {
           DoubleNode head = new DoubleNode(1);
           head.next = new DoubleNode(2);
           head.next.next = new DoubleNode(3);
           head.next.next.next = new DoubleNode(4);
           DoubleNode cur = reverseDoubleNode(head);
           while (cur != null) {
               System.out.println(cur.value);
               cur = cur.next;
           }
       }
   }
   ```

3. 链表删除指定值

   ```java
   public class DeleteDoubleNode {
       public static class DoubleNode {
           public int value;
           public DoubleNode last;
           public DoubleNode next;

           public DoubleNode(int value) {
               this.value = value;
           }
       }

       public static DoubleNode deleteDoubleNode(DoubleNode head, int value) {
           // 从链表头开始，删除连续的值等于value的节点
           while (head != null) {
               if (head.value != value) {
                   break;
               }
               head = head.next;
           }
           // head来到第一个不需要删的位置
           DoubleNode pre = head;
           DoubleNode cur = head.next;
           while (cur != null) {
               if (cur.value == value) {
                   pre.next = cur.next;
               } else {
                   pre.next = cur;
                   cur.last = pre;
                   pre = cur;
               }
               cur = cur.next;
           }
           return head;
       }

       public static void main(String[] args) {
           DoubleNode head = new DoubleNode(1);
           DoubleNode node1 = new DoubleNode(3);
           node1.last = head;
           head.next = node1;
           DoubleNode node2 = new DoubleNode(3);
           node2.last = node1;
           node1.next = node2;
           DoubleNode node3 = new DoubleNode(5);
           node3.last = node2;
           node2.next = node3;
           DoubleNode node4 = new DoubleNode(6);
           node4.last = node3;
           node3.next = node4;
           DoubleNode node5 = new DoubleNode(3);
           node5.last = node4;
           node4.next = node5;
           DoubleNode pt = head;
           while (pt != null) {
               System.out.println(pt.value);
               pt = pt.next;
           }
           System.out.println("===============");

           DoubleNode temp = deleteDoubleNode(head, 3);
           while (temp != null) {
               System.out.println(temp.value);
               temp = temp.next;
           }
       }
   }
   ```

## 双向链表实现队列

包含添加、删除、判断是否为空、返回 size 大小 4 个函数

```java
public class DoubleNodeToQueue {
    public static class Node<T> {
        public T value;
        public Node<T> pre;
        public Node<T> next;

        public Node (T value) {
            this.value = value;
        }
    }

    // 双向链表操作
    public static class DoubleEndsQueue {
        public Node<T> head;
        public Node<T> tail;
    }

}

```

# Master 公式

master 公式是用于计算分治策略解决问题时的时间复杂度分析策略

$$
T [n] = aT[\frac{n}{b}] + T (N^d)
$$

其中 a >= 1 and b > 1 是常量，其表示的意义是 n 表示问题的规模，a 表示递归的次数也就是生成的子问题数，b 表示每次递归是原来的 1/b 之一个规模，f（n）表示分解和合并所要花费的时间之和。

解法：

- 当$d<\log_{b}{a}$时，时间复杂度为$O\left(n^{\log_{b}{a}}\right)$
- 当$d=\log_{b}{a}$时，时间复杂度为$O\left(n^{d}*\log{n}\right)$
- 当$d>\log_{b}{a}$时，时间复杂度为$O\left(n^d\right)$
