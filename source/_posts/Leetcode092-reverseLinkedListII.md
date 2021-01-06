---
title: Leetcode092-reverseLinkedListII
categories: leetcode
tags: [Linked List, Bloomberg, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 22:02:25
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Reverse a linked list from position m to n. Do it in one-pass.

Note: 1 ≤ m ≤ n ≤ length of list.

## Example
```
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

## Solution

It basically does two things:
1. start, which records mNode, bubbles up step by step to where the nNode originally is; start node never change, it is always the mNode;
2. next, which is always the next node of start (obviously it changes every time), is repeatedly being put to the next position of the pre node ( pre node doesn't change either), so that nodes between pre (not include) and start (include) is always in descending order.

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
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null) return null;
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode pre = dummy;    
        for (int i = 0; i < m - 1; i++) pre = pre.next;
        ListNode start = pre.next;
        ListNode next = start.next;
        
        for (int i = 0; i < n - m; i++){
            start.next = next.next;
            next.next = pre.next;
            pre.next = next;
            next = start.next;          
        }
        
        return dummy.next;
    }
}
```

<hr />