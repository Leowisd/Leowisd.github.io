---
title: Leetcode449-Serialize And Deserialize BST
categories: leetcode
tags: [Tree, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-05 00:56:10
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Serialization is converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary search tree. There is no restriction on how your serialization/deserialization algorithm should work. You need to ensure that a binary search tree can be serialized to a string, and this string can be deserialized to the original tree structure.

**The encoded string should be as compact as possible.**

## Example
**Example 1:**
```
Input: root = [2,1,3]
Output: [2,1,3]
```
**Example 2:**
```
Input: root = []
Output: []
```

**Constraints:**

* The number of nodes in the tree is in the range [0, 104].
* 0 <= Node.val <= 104
* The input tree is guaranteed to be a binary search tree.

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null) return "";
        StringBuilder sb = new StringBuilder();
        serializeHelper(sb, root);
        return sb.toString();
    }
    
    private void serializeHelper(StringBuilder sb, TreeNode node){
        if (node == null) return;
        sb.append(node.val);
        sb.append(",");
        serializeHelper(sb, node.left);
        serializeHelper(sb, node.right);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data == null || data.length() == 0) return null;
        Queue<String> q = new LinkedList<>(Arrays.asList(data.split(",")));
        return deserializeHelper(q, Integer.MIN_VALUE, Integer.MAX_VALUE);   
    }
    
    private TreeNode deserializeHelper(Queue<String> q, int min, int max){
        if (q.isEmpty()) return null;
        int cur = Integer.parseInt(q.peek());
        if (cur < min || cur > max) return null;
        q.poll();
        TreeNode node = new TreeNode(cur);
        node.left = deserializeHelper(q, min, cur);
        node.right = deserializeHelper(q, cur, max);
        return node;
    } 
}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// String tree = ser.serialize(root);
// TreeNode ans = deser.deserialize(tree);
// return ans;
```

<hr />