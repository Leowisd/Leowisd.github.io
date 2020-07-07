---
title: Leetcode069-sqrt(x)
categories: leetcode
tags: [Math, Binary Search]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-12 21:55:15
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Implement 
```
int sqrt(int x).
```
Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

## Example

**Example 1:**
```
Input: 4
Output: 2
```
**Example 2:**
```
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.
```
## Solution

Newton's method: https://blog.csdn.net/chenrenxiang/article/details/78286599

```java
class Solution {
    public int mySqrt(int x) {

//         Method 1 (Good to solve): Binary Search        
//         if (x == 0) return 0;
//         int left  = 1;
//         int right = Integer.MAX_VALUE;
        
//         while(left <= right){
//             int mid = left + (right - left)/2;
//             if (mid == x/mid) return mid;
//             else if (mid < x/mid) left = mid + 1;
//             else if (mid > x/mid) right = mid - 1;
//         }
//         return right;
        
        // Newton's method
        long r = x;
        while (r*r > x){
            r = (r + x/r)/2;
        }
        return (int)r;
    }
}
```

<hr />