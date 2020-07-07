---
title: Leetcode234-palindromeLinkedList
categories: leetcode
tags: [Linked List, Two Pointers, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 23:11:09
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a singly linked list, determine if it is a palindrome.

## Example
**Example 1:**
```
Input: 1->2
Output: false
```
**Example 2:**
```
Input: 1->2->2->1
Output: true
```
**Follow up:**

Could you do it in O(n) time and O(1) space?

## Solution

1. Move: fast pointer goes to the end, and slow goes to the middle.
2. Reverse: the right half is reversed, and slow pointer becomes the 2nd head.
3. Compare: run the two pointers head and slow together and compare.

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
    public boolean isPalindrome(ListNode head) {
        ListNode fast = head, slow = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        if (fast != null) { // odd nodes: let right half smaller
            slow = slow.next;
        }
        slow = reverse(slow);
        fast = head;
    
        while (slow != null) {
            if (fast.val != slow.val) {
                return false;
            }
            fast = fast.next;
            slow = slow.next;
        }
        return true;
    }

    public ListNode reverse(ListNode head) {
        ListNode prev = null;
        while (head != null) {
            ListNode next = head.next;
            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
}
```

<hr />