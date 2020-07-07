---
title: Leetcode067-addBinary
categories: leetcode
tags: [String]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-11-19 00:14:53
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two binary strings, return their sum (also a binary string).

The input strings are both non-empty and contains only characters 1 or 0.

## Example
**Example 1:**
```
Input: a = "11", b = "1"
Output: "100"
```
**Example 2:**
```
Input: a = "1010", b = "1011"
Output: "10101"
```

## Solution
```java
public class Solution {
    public String addBinary(String a, String b) {
        String res = "";
        int i = a.length() - 1, j = b.length() -1, carry = 0;
        while (i >= 0 || j >= 0) {
            int sum = carry;
            if (j >= 0) sum += b.charAt(j--) - '0';
            if (i >= 0) sum += a.charAt(i--) - '0';
            res = (sum % 2) + res;
            carry = sum / 2;
        }
        if (carry != 0) res = carry + res;
        return res;
    }
}
```

<hr />