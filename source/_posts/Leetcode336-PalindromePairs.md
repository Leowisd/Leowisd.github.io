---
title: Leetcode336-PalindromePairs
categories: leetcode
tags: [Hash Table, String, Trie, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-11 12:03:17
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a list of unique words, find all pairs of distinct indices (i, j) in the given list, so that the concatenation of the two words, i.e. words[i] + words[j] is a palindrome.

## Example
**Example 1:**
```
Input: ["abcd","dcba","lls","s","sssll"]
Output: [[0,1],[1,0],[3,2],[2,4]] 
Explanation: The palindromes are ["dcbaabcd","abcddcba","slls","llssssll"]
```
**Example 2:**
```
Input: ["bat","tab","cat"]
Output: [[0,1],[1,0]] 
Explanation: The palindromes are ["battab","tabbat"]
```

## Solution
$O(K*N^2)$
```java
class Solution {
    public List<List<Integer>> palindromePairs(String[] words) {
        HashMap<String, Integer> map = new HashMap<>();
        List<List<Integer>> res = new ArrayList<>();
        if (words == null || words.length < 2) return res;
        
        for (int i = 0; i < words.length; i++) map.put(words[i], i);
        if (map.containsKey("")){
            for (String word: map.keySet()){
                if (isPalindrome(word) && !word.equals("")){
                    res.add(Arrays.asList(map.get(""), map.get(word)));
                    res.add(Arrays.asList(map.get(word), map.get("")));
                }
            }
        }
        for (String word: map.keySet()){
            String rev = new StringBuffer(word).reverse().toString();
            if (map.containsKey(rev) && map.get(rev)!=map.get(word))
                res.add(Arrays.asList(map.get(word), map.get(rev)));
        }
        
        for (String word: words){
            for (int i = 1; i < word.length(); i++){
                String p1 = word.substring(0, i);
                String p2 = word.substring(i);
                
                if (isPalindrome(p1)){
                    String rev = new StringBuffer(p2).reverse().toString();
                    if (map.containsKey(rev) && map.get(rev)!=map.get(word)){
                        res.add(Arrays.asList(map.get(rev), map.get(word)));
                    }
                }
                
                if (isPalindrome(p2)){
                    String rev = new StringBuffer(p1).reverse().toString();
                    if (map.containsKey(rev) && map.get(rev) != map.get(word)){
                        res.add(Arrays.asList(map.get(word), map.get(rev)));
                    }
                }
            }
        }
        
        return res;
    }
    private boolean isPalindrome(String s){
        String rev= new StringBuffer(s).reverse().toString();
        if (s.equals(rev)) return true;
        else return false;
    }
}
```

<hr />