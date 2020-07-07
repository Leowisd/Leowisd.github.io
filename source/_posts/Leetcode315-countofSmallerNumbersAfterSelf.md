---
title: Leetcode315-countofSmallerNumbersAfterSelf
categories: leetcode
tags: [Binary Search Tree, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-29 11:35:59
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

## Example
```
Input: [5,2,6,1]
Output: [2,1,1,0] 
Explanation:
To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
```

## Solution
```java
class Solution {
    class Node{
        Node left,right;
        int val;
        int count;
        int dup = 1;
        public Node(int val, int count){
            this.val = val;
            this.count = count;
        }
    }
    public List<Integer> countSmaller(int[] nums) {
        Integer[] res = new Integer[nums.length];
        Node root = null;
        for (int i = nums.length - 1; i >= 0; i--){
            root = insert(nums[i], root, res, i, 0);
        }
        return Arrays.asList(res);
    }
    
    private Node insert(int num, Node node, Integer[] res, int i, int pre){
        if (node == null){
            node = new Node(num, 0);
            res[i] = pre;
        }
        else if (node.val == num){
            node.dup++;
            res[i] = pre + node.count;
        }
        else if (node.val > num){
            node.count++;
            node.left = insert(num, node.left, res, i, pre);
        }
        else node.right = insert(num, node.right, res, i, pre + node.count + node.dup);
        return node;
    }
}
```
Every node will maintain a val sum recording the total of number on it's left bottom side, dup counts the duplication. For example, [3, 2, 2, 6, 1], from back to beginning,we would have:
```
                1(0, 1)
                     \
                     6(3, 1)
                     /
                   2(0, 2)
                       \
                        3(0, 1)
```
<hr />