---
title: Leetcode128-longestConsecutiveSequence
categories: leetcode
tags: [Array, Bloomberg, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-10 19:05:16
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O(n) complexity.

## Example
```
Input: [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

## Solution
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        int res = 0;
        HashSet<Integer> set = new HashSet<>();
        for (int num: nums)
            set.add(num);
        for (int num: set){
            if (!set.contains(num-1)){
                int temp = num + 1;
                while(set.contains(temp))
                    temp++;
                res = Math.max(res, temp - num);
            }
        }
        return res;
    }
}
```

<hr />