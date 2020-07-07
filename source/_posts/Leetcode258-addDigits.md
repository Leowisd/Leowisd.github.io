---
title: Leetcode258-addDigits
categories: leetcode
tags: [Math]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-12 22:37:32
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

## Example
```
Input: 38
Output: 2 
Explanation: The process is like: 3 + 8 = 11, 1 + 1 = 2. 
             Since 2 has only one digit, return it.
```
**Follow up:**
Could you do it without any loop/recursion in O(1) runtime?

## Solution
```java
class Solution {
    public int addDigits(int num) {
        while (num >= 10){
            int temp = 0;
            while (num / 10 > 0){
                temp += num%10;
                num /= 10;
            }
            num += temp;
        }
        return num;
        
        //Follow up:
        //return num == 0 ? 0 : (num % 9 == 0 ? 9 : (num % 9));
    }
}
```

<hr />