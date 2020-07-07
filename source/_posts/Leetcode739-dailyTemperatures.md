---
title: Leetcode739-dailyTemperatures
categories: leetcode
tags: [Stack]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-25 16:22:57
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.

For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].

Note: The length of temperatures will be in the range [1, 30000]. Each temperature will be an integer in the range [30, 100].

## Example
```
```

## Solution
```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        int[] res = new int[T.length];
        if (T == null || T.length == 0) return res;
        
        Stack<Integer> st = new Stack<>();
        for (int i = T.length-1; i>=0; i--){
            while (!st.empty() && T[i] >= T[st.peek()]){
                st.pop();
            }
            if (!st.empty() && T[i] < T[st.peek()]) 
                res[i] = st.peek() - i;
            else res[i] = 0;
            st.push(i);
        }
        
        return res;
    }
}
```

<hr />