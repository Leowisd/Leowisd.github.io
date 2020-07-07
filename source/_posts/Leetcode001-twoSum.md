---
title: Leetcode001-twoSum
categories: leetcode
tags: [Hash Table, Amazon, Microsoft, Google, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-08 17:45:39
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

## Example
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## Solution
```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] res = new int[2];
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < numbers.length; i++) {
            if (map.containsKey(target - numbers[i])) {
                res[1] = i;
                res[0] = map.get(target - numbers[i]);
                return res;
            }
            map.put(numbers[i], i);
        }
        return res;
    }
}
```

<hr />