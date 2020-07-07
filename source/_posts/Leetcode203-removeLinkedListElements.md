---
title: Leetcode203-removeLinkedListElements
categories: leetcode
tags: [Linked List, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-20 18:00:02
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Remove all elements from a linked list of integers that have value val.

## Example
```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```

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
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) return head;
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode cur = head;
        ListNode pre = dummy;
        while(cur != null){
            if (cur.val == val)
                pre.next = cur.next;
            else pre = cur;
            cur = cur.next;
        }
        return dummy.next;
    }
}
```

<hr />