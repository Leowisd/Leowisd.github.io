---
title: Leetcode394-decodeString
categories: leetcode
tags: [Stack, Recursion, Bloomberg, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-01 23:49:27
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given an encoded string, return its decoded string.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or 2[4].

## Example
```
s = "3[a]2[bc]", return "aaabcbc".
s = "3[a2[c]]", return "accaccacc".
s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
```

## Solution

**Solution 1: Stack**
```java
class Solution {
    // Used Stack. 
    public String decodeString(String s) {
        if (s == null || s.length() == 0) return s;
        
        String res = "";
        Stack<Integer> count = new Stack<>();
        Stack<String> resSt = new Stack<>();
        int idx = 0;
        while(idx < s.length()){
            if (Character.isDigit(s.charAt(idx))){
                int c = 0;
                while(Character.isDigit(s.charAt(idx))){
                    c = c * 10 + s.charAt(idx) - 48;
                    idx++;
                }
                count.push(c);
            }
            else if (s.charAt(idx) == '['){
                resSt.push(res);
                res = "";
                idx++;
            }
            else if (s.charAt(idx) == ']'){
                StringBuilder temp = new StringBuilder(resSt.pop());
                int times = count.pop();
                for (int i = 0; i < times; i++)
                    temp.append(res);
                res = temp.toString();
                idx++;
            }
            else res += s.charAt(idx++);
        }
        return res;
    }
}
```

**Solution 2: Recursion with queue**
```java
class Solution {
//     Used recursion with Queue
    public String decodeString(String s) {
        if (s == null || s.length() == 0) return s;
        
        Queue<Character> q = new LinkedList<>();
        for (char ch: s.toCharArray()){
            q.offer(ch);
        }
        return helper(q);
    }
    private String helper(Queue<Character> queue){
        StringBuilder res = new StringBuilder();
        int num = 0;
        while (!queue.isEmpty()){
            char ch = queue.poll();
            if (Character.isDigit(ch)){
                num = num * 10 + ch - 48;
            }
            else if (ch == '['){
                String temp = helper(queue);
                for (int i = 0; i < num; i++)
                    res.append(temp);
                num = 0;
            }
            else if (ch == ']')
                break;
            else 
                res.append(ch);
        }
        return res.toString();
    }
}
```
<hr />