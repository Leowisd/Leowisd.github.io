---
title: Leetcode945-minimumIncrementToMakeArrayUnique
categories: leetcode
tags: [Array, Map]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-25 22:35:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers A, a move consists of choosing any A[i], and incrementing it by 1.

Return the least number of moves to make every value in A unique.

## Example
**Example 1:**
```
Input: [1,2,2]
Output: 1
Explanation:  After 1 move, the array could be [1, 2, 3].
```
**Example 2:**
```
Input: [3,2,1,2,1,7]
Output: 6
Explanation:  After 6 moves, the array could be [3, 4, 1, 2, 5, 7].
It can be shown with 5 or less moves that it is impossible for the array to have all unique values.
```
## Solution
```java
class Solution {
    public int minIncrementForUnique(int[] A) {
        if (A == null || A.length == 0) return 0;
        // Method 1: O(NlgN)
        Arrays.sort(A);
        int steps = 0;
        int available = 0;
        // int available = A[0];
        for (int it: A){
            steps += Math.max(available - it, 0);
            available = Math.max(available, it) + 1;
            // Not clean style
            // if (available >= it){
            //     steps += available - it;
            //     available ++;
            // }
            // else available = it + 1;
        }
        
        // Method 2: O(NlgK)
        // TreeMap<Integer, Integer> map = new TreeMap<>();
        // for (int it: A){
        //     map.put(it, map.getOrDefault(it, 0)+1);
        // }
        // int steps = 0;
        // int available = 0;
        // for (int it: map.keySet()){
        //     int count = map.get(it);
        //     steps += count * Math.max(available - it, 0) + count*(count-1)/2;
        //     available = Math.max(available, it) + count;
        // }
        
        return steps;
    }
}
```
```python
# Union Find, average O(N)
    def minIncrementForUnique(self, A):
        root = {}
        def find(x):
            if x not in root:
                root[x] = x
            elif x != root[x]:
                root[x] = find(root[x])
            elif x + 1 in root:
                root[x] = find(root[x + 1])
            else:
                root[x] = root[x + 1] = x + 1
            return root[x]
        return sum(find(a) - a for a in A)
    }
```
<hr />