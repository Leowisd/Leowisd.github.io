---
title: Leetcode222-countCompleteTreeNodes
categories: leetcode
tags: [Tree, Binary Search, Google, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-11-05 10:29:49
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a complete binary tree, count the number of nodes.

**Note:**

Definition of a complete binary tree from Wikipedia:
In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

## Example
```
Input: 
    1
   / \
  2   3
 / \  /
4  5 6

Output: 6
```

## Solution
Method 1: O(n)
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
    public int countNodes(TreeNode root) {
        if (root == null) return 0;       
        return countNodes(root.left) + countNodes(root.right) + 1;
    }   
}
```

Method 2: $O(log^2(n))$
```java
class Solution{
    public int countNodes(TreeNode root) {
        int left = leftHeight(root);
        int right = rightHeight(root);
        
        if (left == right)
            return (1 << left) - 1;
        else return countNodes(root.left) + countNodes(root.right) + 1;
    }
    private int leftHeight(TreeNode node){
        int dep = 0;
        while(node != null){
            node = node.left;
            dep++;
        }
        return dep;
    }
    private int rightHeight(TreeNode node){
        int dep = 0;
        while(node != null){
            node = node.right;
            dep++;
        }
        return dep;
    }
}
```
<hr />