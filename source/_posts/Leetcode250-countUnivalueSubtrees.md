---
title: Leetcode250-countUnivalueSubtrees
categories: leetcode
tags: [Tree, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 16:37:12
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree, count the number of uni-value subtrees.

A Uni-value subtree means all nodes of the subtree have the same value.

## Example
```
Input:  root = [5,1,5,5,5,null,5]

              5
             / \
            1   5
           / \   \
          5   5   5

Output: 4
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
    int res = 0;
    public int countUnivalSubtrees(TreeNode root) {
        if (root == null) return 0;
        
        helper(root);
        return res;
    }
    
    private boolean helper(TreeNode root){
        if (root == null) return true;
        if (root.left == null && root.right == null){
            res++;
            return true;
        }        
        boolean left = helper(root.left);
        boolean right = helper(root.right);
        if (!left || !right) return false;
        if (root.left == null){
            if (root.val == root.right.val){
                res++;
                return true;
            }
        }
        else if (root.right == null){
            if (root.val == root.left.val){
                res++;
                return true;
            }
        }
        else{
            if (root.val == root.left.val && root.val == root.right.val){
                res++;
                return true;
            }
        }
        return false;
    }
}
```

<hr />