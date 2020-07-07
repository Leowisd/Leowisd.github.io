---
title: Leetcode1249-minimumRemoveToMakeValidParentheses
categories: leetcode
tags: [Stack, String, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 15:13:41
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string s of '(' , ')' and lowercase English characters. 

Your task is to remove the minimum number of parentheses ( '(' or ')', in any positions ) so that the resulting parentheses string is valid and return any valid string.

Formally, a parentheses string is valid if and only if:

* It is the empty string, contains only lowercase characters, or
* It can be written as AB (A concatenated with B), where A and B are valid strings, or
* It can be written as (A), where A is a valid string.

## Example
**Example 1:**
```
Input: s = "lee(t(c)o)de)"
Output: "lee(t(c)o)de"
Explanation: "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.
```
**Example 2:**
```
Input: s = "a)b(c)d"
Output: "ab(c)d"
```
**Example 3:**
```
Input: s = "))(("
Output: ""
Explanation: An empty string is also valid.
```
**Example 4:**
```
Input: s = "(a(b(c)d)"
Output: "a(b(c)d)"
```

**Constraints:**

* 1 <= s.length <= 10^5
* s[i] is one of  '(' , ')' and lowercase English letters.

## Solution
```java
class Solution {
    class Pair{
        public char ch;
        public int idx;
        public Pair(char ch, int idx){
            this.ch = ch;
            this.idx = idx;
        }
    }
    public String minRemoveToMakeValid(String s) {
        StringBuilder sb = new StringBuilder(s);
        Stack<Integer> st = new Stack();
        for (int i = 0; i < sb.length(); ++i) {
            if (sb.charAt(i) == '(') st.add(i + 1);
            if (sb.charAt(i) == ')') {
            if (!st.empty() && st.peek() >= 0) st.pop();
            else st.add(-(i + 1));
            }
        }
        while (!st.empty())
            sb.deleteCharAt(Math.abs(st.pop()) - 1);
        return sb.toString();
    }
}
```

<hr />