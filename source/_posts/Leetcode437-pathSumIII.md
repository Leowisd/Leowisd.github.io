---
title: Leetcode437-pathSumIII
categories: leetcode
tags: [Tree, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-28 15:40:26
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

## Example
```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
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
    private int res = 0;
    public int pathSum(TreeNode root, int sum) {
        if (root == null) return 0;
        HashMap<Integer, Integer> presum = new HashMap<>();
        presum.put(0, 1);
        helper(presum, root, 0, sum);
        return res;
    }
    private void helper(HashMap<Integer, Integer> presum, TreeNode node, int cur, int target){
        if (node == null) return;
        cur = cur + node.val;
        if (presum.getOrDefault(cur - target, 0) > 0){
            res += presum.get(cur - target);
        }
        
        presum.put(cur, presum.getOrDefault(cur, 0) + 1);
        helper(presum, node.left, cur, target);
        helper(presum, node.right, cur, target);
        presum.put(cur, presum.get(cur) - 1);
    }
}
```

<hr />