---
title: Leetcode114-flattenBinaryTreeToLinkedList
categories: leetcode
tags: [DFS, Tree, Stack, Bloomberg, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-10 21:41:56
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a binary tree, flatten it to a linked list in-place.

For example, given the following tree:
```
    1
   / \
  2   5
 / \   \
3   4   6
```
The flattened tree should look like:
```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

## Solution

**Solution 1:** 
Just Post traversal, the best
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
    private TreeNode pre = null; 
    public void flatten(TreeNode root) {
        if (root == null) return;
        flatten(root.right);
        flatten(root.left);
        root.right = pre;
        root.left = null;
        pre = root;
    }
}
```

**Solution 2:**
Used stack, the idea could be used in other problems.
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
    public void flatten(TreeNode root) {
        Stack<TreeNode> st = new Stack<>();
        while (root != null || !st.isEmpty()){
            if (root.right != null) st.push(root.right);
            if (root.left != null){
                root.right = root.left;
                root.left = null;
            }
            else if (!st.isEmpty()){
                root.right = st.pop();
            }
            root = root.right;
        }
    }
}
```

<hr />