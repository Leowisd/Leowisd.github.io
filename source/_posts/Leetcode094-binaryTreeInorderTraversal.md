---
title: Leetcode094-binaryTreeInorderTraversal
categories: leetcode
tags: [Tree, Inorder]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-14 23:17:33
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a binary tree, return the inorder traversal of its nodes' values.

## Example
```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```
**Follow up:** Recursive solution is trivial, could you do it iteratively?

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
    
    public void inOrder(TreeNode node){
        
        if (node.left != null) inOrder(node.left);
        res.add(node.val);
        if (node.right != null) inOrder(node.right);
    }
    public List<Integer> inorderTraversal(TreeNode root) {
        if (root == null) return res;
        
        //Recursive solution
        //inOrder(root);
        
        //Stack method
        // Stack<TreeNode> st = new Stack<>();
        // if (root.right!=null){
        //     st.push(root.right);
        //     root.right = null;
        // }
        // st.push(root);
        // if (root.left!=null){
        //     st.push(root.left);
        //     root.left=null;
        // }
        // while(!st.empty()){
        //     TreeNode node = st.pop();
        //     if (node.right != null){
        //         st.push(node.right);
        //         node.right = null;
        //     }
        //     if (node.left != null){
        //         st.push(node);
        //         st.push(node.left);
        //         node.left = null;
        //     }
        //     else res.add(node.val);
        // }
        
        // return res;

        //iterative method
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode p = root;
        while(!stack.isEmpty() || p != null) {
            if(p != null) {
                stack.push(p);
                p = p.left;
            } else {
                TreeNode node = stack.pop();
                result.add(node.val);  // Add after all left children
                p = node.right;   
            }
        }
        return result;
    }
}
```

<hr />