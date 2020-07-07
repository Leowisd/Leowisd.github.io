---
title: Leetcode103-binaryTreeZigZagLevelOrderTraversal
categories: leetcode
tags: [Tree, Amazon, Microsoft, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-06 18:05:56
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).
## Example
```
For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its zigzag level order traversal as:
[
  [3],
  [20,9],
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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        
        traversal(root, res, 0);
        
        return res;
    }
    public void traversal(TreeNode node, List<List<Integer>> res, int level){
        if (res.size() <= level) res.add(new ArrayList<>());
        
        if (level % 2 == 0) res.get(level).add(node.val);
        else res.get(level).add(0, node.val);
        
        if (node.left != null) traversal(node.left, res, level+1);
        if (node.right != null) traversal(node.right, res, level+1);
    }
}
```

<hr />