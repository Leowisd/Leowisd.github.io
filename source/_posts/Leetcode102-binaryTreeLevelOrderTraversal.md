---
title: Leetcode102-binaryTreeLevelOrderTraversal
categories: leetcode
tags: [Tree, Preorder, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-15 00:13:34
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

## Example
```
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
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
    List<List<Integer>> res = new ArrayList<>();
    
    public void traversal(TreeNode node, int level){
        if (res.size() <= level) res.add(new ArrayList<>());
        res.get(level).add(node.val);
        if (node.left != null) traversal(node.left, level + 1);
        if (node.right != null) traversal(node.right, level + 1);
    }
    public List<List<Integer>> levelOrder(TreeNode root) {
        if (root == null) return res;
        traversal(root, 0);
        return res;
    }
}
```

<hr />