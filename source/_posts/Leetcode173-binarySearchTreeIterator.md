---
title: Leetcode173-binarySearchTreeIterator
categories: leetcode
tags: [Stack, Design, Tree, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 21:11:34
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling next() will return the next smallest number in the BST.

## Example
!()[https://assets.leetcode.com/uploads/2018/12/25/bst-tree.png]
```
BSTIterator iterator = new BSTIterator(root);
iterator.next();    // return 3
iterator.next();    // return 7
iterator.hasNext(); // return true
iterator.next();    // return 9
iterator.hasNext(); // return true
iterator.next();    // return 15
iterator.hasNext(); // return true
iterator.next();    // return 20
iterator.hasNext(); // return false
```
**Note:**

* next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.
* You may assume that next() call will always be valid, that is, there will be at least a next smallest number in the BST when next() is called.

## Solution
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

class BSTIterator {
    
    private Stack<TreeNode> st;
    public BSTIterator(TreeNode root) {
        st = new Stack<>();
        pushAll(root);
    }
    
    /** @return the next smallest number */
    public int next() {
        TreeNode res = st.pop();
        pushAll(res.right);
        return res.val;
    }
    
    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !st.isEmpty();
    }
    
    private void pushAll(TreeNode node){
        while (node != null){
            st.push(node);
            node = node.left;
        }
    }
}
```

<hr />