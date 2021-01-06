---
title: Leetcode179-Largest Number
categories: leetcode
tags: [Sort, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-05 23:09:30
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a list of non-negative integers nums, arrange them such that they form the largest number.

Note: The result may be very large, so you need to return a string instead of an integer.

## Example

**Example 1:**
```
Input: nums = [10,2]
Output: "210"
```
**Example 2:**
```
Input: nums = [3,30,34,5,9]
Output: "9534330"
```
**Example 3:**
```
Input: nums = [1]
Output: "1"
```
**Example 4:**
```
Input: nums = [10]
Output: "10"
``` 

**Constraints:**

* 1 <= nums.length <= 100
* 0 <= nums[i] <= 10^9

## Solution

* Time Complexity: $$O(Nlog^N)$$
* Space Complexity: $$O(N)$$

```java
class Solution {
    public String largestNumber(int[] nums) {
        if (nums == null || nums.length == 0) return "";
        String[] sarr = new String[nums.length];
        for (int i = 0; i < nums.length; i++){
            sarr[i] = String.valueOf(nums[i]);
        }
        Arrays.sort(sarr, new Comparator<String>(){
            @Override
            public int compare(String a, String b){
                return (b + a).compareTo(a + b);
            }
        });
        StringBuilder res = new StringBuilder();
        for (String str: sarr)
            res.append(str);
        if (res.charAt(0) == '0')
            return "0";
        return res.toString();
    }
}
```

<hr />