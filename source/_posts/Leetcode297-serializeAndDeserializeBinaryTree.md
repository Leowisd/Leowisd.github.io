---
title: Leetcode297-serializeAndDeserializeBinaryTree
categories: leetcode
tags: [Tree, Design, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-08 10:31:28
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

## Example
```
You may serialize the following tree:

    1
   / \
  2   3
     / \
    4   5

as "[1,2,3,null,null,4,5]"
```

**Clarification:** The above format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note:** Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

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
public class Codec {

    
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder res = new StringBuilder();
        serializeTree(root, res);
        return res.toString();
    }
    
    private void serializeTree(TreeNode node, StringBuilder res){
        if (node == null){
            res.append("null").append(",");
            return;
        }
        res.append(String.valueOf(node.val)).append(",");
        serializeTree(node.left, res);
        serializeTree(node.right, res);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        Queue<String> q = new LinkedList<>();
        String[] tmp = data.split(",");
        for (int i = 0; i < tmp.length - 1; i++) q.offer(tmp[i]);
        return  deserialize(q);
    }
    
    private TreeNode deserialize(Queue<String> q){
        if (!q.isEmpty()){
            String f = q.poll();
            if (f.equals("null")) return null;
            TreeNode node = new TreeNode(Integer.valueOf(f));
            node.left = deserialize(q);
            node.right = deserialize(q);
            return node;
        }
        return null;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

<hr />