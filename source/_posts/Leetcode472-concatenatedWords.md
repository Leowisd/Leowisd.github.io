---
title: Leetcode472-concatenatedWords
categories: leetcode
tags: [DFS, Trie, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-04 22:41:30
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a list of words (without duplicates), please write a program that returns all concatenated words in the given list of words.
A concatenated word is defined as a string that is comprised entirely of at least two shorter words in the given array.

## Example
```
Input: ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]

Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]

Explanation: "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
 "dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
"ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".
```

**Note:**
* The number of elements of the given array will not exceed 10,000
* The length sum of elements in the given array will not exceed 600,000.
* All the input string will only include lower case letters.
* The returned elements order does not matter.

## Solution
```java
class Solution {
    public List<String> findAllConcatenatedWordsInADict(String[] words) {
        List<String> res = new ArrayList<>();
        if (words == null || words.length == 0) return res;
        
        Set<String> set = new HashSet();
        for (String word: words) set.add(word);
        for (String word: words){
            if (dfs(set, word)) res.add(word);
        }
        return res;
    }
    
    public boolean dfs(Set<String> set, String cur){
        for (int i = 1; i < cur.length(); i++){
            if (set.contains(cur.substring(0, i))){
                String rest = cur.substring(i);
                if (set.contains(rest) || dfs(set, rest)) return true;
            }
        }
        return false;
    }
}
```
Time Complex: $O(N*K^2)$

```java
// Trie Tree
class Solution {
    public List<String> findAllConcatenatedWordsInADict(String[] words) {
        List<String> res = new ArrayList<String>();
        if (words == null || words.length == 0) {
            return res;
        }
        TrieNode root = new TrieNode();
        for (String word : words) { // construct Trie tree
            if (word.length() == 0) {
                continue;
            }
            addWord(word, root);
        }
        for (String word : words) { // test word is a concatenated word or not
            if (word.length() == 0) {
                continue;
            }
            if (testWord(word.toCharArray(), 0, root, 0)) {
                res.add(word);
            }
        }
        return res;
    }
    public boolean testWord(char[] chars, int index, TrieNode root, int count) { // count means how many words during the search path
        TrieNode cur = root;
        int n = chars.length;
        for (int i = index; i < n; i++) {
            if (cur.sons[chars[i] - 'a'] == null) {
                return false;
            }
            if (cur.sons[chars[i] - 'a'].isEnd) {
                if (i == n - 1) { // no next word, so test count to get result.
                    return count >= 1;
                }
                if (testWord(chars, i + 1, root, count + 1)) {
                    return true;
                }
            }
            cur = cur.sons[chars[i] - 'a'];
        }
        return false;
    }
    public void addWord(String str, TrieNode root) {
        char[] chars = str.toCharArray();
        TrieNode cur = root;
        for (char c : chars) {
            if (cur.sons[c - 'a'] == null) {
                cur.sons[c - 'a'] = new TrieNode();
            }
            cur = cur.sons[c - 'a'];
        }
        cur.isEnd = true;
    }
}
class TrieNode {
    TrieNode[] sons;
    boolean isEnd;
    public TrieNode() {
        sons = new TrieNode[26];
    }
}
```
Time Complex: $O(N*K)$

<hr />