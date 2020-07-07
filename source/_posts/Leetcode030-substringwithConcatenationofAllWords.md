---
title: Leetcode030-substringwithConcatenationofAllWords
categories: leetcode
tags: [Hash Table, Sliding Window, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-22 15:21:38
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

You are given a string, s, and a list of words, words, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.

## Example
**Example 1:**
```
Input:
  s = "barfoothefoobarman",
  words = ["foo","bar"]
Output: [0,9]
Explanation: Substrings starting at index 0 and 9 are "barfoo" and "foobar" respectively.
The output order does not matter, returning [9,0] is fine too.
```
**Example 2:**
```
Input:
  s = "wordgoodgoodgoodbestword",
  words = ["word","good","best","word"]
Output: []
```

## Solution
Two HashMaps to judge
```java
public class Solution {
    // Sliding Window    360ms
    // ask interviewer if words is empty, should I return empty list
    public List<Integer> findSubstring(String S, String[] L) {
        List<Integer> res = new LinkedList<>();
        if (L.length == 0 || S.length() < L.length * L[0].length())   return res;
        int N = S.length(), M = L.length, K = L[0].length();
        Map<String, Integer> map = new HashMap<>(), curMap = new HashMap<>();
        for (String s : L) {
            if (map.containsKey(s))   map.put(s, map.get(s) + 1);
            else                      map.put(s, 1);
        }
        String str = null, tmp = null;
        for (int i = 0; i < K; i++) {
            int count = 0;  // remark: reset count 
            for (int l = i, r = i; r + K <= N; r += K) {
                str = S.substring(r, r + K);
                if (map.containsKey(str)) {
                    if (curMap.containsKey(str))   curMap.put(str, curMap.get(str) + 1);
                    else                           curMap.put(str, 1);
                    
                    if (curMap.get(str) <= map.get(str))    count++;
                    while (curMap.get(str) > map.get(str)) {
                        tmp = S.substring(l, l + K);
                        curMap.put(tmp, curMap.get(tmp) - 1);
                        l += K;
                        if (curMap.get(tmp) < map.get(tmp)) count--;
                    }
                    if (count == M) {
                        res.add(l);
                        tmp = S.substring(l, l + K);
                        curMap.put(tmp, curMap.get(tmp) - 1);
                        l += K;
                        count--;
                    }
                }else {
                    curMap.clear();
                    count = 0;
                    l = r + K;
                }
            }
            curMap.clear();
        }
        return res;
    }
}
```
One HashMap and over time limit
```java
// class Solution {
    
//     public List<Integer> findSubstring(String s, String[] words) {
//         HashSet<Integer> res = new HashSet<>();
//         if (words.length == 0) return new ArrayList<Integer>(0);
        
//         HashMap<String, Integer> dic = new HashMap<>();
//         for (String word: words) dic.put(word, dic.getOrDefault(word, 0) + 1);
//         int len = words[0].length();
//         if (s.length() < words.length * len) return new ArrayList<Integer>(0);
        
//         int id = 0;
//         int index = 0;
//         int start = 0;
//         int count = 0;
//         while(id < s.length() - words.length * len + 1){
//             if ((index+1-id)%len == 0){
//                 if (index - start + 1 > words.length * len){
//                     String first = s.substring(start, start + len);
//                     dic.put(first, dic.get(first) + 1);
//                     count--;
//                     start = start + len;
//                 }
                
//                 String cur = s.substring(index - len + 1, index + 1);
//                 if (!dic.containsKey(cur)){
//                     for (int i = 0; i < count; i++){
//                         String pre = s.substring(start, start + len);
//                         dic.put(pre, dic.get(pre) + 1);
//                         start += len;
//                     }
//                     count = 0;
//                     id ++;
//                     start = id;
//                     index = id;
//                 }
//                 else if (dic.containsKey(cur) && dic.get(cur) > 0){
//                     count++;
//                     dic.put(cur, dic.get(cur)-1);
//                     if (count == words.length) res.add(start);
//                 }
//                 else{
//                     int countCopy = count;
//                     for (int i = 0; i < count; i++){
//                         String pre = s.substring(start, start + len);
//                         dic.put(pre, dic.get(pre) + 1);
//                         start += len;
//                         countCopy--;
//                         if (dic.get(cur) > 0) break;
//                     }
//                     count = countCopy;
//                     if (dic.get(cur) > 0) continue;
//                     start += len;
//                 }
//             }
//             index++;
//             if (index >= s.length()){
//                 for (int i = 0; i < count; i++){
//                     String pre = s.substring(start, start + len);
//                     dic.put(pre, dic.get(pre) + 1);
//                     start += len;
//                 }
//                 count = 0;
//                 id ++;
//                 start = id;
//                 index = id;
//             }
//         }
//         return new ArrayList<Integer>(res);
//     }
// }
```

<hr />