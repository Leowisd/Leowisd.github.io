---
title: Leetcode113-pathSumII
categories: leetcode
tags: [Tree, DFS]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-10 21:49:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

**Note:** A leaf is a node with no children.

## Example
Given the below binary tree and sum = 22,
```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
```
Return:
```
[
   [5,4,11,2],
   [5,8,4,5]
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
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        helper(root, sum, res, new ArrayList<Integer>(), 0);
        return res;
    }
    
    private void helper(TreeNode node, int target, List<List<Integer>> res, List<Integer> cur, int sum){
        cur.add(node.val);
        sum += node.val;
        if (node.left == null && node.right == null && sum == target){
            res.add(new ArrayList<>(cur));
            return;
        }
        // System.out.println(cur + ", " + sum);
        if (node.left != null){
            helper(node.left, target, res, cur, sum);
            cur.remove(cur.size()-1);
        }
        if (node.right != null){
            helper(node.right, target, res, cur, sum);
            cur.remove(cur.size()-1);
        }
    }
}
```

<hr />