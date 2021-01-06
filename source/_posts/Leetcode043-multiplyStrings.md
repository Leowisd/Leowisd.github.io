---
title: Leetcode043-Multiply Strings
categories: leetcode
tags: [String, Math, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-05 23:11:36
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2, also represented as a string.

Note: You must not use any built-in BigInteger library or convert the inputs to integer directly.

## Example

**Example 1:**
```
Input: num1 = "2", num2 = "3"
Output: "6"
```
**Example 2:**
```
Input: num1 = "123", num2 = "456"
Output: "56088"
```
**Constraints:**

* 1 <= num1.length, num2.length <= 200
* num1 and num2 consist of digits only.
* Both num1 and num2 do not contain any leading zero, except the number 0 itself.
* 
## Solution

* Time Complexity: $$O(MN)$$
* Space Complexity: $$O(M + N)$$

```java
class Solution {
    public String multiply(String num1, String num2) {
        if (num1.equals("0") || num2.equals("0")) return "0";
        
        int[] product = new int[num1.length() + num2.length()];
        for (int i = num1.length() - 1; i >= 0; i--){
            for (int j = num2.length() - 1; j >= 0; j--){
                int a = num1.charAt(i) - '0';
                int b = num2.charAt(j) - '0';
                product[i + j + 1] += a * b;
            }
        }
        
        int carry = 0;
        for (int i = product.length - 1; i >= 0; i--){
            int temp = (product[i] + carry) % 10;
            carry = (product[i] + carry) / 10;
            product[i] = temp;
        }
        
        StringBuilder res = new StringBuilder();
        for (int num: product)
            res.append(num);
        while(res.length() > 0 && res.charAt(0) == '0') res.deleteCharAt(0);
        
        return res.length() == 0 ? "0" : res.toString();
    }
}
```

<hr />