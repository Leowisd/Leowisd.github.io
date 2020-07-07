---
title: Leetcode557-reverseWordsInAStringIII
categories: leetcode
tags: [String, Microsoft, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-21 11:20:20
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

## Example
```
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```

**Note:** In the string, each word is separated by single space and there will not be any extra space in the string.

## Solution
```java
class Solution {
    public String reverseWords(String s) {
        if (s == null) return "";
        if (s.length() < 2) return s;
        
        int i = 0;
        int j = 0;
        int id = 0;
        char[] seq = s.toCharArray();
        while (id < s.length()){
            if (seq[id] == ' '){
                j = id -1;
                while(i < j){
                    char tmp = seq[i];
                    seq[i] = seq[j];
                    seq[j] = tmp;
                    i ++;
                    j --;
                }
                i = id + 1;
            }
            id ++;
        }
        j = id -1;
        while(i < j){
            char tmp = seq[i];
            seq[i] = seq[j];
            seq[j] = tmp;
            i ++;
            j --;
        }
        
        
        String res = new String(seq);
        return res;
    }
}
```

<hr />