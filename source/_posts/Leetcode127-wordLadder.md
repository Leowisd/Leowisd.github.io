---
title: Leetcode127-wordLadder
categories: leetcode
tags: [BFS, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-09 11:11:09
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

Only one letter can be changed at a time.
Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

**Note:**
* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume beginWord and endWord are non-empty and are not the same.

## Example
**Example 1:**
```
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```
**Example 2:**
```
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```
## Solution
```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        HashSet<String> dic = new HashSet<>();
        for (String word: wordList) dic.add(word);
        if (!dic.contains(endWord)) return 0;
        int res = 1;
        HashSet<String> reachable = new HashSet<>();
        reachable.add(beginWord);
        while(!reachable.contains(endWord)){
            HashSet<String> toAdd = new HashSet<>();
            for (String word: reachable){
                for (int i = 0; i < word.length(); i++){
                    char[] arr = word.toCharArray();
                    for (char ch = 'a'; ch <= 'z'; ch++){
                        arr[i] = ch;
                        String tmp = new String(arr);
                        if (dic.contains(tmp)){
                            toAdd.add(tmp);
                            dic.remove(tmp);
                        }
                    }
                }
            }
            if (toAdd.isEmpty()) return 0;
            reachable = toAdd;
            res ++;
        }
        
        return res;
    }
}
```

<hr />