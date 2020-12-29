---
title: Leetcode167-Two Sum II-Input Array Is Sorted
categories: leetcode
tags: [Two Pointers, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-12-25 18:09:32
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

**Note:**

* Your returned answers (both index1 and index2) are not zero-based.
* You may assume that each input would have exactly one solution and you may not use the same element twice.

## Example
**Example 1:**
```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```
**Example 2:**
```
Input: numbers = [2,3,4], target = 6
Output: [1,3]
```
**Example 3:**
```
Input: numbers = [-1,0], target = -1
Output: [1,2]
```

**Constraints:**

* 2 <= nums.length <= 3 * 104
* -1000 <= nums[i] <= 1000
* nums is sorted in increasing order.
* -1000 <= target <= 1000
## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(1)$$

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int i = 0;
        int j = numbers.length - 1;
        while(i < j){
            int cur = numbers[i] + numbers[j];
            if (cur == target){
                break;
            }
            else if (cur < target){
                i++;
            }
            else j--;
        }
        return new int[]{i + 1, j + 1};
    }
}
```

<hr />