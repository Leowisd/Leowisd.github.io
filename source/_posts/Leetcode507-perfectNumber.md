---
title: Leetcode507-perfectNumber
categories: leetcode
tags: [Math, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-13 16:56:27
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

We define the Perfect Number is a positive integer that is equal to the sum of all its positive divisors except itself.

Now, given an integer n, write a function that returns true when it is a perfect number and false when it is not.

## Example
```
Input: 28
Output: True
Explanation: 28 = 1 + 2 + 4 + 7 + 14
```
**Note:** The input number n will not exceed 100,000,000. (1e8)

## Solution
```java
class Solution {
    public boolean checkPerfectNumber(int num) {
        if (num == 1) return false;
        
        int sum = 1;
        for (int i=2;i<= Math.sqrt(num);i++){
            if (num % i == 0)
                sum += i + num/i;
        }
        
        return (sum == num);
    }
}
```

<hr />