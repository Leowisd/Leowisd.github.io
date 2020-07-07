---
title: Leetcode145-binaryTreePosterTraversal
categories: leetcode
tags: [Tree, Posteroder]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-14 23:51:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a binary tree, return the postorder traversal of its nodes' values.

## Example
```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [3,2,1]
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
    
    public void postOrder(TreeNode node){
        if (node.left != null) postOrder(node.left);
        if (node.right != null) postOrder(node.right);
        res.add(node.val);
    }
    public List<Integer> postorderTraversal(TreeNode root) {
        if (root == null) return res;
        
        //Recursive solution
        //postOrder(root);
        
        //Iterative solution
        // Stack<TreeNode> st = new Stack<>();
        // st.push(root);
        // if (root.right != null){
        //     st.push(root.right);
        //     root.right = null;
        // }
        // if (root.left != null){
        //     st.push(root.left);
        //     root.left = null;
        // }
        // while (!st.empty()){
        //     TreeNode node = st.pop();
        //     if (node.left == null && node.right == null)
        //         res.add(node.val);
        //     else{
        //         st.push(node);
        //         if (node.right != null){
        //             st.push(node.right);
        //             node.right = null;
        //         }
        //         if (node.left != null){
        //             st.push(node.left);
        //             node.left = null;
        //         }
        //     }
        // }
        
        // return res;
        
        LinkedList<Integer> result = new LinkedList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode p = root;
        while(!stack.isEmpty() || p != null) {
            if(p != null) {
                stack.push(p);
                result.addFirst(p.val);  // Reverse the process of preorder
                p = p.right;             // Reverse the process of preorder
            } else {
                TreeNode node = stack.pop();
                p = node.left;           // Reverse the process of preorder
            }
        }
        return result;
    }
}
```

<hr />