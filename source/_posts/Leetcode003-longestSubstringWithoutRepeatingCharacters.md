---
title: Leetcode003-longestSubstringWithoutRepeatingCharacters
tags: [Hash Table, Two Pointers, Amazon, Bloomberg, TikTok]
mathjax: true
date: 2019-01-08 11:59:18
categories: leetcode
description: Solution Report of LeetCode Acceptted
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string, find the length of the longest substring without repeating characters.

## Example

### Example 1

Input: "abcabcbb"

Output: 3 

Explanation: The answer is "abc", with the length of 3. 

### Example 2

Input: "bbbbb"

Output: 1

Explanation: The answer is "b", with the length of 1.

### Example 3

Input: "pwwkew"

Output: 3

Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

## Solution

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) return 0;
        
        HashMap<Character, Integer> map = new HashMap<>();
        int left = 0;
        int right = 0;
        int res = 0;
        while(right < s.length()){
            if (map.containsKey(s.charAt(right))){
                left = Math.max(left, map.get(s.charAt(right)) + 1);
            }
            map.put(s.charAt(right), right);
            res = Math.max(res, right - left + 1);
            right++;
        }
        return res;
    }
}
```

### Solution 1

First set the first element as the current longest substring

For the rest part of the input string, check if each element is in the substring

If not, plus one to current temp length value

If yes, reset the current longest substring from the index where the element occurs last time and reset the temp length value

Each time, comparing the current temp length with the final length 

```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        if len(s) == 0:
            return 0
        if len(s) == 1:
            return 1
        num = len(s)
        sub = ""+s[0]
        temp = 1
        count = 1
        f = 0
        for i in range(1,len(s)):
            if sub.find(s[i]) == -1:
                sub += s[i]
                temp += 1
            else:
                f = sub.find(s[i])+1
                sub = sub[f::]+s[i]
                temp = temp - f + 1
            if temp>count:
                count = temp
        return count
```

### Solution 2

Using a list to record where each letter occurs, -1 for each one for initialization.

Using a value First to record the begining of current longest substring, -1 as initialization.

Looping the string, if the index where the element occurs bigger than the value First, meaning that the element has occurs in current substring, then renew the First and store the element's current index. Renew the count of length at last

```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        if len(s) == 0:
            return 0
        if len(s) == 1:
            return 1
        a = [-1] * 256
        count = 0
        first = -1
        for i in range(len(s)):
            if a[ord(s[i])] > first:
                first = a[ord(s[i])]
            a[ord(s[i])] = i
            count = max(count, (i-first))
        return count
```
<hr />