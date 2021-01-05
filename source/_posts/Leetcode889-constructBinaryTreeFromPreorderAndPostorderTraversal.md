---
title: Leetcode889-Construct Binary Tree From Preorder And Postorder Traversal
categories: leetcode
tags: [Tree, Recursion, Iteration]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-12-30 01:05:32
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Return any binary tree that matches the given preorder and postorder traversals.

Values in the traversals pre and post are distinct positive integers.

## Example
```
Input: pre = [1,2,4,5,3,6,7], post = [4,5,2,6,7,3,1]
Output: [1,2,3,4,5,6,7]
```

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(height)$$

### Recursion 

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    private int i = 0;
    private int j = 0;
    public TreeNode constructFromPrePost(int[] pre, int[] post) {
        TreeNode root = new TreeNode(pre[i++]);
        if (root.val != post[j]){
            root.left = constructFromPrePost(pre, post);
        }
        if (root.val != post[j]){
            root.right = constructFromPrePost(pre, post);
        }
        j++;
        return root;
    }   
}
```

### Iteration
```java
    public TreeNode constructFromPrePost(int[] pre, int[] post) {
        Deque<TreeNode> s = new ArrayDeque<>();
        s.offer(new TreeNode(pre[0]));
        for (int i = 1, j = 0; i < pre.length; ++i) {
            TreeNode node = new TreeNode(pre[i]);
            while (s.getLast().val == post[j]) {
                s.pollLast(); j++;
            }
            if (s.getLast().left == null) s.getLast().left = node;
            else s.getLast().right = node;
            s.offer(node);
        }
        return s.getFirst();
    }
```

<hr />