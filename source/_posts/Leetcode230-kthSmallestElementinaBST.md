---
title: Leetcode230-kthSmallestElementinaBST
categories: leetcode
tags: [Tree, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-13 16:41:30
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

**Note:**
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

## Example
**Example 1:**
```
Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
```
**Example 2:**
```
Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
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
    private int count;
    private int res;
    public int kthSmallest(TreeNode root, int k) {
        count = k;
        inOrder(root);
        return res;
    }
    
    private void inOrder(TreeNode node){
        if (node.left != null) inOrder(node.left);
        count--;
        if (count == 0){
            res = node.val;
            return;
        }
        if (node.right != null) inOrder(node.right);
    }
}
```

<hr />