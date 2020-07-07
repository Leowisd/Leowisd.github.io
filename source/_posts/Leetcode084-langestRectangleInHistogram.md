---
title: Leetcode084-langestRectangleInHistogram
categories: leetcode
tags: [Array, Stack, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-24 21:52:01
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](https://assets.leetcode.com/uploads/2018/10/12/histogram.png)

Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].

![](https://assets.leetcode.com/uploads/2018/10/12/histogram_area.png)

The largest rectangle is shown in the shaded area, which has area = 10 unit.

## Example
```
A histogram where width of each bar is 1, given height = [2,1,5,6,2,3].

The largest rectangle is shown in the shaded area, which has area = 10 unit.
```

## Solution

Method 1: calculate the most left and right bounds which higher than cur
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        if (heights == null || heights.length == 0) return 0;
        
        int[] leftHigher = new int[heights.length];
        int[] rightHigher = new int[heights.length];
        leftHigher[0] = -1;
        rightHigher[heights.length - 1] = heights.length;
        
        for (int i = 1; i < heights.length; i++){
            int index= i - 1;
            while (index >= 0 && heights[index] >= heights[i])
                index = leftHigher[index];
            leftHigher[i] = index;
        }
        for (int i = heights.length - 2; i >= 0; i--){
            int index = i + 1;
            while (index < heights.length && heights[index] >= heights[i])
                index = rightHigher[index];
            rightHigher[i] = index;
        }
        
        int res = Integer.MIN_VALUE;
        for (int i = 0; i < heights.length; i++){
            res = Math.max(res, (rightHigher[i] - leftHigher[i] - 1) * heights[i]);
        }
        
        return res;
    }
}
```

Method 2: Stack based solution, calculate each removed bar whose height larger then the cur. The speed is O(n), but slower than the above solution actually.
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        if (heights == null || heights.length == 0) return 0;
        Stack<Integer> st = new Stack<>();
        int res = 0;
        for (int i = 0; i <= heights.length; i++){
            int h = i == heights.length ? 0 : heights[i];
            while (!st.isEmpty() && h < heights[st.peek()]){
                int preHeight = heights[st.pop()];
                int preBoundary = st.isEmpty() ? -1 : st.peek();
                int len = i - preBoundary - 1;
                res = Math.max(res, preHeight * len);
            }
            st.push(i);
        }
        return res;
    }
}
```
<hr />