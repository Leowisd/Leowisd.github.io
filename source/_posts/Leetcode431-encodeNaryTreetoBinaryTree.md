---
title: Leetcode431-encodeNaryTreetoBinaryTree
categories: leetcode
tags: [Tree, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-22 10:27:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Design an algorithm to encode an N-ary tree into a binary tree and decode the binary tree to get the original N-ary tree. An N-ary tree is a rooted tree in which each node has no more than N children. Similarly, a binary tree is a rooted tree in which each node has no more than 2 children. There is no restriction on how your encode/decode algorithm should work. You just need to ensure that an N-ary tree can be encoded to a binary tree and this binary tree can be decoded to the original N-nary tree structure.

For example, you may encode the following 3-ary tree to a binary tree in this way:

![](https://assets.leetcode.com/uploads/2018/10/12/narytreebinarytreeexample.png)

Note that the above is just an example which might or might not work. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note:**

1. N is in the range of [1, 1000]
2. Do not use class member/global/static variables to store states. Your encode and decode algorithms should be stateless.

## Solution
Basic idea: next level -> left, same level -> right;
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Codec {

    // Encodes an n-ary tree to a binary tree.
    public TreeNode encode(Node root) {
        if (root == null) return null;
        
        TreeNode res = new TreeNode(root.val);
        if (root.children.size() > 0)
            res.left = encode(root.children.get(0));
        
        TreeNode cur = res.left;
        for (int i = 1; i < root.children.size(); i++){
            cur.right = encode(root.children.get(i));
            cur = cur.right;
        }
        
        return res;
    }

    // Decodes your binary tree to an n-ary tree.
    public Node decode(TreeNode root) {
        if (root == null) return null;
        
        Node res  = new Node(root.val, new ArrayList<>());
        TreeNode cur = root.left;
        while (cur != null){
            res.children.add(decode(cur));
            cur = cur.right;
        }
        return res;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(root));
```

<hr />