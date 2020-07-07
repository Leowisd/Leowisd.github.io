---
title: Leetcode110-balancedBianryTree
categories: leetcode
tags: [Tree, DFS, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-11-16 23:42:46
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

## Example
**Example 1**:
```
Given the following tree [3,9,20,null,null,15,7]:

    3
   / \
  9  20
    /  \
   15   7
```
Return true.

**Example 2**:
```
Given the following tree [1,2,2,3,3,null,null,4,4]:

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```
Return false.

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
    // traver tree
    // public boolean isBalanced(TreeNode root) {
    //     if (root == null) return true;
    //     int left = height(root.left);
    //     int right = height(root.right);
    //     if (Math.abs(left - right) > 1) return false;
    //     return isBalanced(root.left) && isBalanced(root.right);      
    // }
    // private int height(TreeNode node){
    //     if (node == null) return 0;
    //     int left = height(node.left);
    //     int right = height(node.right);
    //     return Math.max(left, right) + 1;
    // }
    // Based on DFS     
    public boolean isBalanced(TreeNode root){
        if (root == null) return true;
        return dfs(root) != -1;
    }
    private int dfs(TreeNode node){
        if (node == null) return 0;
        int left = dfs(node.left);
        if (left == -1) return -1;
        int right = dfs(node.right);
        if (right == -1) return -1;
        if (Math.abs(left - right) > 1) return -1;
        return Math.max(left, right) + 1;
    }
}
```

<hr />