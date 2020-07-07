---
title: Leetcode451-sortCharacterByFrequency
categories: leetcode
tags: [Hash Table, Heap, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 12:40:27
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string, sort it in decreasing order based on the frequency of characters.

## Example
**Example 1:**
```
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```
**Example 2:**
```
Input:
"cccaaa"

Output:
"cccaaa"

Explanation:
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.
```
**Example 3:**
```
Input:
"Aabb"

Output:
"bbAa"

Explanation:
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```
## Solution

**Note: In Problems which need to use Hash Table to store single letters/digits, using int[] map = new int[128] instead of HashMap could speed up lots of time.**

```java
class Solution {
    public String frequencySort(String s) {
        if (s == null || s.length() <= 1) return s;
        
        int[] map = new int[128];
        PriorityQueue<Character> pq = new PriorityQueue<>(new Comparator<Character>(){
            @Override
            public int compare(Character a, Character b){
                return map[b] - map[a];
            }
        });
        
        for (char ch: s.toCharArray()){
            map[ch]++;
        }
        for (int i = 0; i < 128; i++)
            if (map[i] > 0)
                pq.offer((char)i);

        StringBuilder res = new StringBuilder();
        while (!pq.isEmpty()){
            char tmp = pq.poll();
            for (int i = 0; i < map[tmp]; i++) res.append(tmp);
        }
        return res.toString();
    }
}
```

<hr />