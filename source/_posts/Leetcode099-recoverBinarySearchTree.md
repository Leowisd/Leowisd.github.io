---
title: Leetcode099-recoverBinarySearchTree
categories: leetcode
tags: [Tree, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-22 22:05:58
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

## Example
**Example 1:**
```
Input: [1,3,null,null,2]

   1
  /
 3
  \
   2

Output: [3,1,null,null,2]

   3
  /
 1
  \
   2
```
**Example 2:**
```
Input: [3,1,4,null,null,2]

  3
 / \
1   4
   /
  2

Output: [2,1,4,null,null,3]

  2
 / \
1   4
   /
  3
```

**Follow up:**

* A solution using O(n) space is pretty straight forward.
* Could you devise a constant space solution?

## Solution

Method 1: Straight method, in-order traversal, space $O(n)$
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
    
    public void recoverTree(TreeNode root) {
        if (root == null) return;
        
        Stack<TreeNode> st = new Stack<TreeNode>();
        TreeNode firstNode =  null;
        TreeNode secondNode = null;
        TreeNode preNode = null;
        
        while(root != null || !st.isEmpty()){
            while (root != null){
                st.push(root);
                root = root.left;
            };
            
            root = st.pop();
            if (preNode != null && preNode.val >= root.val){
                if (firstNode == null) firstNode = preNode;
                if (firstNode != null) secondNode = root;
            }
            preNode = root;
            root = root.right;
        }
        
        int temp = firstNode.val;
        firstNode.val = secondNode.val;
        secondNode.val = temp;
    }
}
```

Method 2: Used Morris Traversal, which based on threaded binary tree. Space $O(1)$
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
    // Used Morris Traversal, which based on threaded binary tree
    public void recoverTree(TreeNode root) {
        TreeNode pre = null;
        TreeNode first = null, second = null;
        // Morris Traversal
        TreeNode temp = null;
		while(root!=null){
			if(root.left!=null){
				// connect threading for root
				temp = root.left;
				while(temp.right!=null && temp.right != root)
					temp = temp.right;
				// the threading already exists
				if(temp.right!=null){
				    if(pre!=null && pre.val > root.val){
				        if(first==null){first = pre;second = root;}
				        else{second = root;}
				    }
				    pre = root;
				    
					temp.right = null;
					root = root.right;
				}else{
					// construct the threading
					temp.right = root;
					root = root.left;
				}
			}else{
				if(pre!=null && pre.val > root.val){
				    if(first==null){first = pre;second = root;}
				    else{second = root;}
				}
				pre = root;
				root = root.right;
			}
		}
		// swap two node values;
		if(first!= null && second != null){
		    int t = first.val;
		    first.val = second.val;
		    second.val = t;
		}
    }
}
```
<hr />