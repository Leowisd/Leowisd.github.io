---
title: Leetcode1153-stringTransformsIntoAnotherString
categories: leetcode
tags: [Hash Table, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 15:51:35
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two strings str1 and str2 of the same length, determine whether you can transform str1 into str2 by doing zero or more conversions.

In one conversion you can convert all occurrences of one character in str1 to any other lowercase English character.

Return true if and only if you can transform str1 into str2.

## Example
**Example 1:**
```
Input: str1 = "aabcc", str2 = "ccdee"
Output: true
Explanation: Convert 'c' to 'e' then 'b' to 'd' then 'a' to 'c'. Note that the order of conversions matter.
```
**Example 2:**
```
Input: str1 = "leetcode", str2 = "codeleet"
Output: false
Explanation: There is no way to transform str1 to str2.
```
**Note:**

1. 1 <= str1.length == str2.length <= 10^4
2. Both str1 and str2 contain only lowercase English letters.

## Solution
此题的对应有以下几个关系:
1. 一对一，每一个char互相对应转换即可 a->b
2. 多对一， aabcc,ccdee, a->c, c->e，其实只要有未在target string出现过的char，那么就可以拿来作为temp char桥梁，比如 a->g->c这样转换就不会同时影响c->e的转换
3. 一对多，a->f, a->g 这样是绝对不可能的，因为char会被同时影响
        
另外还有一种特殊情况就是，source和target的unique char的数量是一样的时候，如果此时是26个
则说明完全不能转换，因为没有extra的temp char作为转换的桥梁
```java
//  there should at least one character that is unused, to use it as the tmp for transformation.
class Solution {
    public boolean canConvert(String str1, String str2) {
        if (str1.equals(str2)) return true;
        HashMap<Character, Character> map = new HashMap<>();
        for (int i = 0; i < str1.length(); i++){
            if (map.getOrDefault(str1.charAt(i), str2.charAt(i)) != str2.charAt(i))
                return false;
            map.put(str1.charAt(i), str2.charAt(i));
        }
        return new HashSet<>(map.values()).size() < 26;
    }
}
```

<hr />