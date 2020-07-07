---
title: Leetcode019-removeNthNodeFromEndofList
categories: leetcode
tags: [Linked List, Two Pointers, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-13 15:19:24
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a linked list, remove the n-th node from the end of list and return its head.


## Example
```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```
**Note:**

Given n will always be valid.

**Follow up:**

Could you do this in one pass?

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) return head;
        
        ListNode fast = head;
        ListNode slow = head;
        for (int i = 0; i < n; i++) fast = fast.next;
        if (fast == null) return head.next;
        while(fast.next != null){
            fast = fast.next;
            slow = slow.next;
        }
        slow.next = slow.next.next;
        return head;
    }
}
```

<hr />