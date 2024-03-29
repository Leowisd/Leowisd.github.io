---
title: Leetcode993-cousinsInBinaryTree
categories: leetcode
tags: [Tree, BFS, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-12 21:43:23
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

In a binary tree, the root node is at depth 0, and children of each depth k node are at depth k+1.

Two nodes of a binary tree are cousins if they have the same depth, but have different parents.

We are given the root of a binary tree with unique values, and the values x and y of two different nodes in the tree.

Return true if and only if the nodes corresponding to the values x and y are cousins.

## Example
**Example 1:**
```
Input: root = [1,2,3,4], x = 4, y = 3
Output: false
```
**Example 2:**
```
Input: root = [1,2,3,null,4,null,5], x = 5, y = 4
Output: true
```
**Example 3:**
```
Input: root = [1,2,3,null,4], x = 2, y = 3
Output: false
```

**Note:**

1. The number of nodes in the tree will be between 2 and 100.
2. Each node has a unique integer value from 1 to 100.

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
    public boolean isCousins(TreeNode root, int x, int y) {
        if (root == null) return false;
        Queue<TreeNode> queue = new LinkedList<>();
        boolean isXexist;
        boolean isYexist;
        queue.offer(root);
        while (!queue.isEmpty()){
            isXexist = false;
            isYexist = false;
            int size = queue.size();
            for (int i = 0; i < size; i++){
                TreeNode node = queue.poll();
                if (node.val == x) isXexist = true;
                if (node.val == y) isYexist = true;
                if (node.left != null && node.right != null){
                    if (node.left.val == x && node.right.val == y) return false;
                    if (node.left.val == y && node.right.val == x) return false;
                }
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            if (isXexist && isYexist) return true;
        }
        return false;
    }
}
```

<hr />