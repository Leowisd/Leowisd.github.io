---
title: Leetcode171-excelSheetColumnNumber
categories: leetcode
tags: [Math, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 22:00:14
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:
```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
```
## Example
**Example 1:**
```
Input: "A"
Output: 1
```
**Example 2:**
```
Input: "AB"
Output: 28
```
**Example 3:**
```
Input: "ZY"
Output: 701
```

## Solution
```java
class Solution {
    public int titleToNumber(String s) {
        if (s == null || s.length() == 0) return 0;
        int res = 0;
        int cur = 1;
        for (int i = s.length() - 1; i >= 0; i--){
            res += cur * (s.charAt(i) - 'A' + 1);
            cur *= 26;
        }
        return res;
    }
}
```

<hr />