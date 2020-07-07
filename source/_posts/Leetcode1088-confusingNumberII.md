---
title: Leetcode1088-confusingNumberII
categories: leetcode
tags: [DFS, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 15:46:34
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
We can rotate digits by 180 degrees to form new digits. When 0, 1, 6, 8, 9 are rotated 180 degrees, they become 0, 1, 9, 8, 6 respectively. When 2, 3, 4, 5 and 7 are rotated 180 degrees, they become invalid.

A confusing number is a number that when rotated 180 degrees becomes a different number with each digit valid.(Note that the rotated number can be greater than the original number.)

Given a positive integer N, return the number of confusing numbers between 1 and N inclusive.

## Example
**Example 1:**
```
Input: 20
Output: 6
Explanation: 
The confusing numbers are [6,9,10,16,18,19].
6 converts to 9.
9 converts to 6.
10 converts to 01 which is just 1.
16 converts to 91.
18 converts to 81.
19 converts to 61.
```
**Example 2:**
```
Input: 100
Output: 19
Explanation: 
The confusing numbers are [6,9,10,16,18,19,60,61,66,68,80,81,86,89,90,91,98,99,100].
```
**Note:**

1 <= N <= 10^9

## Solution
```java
class Solution {
    int res = 0;
    HashMap<Integer, Integer> map = new HashMap<>();
    public int confusingNumberII(int N) {
        map.put(0, 0);
        map.put(1, 1);
        map.put(6, 9);
        map.put(8, 8);
        map.put(9, 6);
        
        helper(0, 0, N);
        return N == 1000000000 ? res + 1 : res;
    }
    private void helper(int idx, int cur, int N){
        if (idx > 9 || cur > N)
            return;
        if (isConfused(cur))
            res++;
        for (int number: map.keySet()){
            if (idx == 0 && number == 0)
                continue;
            helper(idx + 1, cur * 10 + number, N);
        }
    }
    private boolean isConfused(int x){
        long rot = 0;
        int temp = x;
        while(x > 0){
            rot = rot * 10 + map.get(x % 10);
            x /= 10;
        }
        return rot != temp;
    }
}
```

<hr />