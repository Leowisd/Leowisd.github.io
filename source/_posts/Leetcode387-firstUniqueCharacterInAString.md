---
title: Leetcode387-firstUniqueCharacterInAString
categories: leetcode
tags: [Hash Table, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-24 22:23:25
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

## Example
```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```

## Solution
```java
class Solution {
    public int firstUniqChar(String s) {
        if (s == null || s.length() == 0) return -1;
        
        HashMap<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < s.length(); i++){
            map.put(s.charAt(i), map.getOrDefault(s.charAt(i), 0) + 1);
        }
        for (int i = 0; i < s.length(); i++){
            if (map.get(s.charAt(i)) == 1) return i;
        }
        return -1;
    }
}
```

Method 2: More faster
```java
class Solution {
    public int firstUniqChar(String s) {
        if (s.length() == 0) return -1;
        
        int[] countRepeats = new int[128];
        for(int i=0; i<s.length(); i++){
            countRepeats[s.charAt(i)]++;
        }
        for(int i=0; i<s.length(); i++){
            if(countRepeats[s.charAt(i)] == 1)
                return i;
        }
        return -1;
    }
}
```

<hr />