---
title: Leetcode042-trappingRainWater
categories: leetcode
tags: [Two Pointers, Amazon, Microsoft, Google, Bloomberg, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-08 17:21:43
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)
The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. Thanks Marcos for contributing this image!
## Example
```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

## Solution
```java
class Solution {
    public int trap(int[] height) {
        int res = 0;
        if (height == null || height.length == 0) return res;
        
        int i = 0, j = height.length-1;
        int leftmax = 0, rightmax = 0;
        while(i <= j){
            leftmax = Math.max(leftmax, height[i]);
            rightmax = Math.max(rightmax, height[j]);
            if (leftmax < rightmax){// leftmax is smaller than rightmax, so the (leftmax-A[a]) water can be stored
                res += leftmax - height[i];
                i++;
            }
            else{
                res += rightmax - height[j];
                j--;
            }
        }
        return res;
    }
}
```

<hr />