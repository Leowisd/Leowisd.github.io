---
title: Leetcode1231-divideChocolate
categories: leetcode
tags: [Binary Search, Greedy, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 16:43:43
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

You have one chocolate bar that consists of some chunks. Each chunk has its own sweetness given by the array sweetness.

You want to share the chocolate with your K friends so you start cutting the chocolate bar into K+1 pieces using K cuts, each piece consists of some consecutive chunks.

Being generous, you will eat the piece with the minimum total sweetness and give the other pieces to your friends.

Find the maximum total sweetness of the piece you can get by cutting the chocolate bar optimally.

## Example
**Example 1:**
```
Input: sweetness = [1,2,3,4,5,6,7,8,9], K = 5
Output: 6
Explanation: You can divide the chocolate to [1,2,3], [4,5], [6], [7], [8], [9]
```
**Example 2:**
```
Input: sweetness = [5,6,7,8,9,1,2,3,4], K = 8
Output: 1
Explanation: There is only one way to cut the bar into 9 pieces.
```
**Example 3:**
```
Input: sweetness = [1,2,2,1,2,2,1,2,2], K = 2
Output: 5
Explanation: You can divide the chocolate to [1,2,2], [1,2,2], [1,2,2]
```
**Constraints:**

* 0 <= K < sweetness.length <= 10^4
* 1 <= sweetness[i] <= 10^5

## Solution
```java
// Binary Search
// Time O(Nlog(10^9))
// Space O(1)
class Solution {
    public int maximizeSweetness(int[] sweetness, int K) {
        int left = 1;
        int right = (int)1e9/(K + 1);
        
        while(left < right){
            int mid = (left + right + 1) / 2;
            int cur = 0;
            int cuts = 0;
            for (int sweet: sweetness){
                cur += sweet;
                if (cur >= mid){
                    cuts++;
                    cur = 0;
                    if (cuts > K) break;
                }
            }
            if (cuts > K)
                left = mid;
            else right = mid - 1;
        }
        
        return left;
    }
}
```

<hr />