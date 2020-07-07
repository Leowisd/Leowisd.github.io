---
title: Leetcode143-reorderList
categories: leetcode
tags: [Linked List]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-07 23:21:05
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.

## Example

**Example 1** 
```
Given 1->2->3->4, reorder it to 1->4->2->3.
```
**Example 2**
```
Given 1->2->3->4->5, reorder it to 1->5->2->4->3.

```

## Solution
**Solution 1**
Not the best
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
    public void reorderList(ListNode head) {
        if (head == null) return;
        List<ListNode> nodeList = new ArrayList<>();
        ListNode tmp = head;
        while(tmp != null){
            nodeList.add(tmp);
            tmp = tmp.next;
        }
        
        int left = 0;
        int right = nodeList.size()-1;
        ListNode cur = head;
        while(left < right){
            nodeList.get(right).next = nodeList.get(left).next;
            nodeList.get(left).next = nodeList.get(right);
            nodeList.get(right-1).next = null;
//          Speed more better
//          ListNode tmpNode = nodeList.get(left).next;
//          nodeList.get(left).next = nodeList.get(right);
//          cur.next.next = tmpNode;
//          nodeList.get(right-1).next = null;
//          cur = tmpNode;
            left ++;
            right --;
        }
        if (left > right){
            nodeList.get(left).next = null;
            nodeList.get(right).next = nodeList.get(left);  
        }
    }
```
**Solution 2**
Best
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
    public void reorderList(ListNode head) {
            if(head==null||head.next==null) return;
            
            //Find the middle of the list
            ListNode p1=head;
            ListNode p2=head;
            while(p2.next!=null&&p2.next.next!=null){ 
                p1=p1.next;
                p2=p2.next.next;
            }
            
            //Reverse the half after middle  1->2->3->4->5->6 to 1->2->3->6->5->4
            ListNode preMiddle=p1;
            ListNode preCurrent=p1.next;
            while(preCurrent.next!=null){
                ListNode current=preCurrent.next;
                preCurrent.next=current.next;
                current.next=preMiddle.next;
                preMiddle.next=current;
            }
            
            //Start reorder one by one  1->2->3->6->5->4 to 1->6->2->5->3->4
            p1=head;
            p2=preMiddle.next;
            while(p1!=preMiddle){
                preMiddle.next=p2.next;
                p2.next=p1.next;
                p1.next=p2;
                p1=p2.next;
                p2=preMiddle.next;
            }
        }
}
```

<hr />