---
title: Leetcode111-minimumDepthOfBinaryTree
categories: leetcode
tags: [Tree, DFS]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-10 21:38:53
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

## Example
Given binary tree [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
return its minimum depth = 2.

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
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        return helper(root, 1);
    }
    private int helper(TreeNode node, int depth){
        if (node.left == null && node.right == null) return depth;
        if (node.left != null && node.right != null) 
            return Math.min(helper(node.left, depth + 1), helper(node.right, depth + 1));
        else if (node.left == null)
            return helper(node.right, depth + 1);
        else return helper(node.left, depth + 1);
    }
}
```

<hr />