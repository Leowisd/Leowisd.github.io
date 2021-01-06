---
title: Leetcode224-basicCalculator
categories: leetcode
tags: [Stack, Amazon, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-15 00:29:34
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open ( and closing parentheses ), the plus + or minus sign -, non-negative integers and empty spaces.

## Example
**Example 1:**
```
Input: "1 + 1"
Output: 2
```
**Example 2:**
```
Input: " 2-1 + 2 "
Output: 3
```
**Example 3:**
```
Input: "(1+(4+5+2)-3)+(6+8)"
Output: 23
```
**Note:**
* You may assume that the given expression is always valid.
* Do not use the eval built-in library function.

## Solution
```java
class Solution {
    public int calculate(String s) {
        Stack<Integer> st = new Stack<>();
        
        int res = 0;
        int number = 0;
        int sign = 1;
        
        for (int i = 0; i < s.length(); i++){
            char ch = s.charAt(i);
            if (Character.isDigit(ch)){
                number = number*10 + (int)(ch - '0');
            } else if (ch == '+'){
                res += sign * number;
                number = 0;
                sign = 1;
            } else if (ch == '-'){
                res += sign * number;
                number = 0;
                sign = -1;
            } else if (ch == '('){
                st.push(res);
                st.push(sign);
                res = 0;
                sign = 1;
            } else if (ch == ')'){
                res += sign * number;
                number = 0;
                res *= st.pop();
                res += st.pop();
            }
        }
        if (number != 0) res += sign * number;
        
        return res;
    }
}
```

<hr />