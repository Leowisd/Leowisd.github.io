---
title: Leetcode011-containerWithMostWater
tags: [Greedy, Bloomberg]
mathjax: true
date: 2019-01-23 10:47:32
categories: leetcode
description: Solution Report of LeetCode Acceptted
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

### Note

You may not slant the container and n is at least 2.

![](http://ww1.sinaimg.cn/large/cf684029ly1fzhkuw8yqij20m90anwep.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

## Example

```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

## Solution

Greedy

Using two pointers, one to the head and one to the tail

There is a feature, the area of two edges not smaller than the area of the shorter edge with all other edges between the two edges

```python
class Solution:
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        i = 0
        j = len(height)-1
        
        result = 0
        
        while i<j:
            result = max(result, min(height[i], height[j])*(j-i))
            if height[i]<height[j]:
                i += 1
            else:
                j -= 1
        
        return result
```

<hr />