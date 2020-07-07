---
title: Leetcode186-reverseWordsinaStringII
categories: leetcode
tags: [String, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-22 17:02:52
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an input string , reverse the string word by word. 

## Example
```
Input:  ["t","h","e"," ","s","k","y"," ","i","s"," ","b","l","u","e"]
Output: ["b","l","u","e"," ","i","s"," ","s","k","y"," ","t","h","e"]
```
**Note: **

* A word is defined as a sequence of non-space characters.
* The input string does not contain leading or trailing spaces.
* The words are always separated by a single space.
* Follow up: Could you do it in-place without allocating extra space?

## Solution
```java
class Solution {
    public void reverseWords(char[] s) {
        if (s.length == 0) return;
        
        swap(s, 0, s.length - 1);
        
        int start = 0;
        int end = 0;
        while(end < s.length){
            if (s[end] == ' '){
                swap(s, start, end - 1);
                start = end + 1;
            }
            end++;
        }
        swap(s, start, end - 1);
    }
    
    private void swap(char[] s, int i, int j){
        while (i < j){
            char tmp = s[i];
            s[i] = s[j];
            s[j] = tmp;
            i++;
            j--;
        }
    }
}
```

<hr />