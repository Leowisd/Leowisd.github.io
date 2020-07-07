---
title: Leetcode659-splitArrayIntoConsecutiveSubsequences
categories: leetcode
tags: [Heap, Greedy, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 16:58:32
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array nums sorted in ascending order, return true if and only if you can split it into 1 or more subsequences such that each subsequence consists of consecutive integers and has length at least 3.

## Example
**Example 1:**
```
Input: [1,2,3,3,4,5]
Output: True
Explanation:
You can split them into two consecutive subsequences : 
1, 2, 3
3, 4, 5
```
**Example 2:**
```
Input: [1,2,3,3,4,4,5,5]
Output: True
Explanation:
You can split them into two consecutive subsequences : 
1, 2, 3, 4, 5
3, 4, 5
```
**Example 3:**
```
Input: [1,2,3,4,4,5]
Output: False
```

**Constraints:**
* 1 <= nums.length <= 10000
 

## Solution
I used a greedy algorithm.

leftis a hashmap, left[i] counts the number of i that I haven't placed yet.

endis a hashmap, end[i] counts the number of consecutive subsequences that ends at number i

Then I tried to split the nums one by one.

If I could neither add a number to the end of a existing consecutive subsequence nor find two following number in the left, I returned False

Time: O(N)

```java
class Solution {
    public boolean isPossible(int[] nums) {
        HashMap<Integer, Integer> left = new HashMap<>();
        HashMap<Integer, Integer> end = new HashMap<>();
        for (int num: nums){
            left.put(num, left.getOrDefault(num, 0) + 1);
            end.put(num, 0);            
        }
        
        for (int num: nums){
            if (left.get(num) == 0) continue;
            left.put(num, left.get(num) - 1);
            if (end.getOrDefault(num - 1, 0) > 0){
                end.put(num - 1, end.get(num - 1) - 1);
                end.put(num, end.get(num) + 1);
            }
            else if (left.getOrDefault(num + 1, 0) > 0 && left.getOrDefault(num + 2, 0) > 0){
                left.put(num + 1, left.get(num + 1) - 1);
                left.put(num + 2, left.get(num + 2) - 1);
                end.put(num + 2, end.get(num + 2) + 1);
            }
            else return false;
        }
        
        return true;
    }
}
```

<hr />