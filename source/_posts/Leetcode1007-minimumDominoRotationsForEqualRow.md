---
title: Leetcode1007-minimumDominoRotationsForEqualRow
categories: leetcode
tags: [Array, Greedy, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 15:27:52
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

In a row of dominoes, A[i] and B[i] represent the top and bottom halves of the i-th domino.  (A domino is a tile with two numbers from 1 to 6 - one on each half of the tile.)

We may rotate the i-th domino, so that A[i] and B[i] swap values.

Return the minimum number of rotations so that all the values in A are the same, or all the values in B are the same.

If it cannot be done, return -1.

## Example
**Example 1:**
![](https://assets.leetcode.com/uploads/2019/03/08/domino.png)
```
Input: A = [2,1,2,4,2,2], B = [5,2,6,2,3,2]
Output: 2
Explanation: 
The first figure represents the dominoes as given by A and B: before we do any rotations.
If we rotate the second and fourth dominoes, we can make every value in the top row equal to 2, as indicated by the second figure.
```
**Example 2:**
```
Input: A = [3,5,1,2,3], B = [3,6,3,3,4]
Output: -1
Explanation: 
In this case, it is not possible to rotate the dominoes to make one row of values equal.
```

**Note:**

1. 1 <= A[i], B[i] <= 6
2. 2 <= A.length == B.length <= 20000

## Solution
```java
class Solution {
    public int minDominoRotations(int[] A, int[] B) {
        for (int i = 1; i <= 6; i++){
            boolean flag = false;
            for (int j = 0; j < A.length; j++){
                if (A[j] != i && B[j] != i){
                    flag = true;
                    break;
                }
            }
            if (flag) continue;
            int numa = 0;
            int numb = 0;
            for (int j = 0; j < A.length; j++){
                if (A[j] != i) numa++;
                if (B[j] != i) numb++;
            }
            return Math.min(numa, numb);
        }
        return -1;
    }
}
```

<hr />