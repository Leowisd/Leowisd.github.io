---
title: Leetcode206-reverseLinkedList
categories: leetcode
tags: [LinkedList]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-18 23:10:22
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Reverse a singly linked list.

## Example
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```
**Follow up:**
A linked list can be reversed either iteratively or recursively. Could you implement both?


## Solution
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode Recursion(ListNode head, ListNode newHead){
        if (head == null){
            return newHead;
        }
        ListNode next = head.next;
        head.next = newHead;
        return Recursion(next, head);
    }
    
    public ListNode reverseList(ListNode head) {
        // ListNode newHead = null;
        // while (head != null){
        //     ListNode next = head.next;
        //     head.next = newHead;
        //     newHead = head;
        //     head = next;
        // }
        // return newHead;
        return Recursion(head, null);
    }
}
```

<hr />