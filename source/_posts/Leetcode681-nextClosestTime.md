---
title: Leetcode681-Next Closest Time
categories: leetcode
tags: [String, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-04 23:11:00
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a time represented in the format "HH:MM", form the next closest time by reusing the current digits. There is no limit on how many times a digit can be reused.

You may assume the given input string is always valid. For example, "01:34", "12:09" are all valid. "1:34", "12:9" are all invalid.

## Example

**Example 1:**
```
Input: time = "19:34"
Output: "19:39"
Explanation: The next closest time choosing from digits 1, 9, 3, 4, is 19:39, which occurs 5 minutes later.
It is not 19:33, because this occurs 23 hours and 59 minutes later.
```
**Example 2:**
```
Input: time = "23:59"
Output: "22:22"
Explanation: The next closest time choosing from digits 2, 3, 5, 9, is 22:22.
It may be assumed that the returned time is next day's time since it is smaller than the input time numerically.
```

**Constraints:**

* time.length == 5
* time is a valid time in the form "HH:MM".
* 0 <= HH < 24
* 0 <= MM < 60

## Solution

* Time Complexity: $$O(1)$$
* Space Complexity: $$O(1)$$

```java
class Solution {
    public String nextClosestTime(String time) {
        char[] timeArr = time.toCharArray();
        Character[] digits = {timeArr[0], timeArr[1], timeArr[3], timeArr[4]};
        TreeSet<Character> set = new TreeSet<>(Arrays.asList(digits));
        
        timeArr[4] = findNext(set, timeArr[4], '9');
        if (timeArr[4] > time.charAt(4)) return new String(timeArr);
        
        timeArr[3] = findNext(set, timeArr[3], '5');
        if (timeArr[3] > time.charAt(3)) return new String(timeArr);
        
        timeArr[1] = findNext(set, timeArr[1], timeArr[0] == '2' ? '3' : '9');
        if (timeArr[1] > time.charAt(1)) return new String(timeArr);
        
        timeArr[0] = findNext(set, timeArr[0], '2');
        return new String(timeArr);
    }
    
    private char findNext(TreeSet<Character> set, char current, char upperLimit){
        Character next = set.higher(current);
        return next == null || next > upperLimit ? set.first() :next;
    }
}
```

<hr />