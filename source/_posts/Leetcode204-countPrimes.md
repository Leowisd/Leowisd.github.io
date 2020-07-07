---
title: Leetcode204-countPrimes
categories: leetcode
tags: [Math, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-14 10:53:08
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Count the number of prime numbers less than a non-negative number, n.

## Example
```
Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

## Solution
```java
class Solution {
    public int countPrimes(int n) {
        boolean[] notPrimes = new boolean[n];
        int res =0;
        for (int i = 2; i < n; i++){
            if (notPrimes[i] == false){
                res ++;
                for (int j = 2; i * j < n; j++) notPrimes[i * j] = true; 
            }
        }
        return res;
    }
}
```

<hr />