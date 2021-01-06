---
title: Leetcode138-copyListWithRandomPointer
categories: leetcode
tags: [LinkedList, Amazon, Microsoft, Bloomberg, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-23 11:38:39
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

## Example
![](https://discuss.leetcode.com/uploads/files/1470150906153-2yxeznm.png)
```
Input:
{"$id":"1","next":{"$id":"2","next":null,"random":{"$ref":"2"},"val":2},"random":{"$ref":"2"},"val":1}

Explanation:
Node 1's value is 1, both of its next and random pointer points to Node 2.
Node 2's value is 2, its next pointer points to null and its random pointer points to itself.
```

## Solution
**Solution 1: O(1) space**
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;
    public Node random;

    public Node() {}

    public Node(int _val,Node _next,Node _random) {
        val = _val;
        next = _next;
        random = _random;
    }
};
*/
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) return null;
        // loop 1: copy all nodes
        Node cur = head;
        while(cur != null){
            Node next = cur.next;
            cur.next = new Node(cur.val, next, null);
            cur = next;
        }

        // loop 2: assign all random pointers
        cur = head;
        while(cur != null){
            if (cur.random != null){
                cur.next.random = cur.random.next;
            }
            cur = cur.next.next;
        }

        // loop 3: reconstrcut new list
        cur = head;
        Node newHead = cur.next;
        while(cur != null){
            Node next = cur.next.next;
            Node copy = cur.next;
            cur.next = next;
            if (next != null)
                copy.next = next.next;
            cur = next;
        }
        return newHead;
    }
}
```
**Solution 2: HashMap, O(N) space**
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;
    public Node random;

    public Node() {}

    public Node(int _val,Node _next,Node _random) {
        val = _val;
        next = _next;
        random = _random;
    }
};
*/
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) return null;
  
        Map<Node, Node> map = new HashMap<>();
  
        // loop 1. copy all the nodes
        Node node = head;
        while (node != null) {
            map.put(node, new Node(node.val, null, null));
            node = node.next;
        }
  
        // loop 2. assign next and random pointers
        node = head;
        while (node != null) {
            map.get(node).next = map.get(node.next);
            map.get(node).random = map.get(node.random);
            node = node.next;
        }
  
        return map.get(head);
    }
}
```

<hr />