---
title: Leetcode528-randomPickwithWeight
categories: leetcode
tags: [Binary Search, Random, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-11-04 14:17:18
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given an array w of positive integers, where w[i] describes the weight of index i, write a function pickIndex which randomly picks an index in proportion to its weight.

Note:

1. 1 <= w.length <= 10000
2. 1 <= w[i] <= 10^5
3. pickIndex will be called at most 10000 times.

## Example
**Example 1:**
```
Input: 
["Solution","pickIndex"]
[[[1]],[]]
Output: [null,0]
```
**Example 2:**
```
Input: 
["Solution","pickIndex","pickIndex","pickIndex","pickIndex","pickIndex"]
[[[1,3]],[],[],[],[],[]]
Output: [null,0,1,1,1,0]
```
**Explanation of Input Syntax:**

The input is two lists: the subroutines called and their arguments. Solution's constructor has one argument, the array w. pickIndex has no arguments. Arguments are always wrapped with a list, even if there aren't any.

## Solution
```java
class Solution {
    
    int[] wsum;
    Random random;
    public Solution(int[] w) {
        random = new Random();
        for (int i = 1; i < w.length; i++){
            w[i] += w[i - 1];
        }
        wsum = w;
    }
    
    public int pickIndex() {
        int t = random.nextInt(wsum[wsum.length - 1]) + 1;
        int left = 0;
        int right = wsum.length - 1;
        while(left < right){
            int mid = left + (right - left)/2;
            if (wsum[mid] == t) return mid;
            else if (wsum[mid] < t) left = mid + 1;
            else right = mid;
        }
        return left;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```

**Explain:**
Use accumulated freq array to get idx.
w[] = {2,5,3,4} => wsum[] = {2,7,10,14}
then get random val random.nextInt(14)+1, idx is in range [1,14]
```
idx in [1,2] return 0
idx in [3,7] return 1
idx in [8,10] return 2
idx in [11,14] return 3
```
then become LeetCode 35. Search Insert Position

<hr />