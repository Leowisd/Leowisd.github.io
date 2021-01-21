---
title: Leetcode974-Subarray Sums Divisible by K
categories: leetcode
tags: [Array, Hash Table, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-05 18:21:27
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array A of integers, return the number of (contiguous, non-empty) subarrays that have a sum divisible by K.

## Example

**Example 1:**
```
Input: A = [4,5,0,-2,-3,1], K = 5
Output: 7
Explanation: There are 7 subarrays with a sum divisible by K = 5:
[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]
```

**Note:**

* 1 <= A.length <= 30000
* -10000 <= A[i] <= 10000
* 2 <= K <= 10000

## Solution

```
If a subarray is divisible by K, it has to be a multiple of K

a-b=n*k, a = running total, b = any previous subarray sum, same as original prefix sum problems.

We want to solve for b, so using basic algebra, b=a-n*k

We don't know what n is, so we can get rid of n by modding every element by k
(b%k) = (a%k) - (n*k)%k

since n*k is a multiple of k and k goes into it evenly, the result of the (n *k)%k will be 0

therefore
b%k = a%k

is the same as the formula we defined earlier, a-b=n*k

where b = running total, a = any previous subarray sum

So we just have to see if running total mod k is equal to any previous running total mod k
```

### Solution 1: Prefix + Hash Table

* Time Complexity: $$O(N)$$, N = A.length
* Space Complexity: $$O(K)$$

```java
class Solution {
    public int subarraysDivByK(int[] A, int K) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int prefix = 0;
        map.put(0, 1);
        int res = 0;
        
        for (int x: A){
            prefix = (prefix + x % K + K) % K;
            res += map.getOrDefault(prefix, 0);
            map.put(prefix, map.getOrDefault(prefix, 0) + 1);
        }      
        return res;
    }
}
```

### Solution 2: Prefix + Array, faster
```java
class Solution {
    public int subarraysDivByK(int[] A, int K) {
        int[] count = new int[K];
        count[0] = 1;
        int prefix = 0, res = 0;
        for (int a : A) {
            prefix = (prefix + a % K + K) % K;
            res += count[prefix]++;
        }
        return res;
    }
}
```

<hr />