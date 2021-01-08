---
title: Leetcode032-Longest Valid Parentheses
categories: leetcode
tags: [Stack, DP, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-08 01:14:29
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

## Example

**Example 1:**
```
Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".
```
**Example 2:**
```
Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".
```
**Example 3:**
```
Input: s = ""
Output: 0
```

**Constraints:**

* 0 <= s.length <= 3 * 104
* s[i] is '(', or ')'.

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

### Solution 1: Stack

```java
class Solution {
    public int longestValidParentheses(String s) {
        if (s.length() < 2) return 0;
        Stack<Integer> st = new Stack<>();
        int res = 0;
        for (int i = 0; i < s.length(); i++){
            if (s.charAt(i) == '('){
                st.push(i);
            }
            else{
                if (st.isEmpty()){
                    st.push(i);
                }
                else {
                    if (s.charAt(st.peek()) == '('){
                        st.pop();
                        res = Math.max(res, i - (st.isEmpty() ? -1 : st.peek()));
                    }
                    else{
                        st.push(i);
                    }
                }
            }
        }
        return res;
    }
}
```

### Solution 2: DP
```
If s[i] is '(', set dp[i] to 0,because any string end with '(' cannot be a valid one.

Else if s[i] is ')'

     If s[i-1] is '(', dp[i] = dp[i-2] + 2

     Else if s[i-1] is ')' and s[i-dp[i-1]-1] == '(', dp[i] = dp[i-1] + 2 + dp[i-dp[i-1]-2]
```
```java
class Solution {
    public int longestValidParentheses(String s) {
        if (s.length() < 2) return 0;
        int res = 0;
        int[] dp = new int[s.length()];
        for (int i = 1; i < s.length(); i++){
            if (s.charAt(i) == ')'){
                if (s.charAt(i - 1) == '('){
                    dp[i] = (i - 2) >= 0 ? dp[i - 2] + 2 : 2;
                }
                else{// if s[i-1] == ')', combine the previous length.
                    if (i - dp[i - 1] - 1 >= 0 && s.charAt(i - dp[i - 1] - 1) == '('){
                        dp[i] = dp[i - 1] + 2 + (i - dp[i - 1] - 2 >= 0 ? dp[i - dp[i - 1] - 2] : 0);
                    }
                }
                res = Math.max(res, dp[i]);
            }
            //else if s[i] == '(', skip it, because longest[i] must be 0
        }
        return res;
    }
}
```

<hr />