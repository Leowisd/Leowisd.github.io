---
title: Leetcode141-linkedListCycle
categories: leetcode
tags: [LinkedList]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-19 22:06:14
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

## Example

**Example 1:**
```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

**Example 2:**
```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

**Example 3:**
```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```
## Solution
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {        
        if (head == null) return false;
        ListNode p = head;
        while (p != null){
            if (p.next == head) return true;
            ListNode tmp = p.next;
            p.next = head;
            p = tmp;
        }
        return false;
        // Excellent Method, but logical
        // ListNode slow = head;
        // ListNode fast = head;
        // while (fast.next != null && fast.next.next != null){
        //     slow = slow.next;
        //     fast = fast.next.next;
        //     if (slow == fast) return true;
        // }
        // return false;

        
    }
}
```

<hr />