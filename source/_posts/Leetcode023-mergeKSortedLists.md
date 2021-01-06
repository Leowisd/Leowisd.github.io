---
title: Leetcode023-mergeKSortedLists
categories: leetcode
tags: [Heap, Divide and Conquer, Amazon, Bloomberg, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-07 15:44:56
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

## Example
```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

## Solution
Devide and Conquer, O(NlogK)
```java
// Devide and Conquer, O(NlogK)
class Solution{
    public static ListNode mergeKLists(ListNode[] lists){
        return partion(lists,0,lists.length-1);
    }

    public static ListNode partion(ListNode[] lists,int s,int e){
        if(s==e)  return lists[s];
        if(s<e){
            int q=(s+e)/2;
            ListNode l1=partion(lists,s,q);
            ListNode l2=partion(lists,q+1,e);
            return merge(l1,l2);
        }else
            return null;
    }

    //This function is from Merge Two Sorted Lists.
    public static ListNode merge(ListNode l1,ListNode l2){
        if(l1==null) return l2;
        if(l2==null) return l1;
        if(l1.val<l2.val){
            l1.next=merge(l1.next,l2);
            return l1;
        }else{
            l2.next=merge(l1,l2.next);
            return l2;
        }
    }   
}
```

Heap, O(NlogN)
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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;

        // PriorityQueue<ListNode> pq = new PriorityQueue<>((a,b) -> a.val - b.val); //36ms
        PriorityQueue<ListNode> pq = new PriorityQueue<ListNode>(new Comparator<ListNode>(){
            @Override
            public int compare(ListNode a, ListNode b){
                return a.val-b.val;
            }
        }); //5ms
        for (ListNode it: lists)
            if (it != null) pq.offer(it);
            
        ListNode res = new ListNode(0);
        ListNode cur = res;
        while(!pq.isEmpty()){
            cur.next = pq.poll();
            cur = cur.next;
            if (cur.next != null) pq.offer(cur.next);
        }   
        return res.next;
    }
}
```

<hr />