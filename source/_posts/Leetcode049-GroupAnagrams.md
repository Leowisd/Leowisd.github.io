---
title: Leetcode049-GroupAnagrams
categories: leetcode
tags: [Hash Table, String, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-06 12:11:48
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given an array of strings, group anagrams together.

## Example
```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```
Note:
* All inputs will be in lowercase.
* The order of your output does not matter.

## Solution
O(N*KlogK)
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> res = new ArrayList<>();
        if (strs == null || strs.length == 0) return res;
        
        HashMap<String, List<String>> map = new HashMap<>();        
        for (String st: strs){
            char[] chs = st.toCharArray();           
           
            String key = "";
            Arrays.sort(chs);
            key = String.valueOf(chs);
            
            if (map.containsKey(key)){
                List<String> tmp = new ArrayList<>(map.get(key));
                tmp.add(st);
                map.put(key, tmp);
            }
            else{
                List<String> tmp = new ArrayList<>();
                tmp.add(st);
                map.put(key, tmp);
            }  
        }
        return new ArrayList<List<String>>(map.values());
    }
}
```
O(N*K)
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();
        
        for (String str : strs) {
            String encoded = encode(str);
            if (map.containsKey(encoded))
                map.get(encoded).add(str);
            else {
                List<String> list = new LinkedList<>();
                list.add(str);
                map.put(encoded, list);
            }
        }
        
        return new ArrayList<List<String>>(map.values());
    }
    
    private String encode(String str) {
        int[] freq = new int[26];
        String spliter = "-";
        
        for (int i = 0; i < str.length(); i++)
            freq[str.charAt(i) - 'a']++;
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < freq.length; i++)
            sb.append(freq[i]).append(spliter);
        
        return sb.toString();
    }
}
```

<hr />