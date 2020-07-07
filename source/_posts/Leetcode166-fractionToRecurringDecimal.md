---
title: Leetcode166-fractionToRecurringDecimal
categories: leetcode
tags: [Hash Table, Math, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-16 22:53:30
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

## Example
**Example 1:**
```
Input: numerator = 1, denominator = 2
Output: "0.5"
```
**Example 2:**
```
Input: numerator = 2, denominator = 1
Output: "2"
```
**Example 3:**
```
Input: numerator = 2, denominator = 3
Output: "0.(6)"
```

## Solution
```java
class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        if (numerator == 0) return "0";
        StringBuilder res = new StringBuilder();
        res.append((numerator > 0) ^ (denominator > 0) ? "-" : "");
        long num = Math.abs((long)numerator);
        long den = Math.abs((long)denominator);
        
//      integral part
        res.append(num / den);
        num %= den;
        if (num == 0) 
            return res.toString();
        
//      fraction part
        res.append(".");
        HashMap<Long, Integer> map = new HashMap<>();
        map.put(num, res.length());
        while(num > 0){
            num *= 10;
            res.append(num / den);
            num %= den;
            if (map.containsKey(num)){
                res.insert(map.get(num), "(");
                res.append(")");
                break;
            }
            else map.put(num, res.length());
        }
        
        return res.toString();
    }
}
```

<hr />