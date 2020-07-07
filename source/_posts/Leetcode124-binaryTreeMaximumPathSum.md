---
title: Leetcode124-binaryTreeMaximumPathSum
categories: leetcode
tags: [Tree, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-07 10:26:18
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

## Example
**Example 1:**
```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```
**Example 2:**
```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```
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
    private int res = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root){
        if (root == null) return 0;
        travelsal(root);
        return res;
    }
    
    public int travelsal(TreeNode node){
        if (node == null) return 0;
        
        int left = Math.max(travelsal(node.left), 0);
        int right = Math.max(travelsal(node.right), 0);
        res = Math.max(res, left + right + node.val);
        return Math.max(left, right) + node.val;
    }
}
```

<hr />