---
title: Leetcode1047-removeAllAdjacentDuplicatesInString
categories: leetcode
tags: [Stack, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 10:55:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string S of lowercase letters, a duplicate removal consists of choosing two adjacent and equal letters, and removing them.

We repeatedly make duplicate removals on S until we no longer can.

Return the final string after all such duplicate removals have been made.  It is guaranteed the answer is unique.

## Example
```
Input: "abbaca"
Output: "ca"
Explanation: 
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".
```

**Note:**

* 1 <= S.length <= 20000
* S consists only of English lowercase letters.

## Solution
**Solution 1: Basic method, used Stack, O(N), 24ms**
```java
class Solution {
//     Used Stack, with reverse(), O(N), 24ms
    public String removeDuplicates(String S) {
        if (S == null || S.length() == 0) return S;
        
        Stack<Character> st = new Stack<>();
        for (char ch : S.toCharArray()){
            if (!st.isEmpty() && st.peek() == ch)
                st.pop();
            else 
                st.push(ch);
        }
        StringBuilder res = new StringBuilder();
        while(!st.isEmpty())
            res.append(st.pop());
        return res.reverse().toString();
    }
}
```

**Solution 2: Improved, used Deque, O(N), 11ms**
```java
class Solution {
//     Used Deque, O(N), 11ms
    public String removeDuplicates(String S) {
        Deque<Character> dq = new ArrayDeque<>();
        for (char c : S.toCharArray()) {
            if (!dq.isEmpty() && dq.peekLast() == c) { 
                dq.pollLast();
            }else {
                dq.offer(c);
            }
        }
        StringBuilder sb = new StringBuilder();
        for (char c : dq) { sb.append(c); }
        return sb.toString();
    }
}
```

**Solution 3: The actual most fastest. Two pointers. O(N), 3ms**
```java
class Solution {
//     Two pointers, O(N), 3ms
    public String removeDuplicates(String s) {
        int i = 0, n = s.length();
        char[] res = s.toCharArray();
        for (int j = 0; j < n; j++, i++) {
            res[i] = res[j];
            if (i > 0 && res[i - 1] == res[i]) // count = 2
                i -= 2;
        }
        return new String(res, 0, i);
    }
}
```
<hr />