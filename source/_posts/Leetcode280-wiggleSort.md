---
title: Leetcode280-Wiggle Sort
categories: leetcode
tags: [Array, Sort, Greedy, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2022-01-10 21:59:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an integer array nums, reorder it such that nums[0] <= nums[1] >= nums[2] <= nums[3]....

You may assume the input array always has a valid answer.

## Example

**Example 1:**
```
Input: nums = [3,5,2,1,6,4]
Output: [3,5,1,6,2,4]
Explanation: [1,6,2,5,3,4] is also accepted.
```
**Example 2:**
```
Input: nums = [6,6,5,6,3,8]
Output: [6,6,5,6,3,8]
```

**Constraints:**

* 1 <= nums.length <= 5 * 104
* 0 <= nums[i] <= 104
* It is guaranteed that there will be an answer for the given input nums.

**Follow up:** Could you solve the problem in O(n) time complexity?

## Solution

**Solution 1:** Sort, O(NlogN)
```java
class Solution {
    public void wiggleSort(int[] nums) {
        Arrays.sort(nums);
        for (int i = 1; i < nums.length - 1; i += 2){
            if (i % 2 == 1 && nums[i] < nums[i + 1]){
                int temp = nums[i];
                nums[i] = nums[i + 1];
                nums[i + 1] = temp;
            }
        }
    }
}
```

**Solution 2:** Greedy, O(N)
```java
class Solution {
//     Assume [0,i-1] are all wiggled
//     for position i
//     if i is even, then a[i - 2] <= a[i - 1]
//     if a[i - 1] >= a[i], pass
//     if a[i - 1] < a[i], swap a[i - 1] with a[i]. Since a[i - 2] <= a[i -1], so a[i - 2] < a[i], so [0, i] wiggled after swapping
    
//     if i is odd, then a[i - 2] >= a[i - 1]
//     if a[i - 1] <= a[i], pass
//     if a[i - 1] > a[i], swap a[i - 1] with a[i]. Since a[i - 2] >= a[i - 1], so a[i - 2] > a[i], so [0, i]wiggled after swapping 
    public void wiggleSort(int[] nums) {
        for (int i = 1; i < nums.length; i++){
            if (i % 2 == 0){
                if (nums[i - 1] < nums[i]){
                    swap(nums, i);
                }
            }
            else{
                if (nums[i - 1] > nums[i]){
                    swap(nums, i);
                }
            }
        }
    }
    
    private void swap(int[] nums, int idx){
        int temp = nums[idx - 1];
        nums[idx - 1] = nums[idx];
        nums[idx] = temp;
    }
}
```

<hr />