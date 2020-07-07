---
title: Leetcode006-zigZagConversion
tags: [String, 2D-list]
mathjax: true
date: 2019-01-22 10:49:47
categories: leetcode
description: Solution Report of LeetCode Acceptted
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows);

## Example

### Example 1

Input: s = "PAYPALISHIRING", numRows = 3

Output: "PAHNAPLSIIGYIR"

### Example 2

Input: s = "PAYPALISHIRING", numRows = 4

Output: "PINALSIGYAHRPI"

Explanation:
```
P     I    N
A   L S  I G
Y A   H R
P     I
```
## Solution

Using 2D-list to store the result of conversion, each list in 2D-list store one row 

Following the rule of zigzag conversion to traverse the input string

```python
class Solution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows == 1:
            return s
        
        a = [[] for i in range(numRows)]
        
        row = 0
        direction = 1
        
        for x in s:
            a[row].append(x)
            if row == numRows-1:
                direction = -1
            elif row == 0:
                direction = 1
            row += direction
            
        result = ''
        for row in a:
            for x in row:
                result += x
        return result
```

<hr />