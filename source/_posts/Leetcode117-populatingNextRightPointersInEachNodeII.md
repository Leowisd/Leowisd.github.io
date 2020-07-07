---
title: Leetcode117-populatingNextRightPointersInEachNodeII
categories: leetcode
tags: [Tree, Iteration, Two Pointers, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 11:21:23
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a binary tree
```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

**Follow up:**

* You may only use constant extra space.
* Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.

## Example
![](https://assets.leetcode.com/uploads/2019/02/15/117_sample.png)
```
Input: root = [1,2,3,4,5,null,7]
Output: [1,#,2,3,#,4,5,7,#]
Explanation: Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

**Constraints:**

* The number of nodes in the given tree is less than 6000.
* -100 <= node.val <= 100

## Solution

Used three pointers. One to record each level's head, one to record the prev node in one level, one to traversal nodes in one level.

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/
class Solution {
    public Node connect(Node root) {
        if (root == null) return root;
        
        Node head = null;
        Node pre = null;
        Node cur = root;
        
        while(cur != null){
            
            while(cur != null){
                if (cur.left != null){
                    if (pre != null)
                        pre.next = cur.left;
                    else
                        head = cur.left;
                    pre = cur.left;
                }
                if (cur.right != null){
                    if (pre != null)
                        pre.next = cur.right;
                    else 
                        head = cur.right;
                    pre = cur.right;
                }
                cur = cur.next;
            }
            
            cur = head;
            pre = null;
            head = null;
        }
        
        return root;
    }
}
```

<hr />