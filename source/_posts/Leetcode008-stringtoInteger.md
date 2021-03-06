---
title: Leetcode008-stringtoInteger
tags: [String, Bloomberg]
mathjax: true
date: 2019-01-22 21:19:12
categories: leetcode
description: Solution Report of LeetCode Acceptted
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Implement atoi which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

### Note

* Only the space character ' ' is considered as whitespace character.
* Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (2^31 − 1) or INT_MIN (−2^31) is returned.

## Example

### Example 1

Input: "42"

Output: 42

### Example 2

Input: "   -42"

Output: -42

Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.

### Example 3

Input: "4193 with words"

Output: 4193

Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.

### Example 4

Input: "words and 987"

Output: 0

Explanation: The first non-whitespace character is 'w', which is not a numerical digit or a +/- sign. Therefore no valid conversion could be performed.

### Example 5

Input: "-91283472332"

Output: -2147483648

Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.

## Solution

```java
class Solution {
    public int myAtoi(String str) {
         int index = 0, sign = 1, total = 0;
        //1. Empty string
        str = str.trim();
        if(str.length() == 0) return 0;

        //2. Remove Spaces
        while(index < str.length() && str.charAt(index) == ' ')
            index ++;

        //3. Handle signs
        if(str.charAt(index) == '+' || str.charAt(index) == '-'){
            sign = str.charAt(index) == '+' ? 1 : -1;
            index ++;
        }  
    
        //4. Convert number and avoid overflow
        while(index < str.length()){
            int digit = str.charAt(index) - '0';
            if(digit < 0 || digit > 9) break;

            //check if total will be overflow after 10 times and add digit
            if(Integer.MAX_VALUE/10 < total || Integer.MAX_VALUE/10 == total && Integer.MAX_VALUE %10 < digit)
                return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;

            total = 10 * total + digit;
            index ++;
        }
        return total * sign;
    }
}
```

Delete begining spaces

Considering empty string and the string containing only whitespace characters

Considering +/-, +-/-+/++-/....

```python
class Solution:
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        limit = pow(2, 31)
        result = ''
        noWhite = 0
        minus = 0
        
        if len(str) == 0:
            return 0
        
        while str[0] == ' ':
            str = str[1:]
            if str =='':
                return 0
            
        if (str[0] >= '0' and str[0]<='9'):
            sign = 1
        elif (str[0] == '+'):
            str = str[1:]
            sign = 1
        elif (str[0] == '-'):
            str = str[1:]
            sign = -1
        else:
            return 0
        
        result = 0
        for x in str:
            if x >= '0' and x <='9':
                result = result*10 + ord(x) - 48
            else:
                break
        
        result *= sign
        if (result > limit-1):
            return limit-1
        elif (result < -limit):
            return -limit
        else:
            return result
```

**Note:** odd() and chr()

<hr />