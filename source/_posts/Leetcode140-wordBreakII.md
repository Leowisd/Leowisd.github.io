---
title: Leetcode140-wordBreakII
categories: leetcode
tags: [DFS, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-09 10:42:51
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences.

**Note:**

* The same word in the dictionary may be reused multiple times in the segmentation.
* You may assume the dictionary does not contain duplicate words.

## Example
**Example 1:**
```
Input:
s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]
Output:
[
  "cats and dog",
  "cat sand dog"
]
```
**Example 2:**
```
Input:
s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
Output:
[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]
Explanation: Note that you are allowed to reuse a dictionary word.
```
**Example 3:**
```
Input:
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]
Output:
[]
```
## Solution
**Solution 1**

DFS function returns an array including all substrings derived from s

```java
class Solution{
    // DFS solution3: store useful substring
    public List<String> wordBreak(String s, List<String> wordDict) {
        HashSet<String> dic = new HashSet<>();
        for (String word: wordDict) dic.add(word);
        return DFS(s, dic, new HashMap<String, LinkedList<String>>());
    }       

    private List<String> DFS(String s, Set<String> wordDict, HashMap<String, LinkedList<String>>map) {
        if (map.containsKey(s)) 
            return map.get(s);
        
        LinkedList<String>res = new LinkedList<String>();     
        if (s.length() == 0) {
            res.add("");
            return res;
        }               
        for (String word : wordDict) {
            if (s.startsWith(word)) {
                List<String>sublist = DFS(s.substring(word.length()), wordDict, map);
                for (String sub : sublist) 
                    res.add(word + (sub.isEmpty() ? "" : " ") + sub);               
            }
        }       
        map.put(s, res);
        return res;
    }
}
```

**Solution 2: not the fastest**

```java
class Solution {
    // DFS solution : store unable substring
    boolean isSuccess = false;
    public List<String> wordBreak(String s, List<String> wordDict) {
        List<String> res = new ArrayList<>();
        if (s == null || s.length() == 0) return res;

        HashSet<String> dic = new HashSet<>();
        for (String word: wordDict) dic.add(word);
        
        HashSet<String> noWay = new HashSet<>();
        String seq = "";
        dfs(s, dic, noWay, seq, res);
        
        return res;
    }
    
    private void dfs(String s, HashSet<String> dic, HashSet<String> noWay, String seq, List<String> res){
        if (s == null || s.length() == 0){
            if (seq != null || seq.length() != 0){
                res.add(seq.trim());
                isSuccess = true;
            }
            return;
        }
        for (int i = 1; i <= s.length(); i++){
            String first = s. substring(0, i);
            String last = s.substring(i);
            if (dic.contains(first) && !noWay.contains(last)){
                String tmp = seq;
                seq += first + " ";
                dfs(last, dic, noWay, seq, res);
                if (!isSuccess) noWay.add(last);
                seq = tmp;
                if (seq.length() == 0 && isSuccess == true) isSuccess = false;  
            }
        }
    }
}
```

<hr />