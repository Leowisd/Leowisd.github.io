---
title: Leetcode100-Same Tree
categories: leetcode
tags: [Tree, Amazon, Bloomberg, Linkedin]
description: Solution Report of LeetCode Accepted
mathjax: true
date: 2019-10-13 09:54:05
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

## Example
**Example 1:**
```
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
```
**Example 2:**
```
Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
```
**Example 3:**
```
Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false
```

## Solution

**Solution 1: Recursion**

Time Complex: $$O(N)$$

Space Complex: $$O(logN)$$

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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        if (p.val != q.val) return false;
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```

**Solution 2: Iteration**

Time Complex: $$O(N)$$

Space Complex: $$O(logN)$$

```java
// Iteration solution, use stack to preorder trees
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        Stack<TreeNode> stP = new Stack<>();
        Stack<TreeNode> stQ = new Stack<>();
        if (p != null){
            stP.push(p);
        }
        if (q != null){
            stQ.push(q);
        }
        
        while(!stP.isEmpty() && !stQ.isEmpty()){
            TreeNode nodeP = stP.pop();
            TreeNode nodeQ = stQ.pop();
            if (nodeP.val != nodeQ.val){
                return false;
            }
            if (nodeP.left != null){
                stP.push(nodeP.left);
            }
            if (nodeQ.left != null){
                stQ.push(nodeQ.left);
            }
            if (stP.size() != stQ.size()){
                return false;
            }
            if (nodeP.right != null){
                stP.push(nodeP.right);
            }
            if (nodeQ.right != null){
                stQ.push(nodeQ.right);
            }
            if (stP.size() != stQ.size()){
                return false;
            }            
        }
        return stP.size() == 0 && stQ.size() == 0;
    }
}
```

<hr />