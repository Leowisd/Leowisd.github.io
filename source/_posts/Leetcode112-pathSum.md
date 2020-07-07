---
title: Leetcode112-pathSum
categories: leetcode
tags: [Tree, DFS]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-01-27 23:51:18
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

Note: A leaf is a node with no children.

## Example

Given the below binary tree and sum = 22,
```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.


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
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) return false;
        return dfs(root, sum, 0);
    }
    private boolean dfs(TreeNode node, int sum, int cur){
        if (node == null) return false;
        cur += node.val;
        if (node.left == null && node.right == null){
            if (cur == sum) return true;
            return false;
        }
        return dfs(node.left, sum, cur) || dfs(node.right, sum, cur);
    }
}
```

<hr />