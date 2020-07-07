---
title: Leetcode307-rangeSumQuery-Mutable
categories: leetcode
tags: [Binary Indexed Tree, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-15 00:36:14
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

The update(i, val) function modifies nums by updating the element at index i to val.

## Example
```
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```
**Note:**

1. The array is only modifiable by the update function.
2. You may assume the number of calls to update and sumRange function is distributed evenly.

## Solution
```java
class NumArray {
    private int[] nums;
    private int[] BIT;
    public NumArray(int[] nums) {
        this.nums = nums;
        this.BIT = new int[nums.length + 1];
        for (int i=0; i<nums.length; i++){
            add(i, nums[i]);
        }
    }
    
    private void add(int k, int delt){
        k++;
        while (k <= nums.length){
            BIT[k] += delt;
            k += k & (-k);
        }
    }
    
    public void update(int i, int val) {
        int diff = val - nums[i];
        nums[i] = val;
        add(i, diff);
    }
    
    private int getSum(int k){
        int temp = 0;
        k++;
        while (k>0){
            temp += BIT[k];
            k -= k & (-k);
        }
        return temp;
    }
    
    public int sumRange(int i, int j) {
        return getSum(j) - getSum(i - 1);    
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(i,val);
 * int param_2 = obj.sumRange(i,j);
 */
```

<hr />