---
title: Leetcode652-findDuplicateSubtrees
categories: leetcode
tags: [Tree, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 15:54:39
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree, return all duplicate subtrees. For each kind of duplicate subtrees, you only need to return the root node of any one of them.

Two trees are duplicate if they have the same structure with same node values.

## Example
```
        1
       / \
      2   3
     /   / \
    4   2   4
       /
      4
```
The following are two duplicate subtrees:
```
      2
     /
    4
```
and
```
    4
```

Therefore, you need to return above trees' root in the form of a list.

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
    public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
        HashMap<String, Integer> map = new HashMap<>();
        List<TreeNode> res = new ArrayList<TreeNode>();
        helper(root, map, res);
        return res;
    }
    
    private String helper(TreeNode node, HashMap<String, Integer> map, List<TreeNode> res){
        if (node == null) return "#";
        String cur = node.val + "-" + helper(node.left, map, res) + "-" + helper(node.right, map, res);
        if (map.getOrDefault(cur, 0) == 1) res.add(node);
        map.put(cur, map.getOrDefault(cur, 0) + 1);
        return cur;
    }
}
```

<hr />