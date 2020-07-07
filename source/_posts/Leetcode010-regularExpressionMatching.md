---
title: Leetcode010-regularExpressionMatching
tags: [String]
mathjax: true
date: 2019-01-23 10:08:58
categories: leetcode
description: Solution Report of LeetCode Acceptted
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.
```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```
The matching should cover the entire input string (not partial).

### Note

* s could be empty and contains only lowercase letters a-z.
* p could be empty and contains only lowercase letters a-z, and characters like . or *.

## Example

### Example 1

```
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

### Example 2

```
Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the precedeng element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

### Example 3

```
Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

### Example 4

```
Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".
```

### Example 5

```
Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```

## Solution

Using DFS

Considering s ='' or p=''

Considering if there is a '*'

```python
class Solution:
    def isEndOfStar(self, p):
        while p!='':
            if len(p) ==1 or (len(p)>1 and p[1]!='*'):
                return False
            p = p[2:]
        return True
    
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        if p =='':
            return s == ''
        
        if s =='':
            return self.isEndOfStar(p)
        
        if len(p) == 1 or (len(p) > 1 and p[1]!='*'):
#       without *
            if s[0]!=p[0] and p[0] !='.':
                return False
            else:
                return self.isMatch(s[1:],p[1:])
        else:
#       with *
            if self.isMatch(s, p[2:]):
                return True
            while s[0] == p[0] or p[0] == '.':
                s = s[1:]
                
                if self.isMatch(s, p[2:]):
                    return True
                if s =='':
                    return self.isEndOfStar(p)
            return False
        

```

<hr />