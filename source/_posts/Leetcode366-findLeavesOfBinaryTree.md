---
title: Leetcode366-findLeavesOfBinaryTree
categories: leetcode
tags: [Tree, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-15 00:44:23
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree, collect a tree's nodes as if you were doing this: Collect and remove all leaves, repeat until the tree is empty.

## Example
```
Input: [1,2,3,4,5]
  
          1
         / \
        2   3
       / \     
      4   5    

Output: [[4,5,3],[2],[1]]
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
    public List<List<Integer>> findLeaves(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        
        traversal(root, res);
        
        return res;
    }
    
    private int traversal(TreeNode node, List<List<Integer>> res){
        if (node == null) return -1;
        int level = Math.max(traversal(node.left, res), traversal(node.right, res)) + 1;
        if (level >= res.size()) res.add(new ArrayList<Integer>());
        res.get(level).add(node.val);
        return level;
    }
}
```

<hr />