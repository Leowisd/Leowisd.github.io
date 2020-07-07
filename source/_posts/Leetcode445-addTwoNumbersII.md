---
title: Leetcode445-addTwoNumbersII
categories: leetcode
tags: [Linked List, Microsoft, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-21 16:23:34
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

## Example
```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

## Solution
Can use Stack instead of List to store these two numbers
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if (l1 == null && l2 == null) return l1;
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        
        List<Integer> num1 = new ArrayList<>();
        List<Integer> num2 = new ArrayList<>();
        while(l1 != null){
            num1.add(l1.val);
            l1 = l1.next;
        }
        while(l2 != null){
            num2.add(l2.val);
            l2 = l2.next;
        }
        
        int i = num1.size()-1;
        int j = num2.size()-1;
        int d = 0;
        List<Integer> res = new ArrayList<>();
        while(i >= 0 && j >= 0){
            int tmp = num1.get(i) + num2.get(j) + d;
            d = tmp /10;
            res.add(tmp%10);
            i--;
            j--;
        }
        if (i >= 0){
            for (int k = i; k >= 0; k--){
                int tmp = num1.get(k) + d; 
                res.add(tmp%10);
                d = tmp/10;
            }
        }
        else if (j >= 0){
            for (int k = j; k >= 0; k--){
                int tmp = num2.get(k) + d; 
                res.add(tmp%10);
                d = tmp/10;
            }
        }
        if (d > 0) res.add(1);
        
        ListNode head = new ListNode(0);
        ListNode cur = head;
        for (int k = res.size()-1; k >= 0; k--){
            cur.next = new ListNode(res.get(k));
            cur = cur.next;
        }
        return head.next;
    }
}
```

<hr />