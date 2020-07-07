---
title: Leetcode285-inorderSuccessorInBST
categories: leetcode
tags: [Tree, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-29 23:44:30
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

The successor of a node p is the node with the smallest key greater than p.val.

## Example
**Example 1:**
![](https://assets.leetcode.com/uploads/2019/01/23/285_example_1.PNG)
```
Input: root = [2,1,3], p = 1
Output: 2
Explanation: 1's in-order successor node is 2. Note that both p and the return value is of TreeNode type.
```
**Example 2:**
![](https://assets.leetcode.com/uploads/2019/01/23/285_example_2.PNG)
```
Input: root = [5,3,6,2,4,null,null,1], p = 6
Output: null
Explanation: There is no in-order successor of the current node, so the answer is null.
```
**Note:**

1. If the given node has no in-order successor in the tree, return null.
2. It's guaranteed that the values of the tree are unique.

## Solution

**Solution 1:** Basical Solution, O(h);
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
    // Solution 1: basic one, O(h)
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null) return null;
        TreeNode res = null;
        
        if (p.right != null){
            p = p.right;
            while(p.left != null){
                p = p.left;
            }
            return p;
        }
        
        while(root != p){
            root = (p.val > root.val) ? root.right : (res = root).left;
        }
        return res;
        
    }
}
```
**Solution 2:** Improved solution, O(h)
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
// Solution 2: more improved, O(h)
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode res = null;
        while(root != null){
            root = (root.val > p.val) ? (res = root).left : root.right;
        }
        return res;
    }
}
```

<hr />