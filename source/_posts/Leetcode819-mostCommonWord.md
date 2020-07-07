---
title: Leetcode819-mostCommonWord
categories: leetcode
tags: [String, Hash Table]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-07 18:32:57
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words.  It is guaranteed there is at least one word that isn't banned, and that the answer is unique.

Words in the list of banned words are given in lowercase, and free of punctuation.  Words in the paragraph are not case sensitive.  The answer is in lowercase.

## Example
```
Input: 
paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
banned = ["hit"]
Output: "ball"
Explanation: 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.
```
**Note:**

* 1 <= paragraph.length <= 1000.
* 0 <= banned.length <= 100.
* 1 <= banned[i].length <= 10.
* The answer is unique, and written in lowercase (even if its occurrences in paragraph may have uppercase symbols, and even if it is a proper noun.)
* paragraph only consists of letters, spaces, or the punctuation symbols !?',;.
* There are no hyphens or hyphenated words.
* Words only consist of letters, never apostrophes or other punctuation symbols.

## Solution
```java
class Solution {
    // public String mostCommonWord(String p, String[] banned) {
    //     Set<String> ban = new HashSet<>(Arrays.asList(banned));
    //     Map<String, Integer> count = new HashMap<>();
    //     String[] words = p.replaceAll("\\W+" , " ").toLowerCase().split("\\s+");
    //     for (String w : words) if (!ban.contains(w)) count.put(w, count.getOrDefault(w, 0) + 1);
    //     return Collections.max(count.entrySet(), Map.Entry.comparingByValue()).getKey();
    // }
    public String mostCommonWord(String paragraph, String[] banned) {
        if (paragraph == null || paragraph.length() == 0) return "";
        
        HashSet<String> set = new HashSet<>();
        for (String st: banned) set.add(st);
        
        HashMap<String, Integer> map = new HashMap<>();
        String p = "";
        for (char c : paragraph.toCharArray()){
            if (Character.isLowerCase(c) || Character.isUpperCase(c)){
                p += c;
            }
            else if (p.length() > 0){
                p = p.toLowerCase();
                map.put(p, map.getOrDefault(p, 0)+1);    
                p = "";
            }
        }
        if (p.length()>0){
            p = p.toLowerCase();
            map.put(p, map.getOrDefault(p, 0)+1);    
        }
        
        int max = -1;
        String res = "";
        
        for (String s: map.keySet()){
            if (max < map.get(s) && !set.contains(s)){
                max = map.get(s);
                res = s;
            }
        }
        
        return res;
    }
}
```

<hr />