---
title: Leetcode020-validParentheses
categories: leetcode
tags: [String, Stack, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-11 12:15:02
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

* Open brackets must be closed by the same type of brackets.
* Open brackets must be closed in the correct order.
* Note that an empty string is also considered valid.

## Example
**Example 1:**
```
Input: "()"
Output: true
```
**Example 2:**
```
Input: "()[]{}"
Output: true
```
**Example 3:**
```
Input: "(]"
Output: false
```
**Example 4:**
```
Input: "([)]"
Output: false
```
**Example 5:**
```
Input: "{[]}"
Output: true
```
## Solution
```java
class Solution {
    public boolean isValid(String s) {
        if(s == null || s.length() == 0) return true;
        Stack<Character> st = new Stack<>();
        for (char ch: s.toCharArray()){
            if (ch == '(' || ch == '[' || ch == '{') st.push(ch);
            else switch (ch){
                case ')':
                    if (st.isEmpty() || st.pop() != '(')
                        return false;
                    break;
                case ']':
                    if (st.isEmpty() || st.pop() != '[')
                        return false;
                    break;
                case '}':
                    if (st.isEmpty() || st.pop() != '{')
                        return false;
                    break;
            }
        }
        if (!st.isEmpty()) return false;
        return true;
    }
}
```

<hr />