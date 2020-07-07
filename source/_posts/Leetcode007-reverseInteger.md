---
title: Leetcode007-reverseInteger
tags: [String, Bloomberg]
mathjax: true
date: 2019-01-22 11:07:44
categories: leetcode
description: Solution Report of LeetCode Acceptted

---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a 32-bit signed integer, reverse digits of an integer.

## Example

### Example 1

Input: 123

Output: 321

### Example 2

Input: -123

Output: -321

### Example 3

Input: 120

Output: 21

### Note

Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## Solution

Easy problem

```java
class Solution {

    public int reverse(int x)
    {
        int result = 0;

        while (x != 0)
        {
            int tail = x % 10;
            int newResult = result * 10 + tail;
            if ((newResult - tail) / 10 != result)
                return 0;
            result = newResult;
            x = x / 10;
        }

        return result;
    }
}
```


### Method 1

convert to string and reverse

```python
class Solution:
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        limit = pow(2,31)
        if x<0:
            x = abs(x)
            result = -int(str(x)[::-1])
        else:
            result = int(str(x)[::-1])
        if result >= (-limit) and result<=(limit-1):
            return result
        else:
            return 0
```

### Method 2

Convert to list and reverse

```python
class Solution:
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        limit = pow(2,31)
        
        l = list(str(x))
        n = len(l)
        
        for i in range(n-1, 0 ,-1):
            if l[i] != '0':
                l = l[:i+1]
                break
                
        if l[0] == '-':
            l = l[:0:-1]
            l.insert(0,'-')
        else:
            l = l[::-1]
        result = int(''.join(l))
        
        
        if result >= (-limit) and result<=(limit-1):
            return result
        else:
            return 0
```

<hr />