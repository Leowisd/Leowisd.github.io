---
title: Leetcode543-diameterOfBinaryTree
categories: leetcode
tags: [Tree, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 22:44:39
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

## Example
Given a binary tree
```
          1
         / \
        2   3
       / \     
      4   5    
```
Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

**Note:** The length of path between two nodes is represented by the number of edges between them.

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
class Solution {
    private int res = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        if (root == null) return 0;
        
        helper(root);
        
        return res;
    }
    
    private int helper(TreeNode root){
        if (root == null) return -1;
        if (root.left == null && root.right == null) return 0;
        int left = helper(root.left) + 1;
        int right = helper(root.right) + 1;
        res = Math.max(res, left + right);
        return Math.max(left, right);
    }
}
```

<hr />