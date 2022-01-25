---
title: Leetcode671-Second Minimum Node In a BinaryTree
categories: leetcode
tags: [Tree, Linkedln, DFS]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2022-01-24 15:07:05
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a non-empty special binary tree consisting of nodes with the non-negative value, where each node in this tree has exactly two or zero sub-node. If the node has two sub-nodes, then this node's value is the smaller value among its two sub-nodes. More formally, the property root.val = min(root.left.val, root.right.val) always holds.

Given such a binary tree, you need to output the second minimum value in the set made of all the nodes' value in the whole tree.

If no such second minimum value exists, output -1 instead.

## Example
**Example 1**
![](https://assets.leetcode.com/uploads/2020/10/15/smbt1.jpg)

```
Input: root = [2,2,5,null,null,5,7]
Output: 5
Explanation: The smallest value is 2, the second smallest value is 5.
```

**Example 2**
![](https://assets.leetcode.com/uploads/2020/10/15/smbt2.jpg)
```
Input: root = [2,2,2]
Output: -1
Explanation: The smallest value is 2, but there isn't any second smallest value.
```

**Constraints:**

* The number of nodes in the tree is in the range [1, 25].
* 1 <= Node.val <= 231 - 1
* root.val == min(root.left.val, root.right.val) for each internal node of the tree.

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

In this tree, the root should be the smallest node.

If the value of the children of the root node is not same, root val should be the smaller child value, but the larger one may not the second smallest one, cause the second smallest one may also in the subtree of the smaller value node.

Similar, if the two children value are the same, then calculate the second smallest value of each subtree, then compare them to find the smaller one as the second smallest value.

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
    public int findSecondMinimumValue(TreeNode root) {
        if (root == null || root.left == null || root.right == null){
            return -1;
        }
        int left = root.left.val;
        int right = root.right.val;
        if (root.val ==  left){
            left = findSecondMinimumValue(root.left);
        }
        if (root.val == right){
            right = findSecondMinimumValue(root.right);
        }
        if (left == -1){
            return right;
        }
        if (right == -1){
            return left;
        }
        return Math.min(left, right);
    }
}
```

<hr />