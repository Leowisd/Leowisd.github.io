---
title: Leetcode450-Delet Node in a BST
categories: leetcode
tags: [Tree, BST, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2022-01-13 15:32:00
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

* Search for a node to remove.
* If the node is found, delete the node.


## Example

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/04/del_node_1.jpg)

```
Input: root = [5,3,6,2,4,null,7], key = 3
Output: [5,4,6,2,null,null,7]
Explanation: Given key to delete is 3. So we find the node with value 3 and delete it.
One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.
```
![](https://assets.leetcode.com/uploads/2020/09/04/del_node_supp.jpg)

**Example 2:**
```
Input: root = [5,3,6,2,4,null,7], key = 0
Output: [5,3,6,2,4,null,7]
Explanation: The tree does not contain a node with value = 0.
```
**Example 3:**
```
Input: root = [], key = 0
Output: []
```
**Constraints:**

* The number of nodes in the tree is in the range [0, 104].
* -105 <= Node.val <= 105
* Each node has a unique value.
* root is a valid binary search tree.
* -105 <= key <= 105

## Solution

* Time Complexity: $$O(logN)$$ or $$O(H)$$
* Space Complexity: $$O(N)$$

```java
// O(logN) = O(H)
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return null;
        
        if (key < root.val){
            root.left = deleteNode(root.left, key);
        }
        else if (key > root.val){
            root.right = deleteNode(root.right, key);
        }
        else{
            if (root.left == null && root.right == null){
                root = null;
            }
            else if (root.right != null){
                root.val = nextLarger(root);
                root.right = deleteNode(root.right, root.val);
            }
            else {
                root.val = preSmaller(root);
                root.left = deleteNode(root.left, root.val);
            }
        }
        return root;
    }
    
    private int nextLarger(TreeNode root){
        root = root.right;
        while(root.left != null) root = root.left;
        return root.val;
    }
    
    private int preSmaller(TreeNode root){
        root = root.left;
        while(root.right != null) root = root.right;
        return root.val;
    }
}
```

<hr />