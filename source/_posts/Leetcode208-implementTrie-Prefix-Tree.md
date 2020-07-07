---
title: Leetcode208-implementTrie(Prefix_Tree)
categories: leetcode
tags: [Trie, Design, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-11-05 10:48:20
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Implement a trie with insert, search, and startsWith methods.

## Example
```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```
**Note:**

* You may assume that all inputs are consist of lowercase letters a-z.
* All inputs are guaranteed to be non-empty strings.

## Solution
```java
class Trie {

    class TrieNode{
        boolean isWord;
        TrieNode[] next;
        public TrieNode(){
            next = new TrieNode[26];
            isWord = false;
        }
    }
    
    TrieNode root;
    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        char[] wArray = word.toCharArray();
        TrieNode cur = root;
        for (char ch: wArray){
            if (cur.next[ch - 'a'] == null){
                cur.next[ch - 'a'] = new TrieNode();
                cur = cur.next[ch - 'a'];
            }
            else{
                cur = cur.next[ch - 'a'];
            }
        }
        cur.isWord = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode cur = root;
        char[] wArray = word.toCharArray();
        for (char ch: wArray){
            if (cur.next[ch - 'a'] == null) return false;
            else cur = cur.next[ch - 'a'];
        }
        return cur.isWord;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode cur = root;
        char[] wArray = prefix.toCharArray();
        for (char ch: wArray){
            if (cur.next[ch - 'a'] == null) return false;
            else cur = cur.next[ch - 'a'];
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

<hr />