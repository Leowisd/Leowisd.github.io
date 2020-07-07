---
title: Leetcode009-palindromeNumber
tags: [String, Bloomberg]
mathjax: true
date: 2019-01-22 21:42:58
categories: leetcode
description: Solution Report of LeetCode Acceptted
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

## Example

### Example 1

Input: 121

Output: true

### Example 2

Input: -121

Output: false

Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

### Example 3

Input: 10

Output: false

Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

## Solution


```java
public boolean isPalindrome(int x) {
    if (x<0 || (x!=0 && x%10==0)) return false;
    int rev = 0;
    while (x > rev){
    	rev = rev*10 + x%10;
    	x = x/10;
    }
    return (x==rev || x==rev/10);
}
```

### Solution 1

Convert to string

```python
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        s = str(x)
        s1 = s[::-1]
        
        if s==s1:
            return True
        else:
            return False
```

### Solution 2

Don't convert, using / and %

```python
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x<0:
            return False
        
        tmp = x
        result = 0

        while tmp>0:
            result = result*10 + tmp%10
            tmp = tmp //10

        return x == result
```

<hr />