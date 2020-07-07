---
title: Leetcode144-binaryTreePreorderTraversal
categories: leetcode
tags: [Tree, Preorder]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-13 23:53:57
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree, return the preorder traversal of its nodes' values.

## Example
```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,2,3]
```
**Follow up**: Recursive solution is trivial, could you do it iteratively?

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
    List<Integer> res = new ArrayList<>();
    
    public void preOrder(TreeNode node){
        res.add(node.val);
        if (node.left != null) preOrder(node.left);
        if (node.right != null) preOrder(node.right);
        return;
    }
    
    public List<Integer> preorderTraversal(TreeNode root){
        if (root == null) return res;
        //Recursive solution
        //preOrder(root);
        
        //Stack method
        // Stack<TreeNode> toDo = new Stack<>();
        // toDo.push(root);
        // while(!toDo.empty()){
        //     TreeNode node = toDo.pop();
        //     res.add(node.val);
        //     if (node.right != null) toDo.push(node.right);
        //     if (node.left != null) toDo.push(node.left);
        // }
        // return res;
        
        //iterative method
        List<Integer> result = new ArrayList<>();
        Deque<TreeNode> stack = new ArrayDeque<>();
        TreeNode p = root;
        while(!stack.isEmpty() || p != null) {
            if(p != null) {
                stack.push(p);
                result.add(p.val);  // Add before going to children
                p = p.left;
            } else {
                TreeNode node = stack.pop();
                p = node.right;   
            }
        }
        return result;
    }
}
```

<hr />