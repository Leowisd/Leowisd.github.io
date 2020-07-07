---
title: Leetcode202-happyNumber
categories: leetcode
tags: [Hash Table, Math, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-20 16:37:55
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.
## Example
```
Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

## Solution
```java
class Solution {
    public boolean isHappy(int n) {
        if (n == 0) return false;
        if (n == 1) return true;
        HashSet<Integer> set = new HashSet<>();
        set.add(n);
        while(n != 1){
            int sum = 0;
            while(n != 0){
                sum += Math.pow((n % 10), 2);
                n /= 10;
            }
            if (set.contains(sum)) return false;
            set.add(sum);
            n = sum;
        }
        return true;
    }
}
```

<hr />