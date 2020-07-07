---
title: Leetcode708-insertIntoASortedCircularLinkedList
categories: leetcode
tags: [Linked List, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 14:50:44
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a node from a Circular Linked List which is sorted in ascending order, write a function to insert a value insertVal into the list such that it remains a sorted circular list. The given node can be a reference to any single node in the list, and may not be necessarily the smallest value in the circular list.

If there are multiple suitable places for insertion, you may choose any place to insert the new value. After the insertion, the circular list should remain sorted.

If the list is empty (i.e., given node is null), you should create a new single circular list and return the reference to that single node. Otherwise, you should return the original given node.

## Example
**Example 1:**


![](https://assets.leetcode.com/uploads/2019/01/19/example_1_before_65p.jpg)

```
Input: head = [3,4,1], insertVal = 2
Output: [3,4,1,2]
Explanation: In the figure above, there is a sorted circular list of three elements. You are given a reference to the node with value 3, and we need to insert 2 into the list. The new node should be inserted between node 1 and node 3. After the insertion, the list should look like this, and we should still return node 3.
```

![](https://assets.leetcode.com/uploads/2019/01/19/example_1_after_65p.jpg)

**Example 2:**
```
Input: head = [], insertVal = 1
Output: [1]
Explanation: The list is empty (given head is null). We create a new single circular list and return the reference to that single node.
```
**Example 3:**
```
Input: head = [1], insertVal = 0
Output: [1,0]
```

**Constraints:**

* 0 <= Number of Nodes <= 5 * 10^4
* -10^6 <= Node.val <= 10^6
* -10^6 <= insertVal <= 10^6

## Solution
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _next) {
        val = _val;
        next = _next;
    }
};
*/
class Solution {
    public Node insert(Node head, int insertVal) {
// Case A: Empty
        if (head == null){
            Node temp = new Node(insertVal);
            temp.next = temp;
            return temp;
        }
// Case B: Not Empty
        Node cur = head;
        while (true){
            if (cur.val < cur.next.val){
// Case B1: there are two distinct nodes, still climbing
                if (insertVal >= cur.val && insertVal <= cur.next.val){
                    cur.next = new Node(insertVal, cur.next);
                    break;
                }
            }
            else if (cur.val > cur.next.val){
// Case B2: there are two distinct nodes, back to the minmum node
                if (insertVal >= cur.val || insertVal <= cur.next.val){
                    cur.next = new Node(insertVal, cur.next);
                    break;
                }
            }
            else if (cur.next == head){
// Case B3: all nodes in the list are the same
                cur.next = new Node(insertVal, cur.next);
                break;
            }
            cur = cur.next;
        }
        return head;
    }
}
```

<hr />