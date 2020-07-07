---
title: Leetcode105-constructBinaryTreeFromPreorderAndInorderTraversal
categories: leetcode
tags: [Tree, DFS, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-08 23:40:22
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**
You may assume that duplicates do not exist in the tree.

For example, given
```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```

Return the following binary tree:
```
    3
   / \
  9  20
    /  \
   15   7
```
## Example


## Solution

Basic solution, but could be faster
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return helper(0, 0, inorder.length - 1, preorder, inorder);
    }
    private TreeNode helper(int prestart, int instart, int inend, int[] preorder, int[] inorder){
        if (prestart > preorder.length - 1 || instart > inend)
            return null;
        TreeNode root = new TreeNode(preorder[prestart]);
        int index = 0;
        for (int i = instart; i <= inend; i++){
            if (inorder[i] == root.val){
                index = i;
                break;
            }
        }
        root.left = helper(prestart + 1, instart, index - 1, preorder, inorder);
        root.right = helper(prestart + index - instart + 1, index + 1, inend, preorder, inorder);
        return root;
    }
}
```

Used HasMap, faster
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < inorder.length; i++)
            map.put(inorder[i], i);
        return helper(0, preorder.length - 1, 0, inorder.length-1, preorder, inorder, map);
    }
    private TreeNode helper(int prestart, int preend, int instart, int inend, int[] preorder, int[] inorder, HashMap<Integer, Integer> map){
        if (prestart > preend || instart > inend)
            return null;
        TreeNode root = new TreeNode(preorder[prestart]);
        int index = map.get(root.val);
        root.left = helper(prestart + 1, prestart + index - instart, instart, index - 1, preorder, inorder, map);
        root.right = helper(prestart + index - instart + 1, preend, index + 1, inend, preorder, inorder, map);
        return root;
    }
}
```

<hr />