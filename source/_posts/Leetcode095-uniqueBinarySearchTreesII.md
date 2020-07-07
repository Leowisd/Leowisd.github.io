---
title: Leetcode095-uniqueBinarySearchTreesII
categories: leetcode
tags: [Tree, Recursion, DP]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-22 23:23:35
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1 ... n.

## Example
```
Input: 3
Output:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
Explanation:
The above output corresponds to the 5 unique BST's shown below:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

## Solution

Method 1: Basic recursion method 
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
    public List<TreeNode> generateTrees(int n) {
        if (n == 0) return new ArrayList<TreeNode>();
        return helper(1, n);
    }
    
    public List<TreeNode> helper(int left, int right){
        List<TreeNode> res = new ArrayList<>();

        if (left > right) {
            res.add(null);
            return res;
        }
        
        for (int i = left; i <= right; i++){
            List<TreeNode> leftTree = helper(left, i - 1);
            List<TreeNode> rightTree = helper(i + 1, right);
            
            for (TreeNode leftNode: leftTree){
                for (TreeNode rightNode: rightTree){
                    TreeNode newNode = new TreeNode(i);
                    newNode.left = leftNode;
                    newNode.right = rightNode;
                    res.add(newNode);
                }
            }
        }

        return res;
    }
}
```

Method2: Recursion with momory, a kind of DP. Used memory[i][j][] to store BSTs constructed by i..j. In this method, used list which need to be initilized to store. The time for initialization if O^2, it's not good. Maybe can change to Array to store. 
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
    public List<TreeNode> generateTrees(int n) {
        if (n == 0) return new ArrayList<TreeNode>();
        List<List<List<TreeNode>>> memory = new ArrayList<>();
        for (int i = 0; i < n; i++){
            memory.add(new ArrayList<>());
            for (int j = 0; j < n; j++) memory.get(i).add(new ArrayList<TreeNode>());
        }
        return helper(1, n, memory);
    }
    
    public List<TreeNode> helper(int left, int right, List<List<List<TreeNode>>> memory){
        List<TreeNode> res = new ArrayList<>();

        if (left > right) {
            res.add(null);
            return res;
        }
        if (memory.get(left - 1).get(right - 1).size() != 0) return memory.get(left - 1).get(right - 1);
        for (int i = left; i <= right; i++){
            List<TreeNode> leftTree = helper(left, i - 1, memory);
            List<TreeNode> rightTree = helper(i + 1, right, memory);
            
            for (TreeNode leftNode: leftTree){
                for (TreeNode rightNode: rightTree){
                    TreeNode newNode = new TreeNode(i);
                    newNode.left = leftNode;
                    newNode.right = rightNode;
                    res.add(newNode);
                }
            }
        }
        List<TreeNode> temp = memory.get(left - 1).get(right - 1);
        temp = res;
        return res;
    }
}
```

<hr />