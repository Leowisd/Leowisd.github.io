---
title: Leetcode410-splitArrayLargestSum
categories: leetcode
tags: [Binary Search, Google, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-29 11:07:20
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given an array which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays. Write an algorithm to minimize the largest sum among these m subarrays.

**Note:**
If n is the length of array, assume the following constraints are satisfied:

* 1 ≤ n ≤ 1000
* 1 ≤ m ≤ min(50, n)

## Example
```
Input:
nums = [7,2,5,10,8]
m = 2

Output:
18

Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

## Solution
1. Given a result, it is easy to test whether it is valid or not.
2. The max of the result is the sum of the input nums.
3. The min of the result is the max num of the input nums.
Given the 3 conditions above we can do a binary search. (need to deal with overflow)
```java
class Solution {
    public int splitArray(int[] nums, int m) {
        long sum = 0;
        long max = 0;
        for (int num: nums){
            max = Math.max(max, num);
            sum += num;
        }
        
        long low = max;
        long high = sum;
        while(low < high){
            long mid = (low + high)/2;
            if (valid(nums, m, mid)){
                high = mid;
            }
            else low = mid + 1;
        }
        return (int)high;
    }
    
    private boolean valid(int[] nums, int m, long max){
        long cur = 0;
        int count = 1;
        for (int num: nums){
            cur += num;
            if (cur > max){
                cur = num;
                count++;
                if (count > m) return false;
            }
        }
        return true;
    }

}
```

<hr />