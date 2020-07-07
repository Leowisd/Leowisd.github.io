---
title: Leetcode503-nextGreaterElementII
categories: leetcode
tags: [Stack, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-14 11:41:51
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.

## Example
```
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number; 
The second 1's next greater number needs to search circularly, which is also 2.
```
**Note:** The length of given array won't exceed 10000.

## Solution
```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        if (nums == null || nums.length == 0) return new int[0];
        int[] res = new int[nums.length];
        
        Stack<Integer> st = new Stack<>();
        
        for (int i = nums.length - 1; i >= 0; i--) st.push(i);
        
        for (int i = nums.length - 1; i >= 0; i--){
            res[i] = -1;
            while(!st.isEmpty() && nums[i] >= nums[st.peek()]) st.pop();
            if (!st.isEmpty()) res[i] = nums[st.peek()];
            st.push(i);
        }
        
        return res;
    }
}
```

<hr />