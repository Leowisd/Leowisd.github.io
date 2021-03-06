---
title: Leetcode987-verticalOrderTraversalOfABinaryTree
categories: leetcode
tags: [Hash Map, Tree, Bloomberg, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 15:28:30
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a binary tree, return the vertical order traversal of its nodes values.

For each node at position (X, Y), its left and right children respectively will be at positions (X-1, Y-1) and (X+1, Y-1).

Running a vertical line from X = -infinity to X = +infinity, whenever the vertical line touches some nodes, we report the values of the nodes in order from top to bottom (decreasing Y coordinates).

If two nodes have the same position, then the value of the node that is reported first is the value that is smaller.

Return an list of non-empty reports in order of X coordinate.  Every report will have a list of values of nodes.

## Example
**Example 1:**

![](https://assets.leetcode.com/uploads/2019/01/31/1236_example_1.PNG)

```
Input: [3,9,20,null,null,15,7]
Output: [[9],[3,15],[20],[7]]
Explanation: 
Without loss of generality, we can assume the root node is at position (0, 0):
Then, the node with value 9 occurs at position (-1, -1);
The nodes with values 3 and 15 occur at positions (0, 0) and (0, -2);
The node with value 20 occurs at position (1, -1);
The node with value 7 occurs at position (2, -2).
```
**Example 2:**

![](https://assets.leetcode.com/uploads/2019/01/31/tree2.png)
```
Input: [1,2,3,4,5,6,7]
Output: [[4],[2],[1,5,6],[3],[7]]
Explanation: 
The node with value 5 and the node with value 6 have the same position according to the given scheme.
However, in the report "[1,5,6]", the node value of 5 comes first since 5 is smaller than 6.
```

**Note:**

1. The tree will have between 1 and 1000 nodes.
2. Each node's value will be between 0 and 1000.

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
    public List<List<Integer>> verticalTraversal(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        Map<Integer, TreeSet<int[]>> map = new TreeMap<>();
        helper(map, root, 0, 0);
        for (int order: map.keySet()){
            List<Integer> temp = new ArrayList<>();
            for (int[] pair: map.get(order)){
                temp.add(pair[0]);
            }
            res.add(temp);
        }
        return res;
    }
    
    private void helper(Map<Integer, TreeSet<int[]>> map, TreeNode node, int order, int level){
        if (node == null) return;
        if (!map.containsKey(order))
            map.put(order, new TreeSet<int[]>(new Comparator<int[]>(){
                @Override
                public int compare(int[] a, int[] b){
                    if (a[1] != b[1])
                        return a[1] - b[1];
                    else return a[0] - b[0];
                }
            }));
        map.get(order).add(new int[]{node.val, level});
        helper(map, node.left, order - 1, level + 1);
        helper(map, node.right, order + 1, level + 1);
    }
}
```

<hr />