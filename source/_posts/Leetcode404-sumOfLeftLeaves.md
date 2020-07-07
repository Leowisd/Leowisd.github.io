---
title: Leetcode404-sumOfLeftLeaves
categories: leetcode
tags: [Tree, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-10 18:56:56
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Find the sum of all left leaves in a given binary tree.

## Example
```
    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
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
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) return 0;
        int res = 0;
        if (root.left != null){
            if (root.left.left == null && root.left.right == null) res += root.left.val;
            else res += sumOfLeftLeaves(root.left);
        }
        res += sumOfLeftLeaves(root.right);
        return res;
    }
}
```

<hr />