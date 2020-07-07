---
title: Leetcode031-nextPermutation
categories: leetcode
tags: [Array, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 20:33:18
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

## Solution

Step 1: From the end, find the first element breaks the decsending sequence, which is the element need to be changed to a bigger because the decsending elements after it are already finished

Step 2: From the end, find the first element that bigger than the element found at step 1, which is the new elelment at the position of the step 1 emelemt. Swap them, which doesn't change the decsending order of that sequence.

Step 3: Reverse the decsending sequence.

```java
class Solution {
    public void nextPermutation(int[] nums) {
        if (nums == null || nums.length == 0) return;
        int idx = nums.length - 2;
        while(idx >= 0 && nums[idx] >= nums[idx + 1]) idx--; // Find 1st id i that breaks descending order
        
        if (idx >= 0){                                       // If not entirely descending
            int j = nums.length - 1;                         // Start from the end
            while(j > idx && nums[j] <= nums[idx]) j--;      // Find rightmost first larger id j
            swap(nums, idx, j);                              // Switch i and j
        }
        
        reverse(nums, idx + 1, nums.length - 1);             // Reverse the descending sequence
    }
    
    private void swap(int[] nums, int x, int y){
        int tmp = nums[x];
        nums[x] = nums[y];
        nums[y] = tmp;
    }
    private void reverse(int[] nums, int x, int y){
        while(x < y) swap(nums, x++, y--);
    }
}
```

<hr />