---
title: Leetcode211-Design Add and Search Words Data Structure
categories: leetcode
tags: [String, Trie, DFS, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2022-01-13 14:31:29
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

* WordDictionary() Initializes the object.
* void addWord(word) Adds word to the data structure, it can be matched later.
* bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

## Example

```
Input
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output
[null,null,null,null,false,true,true,true]

Explanation
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True
```

**Constraints:**

* 1 <= word.length <= 500
* word in addWord consists lower-case English letters.
* word in search consist of  '.' or lower-case English letters.
* At most 50000 calls will be made to addWord and search.

## Solution

**Solution 1:** HashMap, O(MN^2)

```java
// O(N^2 * M)
class WordDictionary {
    Map<Integer, Set<String>> d;

    /** Initialize your data structure here. */
    public WordDictionary() {
        d = new HashMap();
    }

    /** Adds a word into the data structure. */
    public void addWord(String word) {
        int m = word.length();
        if (!d.containsKey(m)) {
            d.put(m, new HashSet());
        }
        d.get(m).add(word);
    }

    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    public boolean search(String word) {
        int m = word.length();
        if (d.containsKey(m)) {
            for (String w : d.get(m)) {
                int i = 0;
                while ((i < m) && (w.charAt(i) == word.charAt(i) || word.charAt(i) == '.')) {
                    i++;
                }
                if (i == m) return true;
            }
        }
        return false;
    }
}
```

**Solution 2:** Trie Tree, O(MN) for defined words without dots, O(NM^26) for undefined words
```java
class TrieNode {
    Map<Character, TrieNode> children = new HashMap<>();
    boolean isWord = false;
    
    public TrieNode(){
    }
}

class WordDictionary {
    private TrieNode node;
    
    public WordDictionary() {
        node = new TrieNode();
    }
    
    public void addWord(String word) {
        TrieNode cur = node;
        for (char ch: word.toCharArray()){
            if (!cur.children.containsKey(ch)){
                cur.children.put(ch, new TrieNode());
            }
            cur = cur.children.get(ch);
        }
        cur.isWord = true;
    }
    
    private boolean searchTrieTree(TrieNode node, String word){
        for (int i = 0; i < word.length(); i++){
            char ch = word.charAt(i);
            if (!node.children.containsKey(ch)){
                if (ch == '.'){
                    for (char c: node.children.keySet()) {
                        TrieNode child = node.children.get(c);
                        if (searchTrieTree(child, word.substring(i + 1))){
                            return true;
                        }
                    }
                }
                return false;
            }
            else{
                node = node.children.get(ch);
            }
        }
        return node.isWord;
    } 
    
    public boolean search(String word) {
        return searchTrieTree(node,word);
    }
}
```

<hr />