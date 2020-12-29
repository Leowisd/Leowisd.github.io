---
title: Leetcode777-Swap Adjacent In LR String
categories: leetcode
tags: [Two Pointers, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-12-25 17:52:35
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

In a string composed of 'L', 'R', and 'X' characters, like "RXXLRXRXL", a move consists of either replacing one occurrence of "XL" with "LX", or replacing one occurrence of "RX" with "XR". Given the starting string start and the ending string end, return True if and only if there exists a sequence of moves to transform one string to the other.

## Example
**Example 1:**
```
Input: start = "RXXLRXRXL", end = "XRLXXRRLX"
Output: true
Explanation: We can transform start to end following these steps:
RXXLRXRXL ->
XRXLRXRXL ->
XRLXRXRXL ->
XRLXXRRXL ->
XRLXXRRLX
```
**Example 2:**
```
Input: start = "X", end = "L"
Output: false
```
**Example 3:**
```
Input: start = "LLR", end = "RRL"
Output: false
```
**Example 4:**
```
Input: start = "XL", end = "LX"
Output: true
```
**Example 5:**
```
Input: start = "XLLR", end = "LXLX"
Output: false
```

**Constraints:**

* 1 <= start.length <= 104
* start.length == end.length
* Both start and end will only consist of characters in 'L', 'R', and 'X'.


## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

```java
class Solution {
    public boolean canTransform(String start, String end) {
        if (start.length() != end.length()) return false;
        // if (!start.replace("X", "").equals(end.replace("X", ""))) return false;
        int i = 0;
        int j = 0;
        char[] startArr = start.toCharArray();
        char[] endArr = end.toCharArray();
        // while (i < startArr.length && j < endArr.length){
        while (i < startArr.length || j < endArr.length){
            while(i < startArr.length && startArr[i] == 'X') i++;
            while(j < endArr.length && endArr[j] == 'X') j++;
            
            if (i == startArr.length && j == endArr.length) return true;
            if (i == startArr.length || j == endArr.length) return false;
            
            if (startArr[i] != endArr[j]) return false;
            if (startArr[i] == 'L' && i < j) return false;
            if (startArr[i] == 'R' && i > j) return false;
            i++;
            j++;
        }
        // return true;
        return i == j;
    }
}
```

<hr />