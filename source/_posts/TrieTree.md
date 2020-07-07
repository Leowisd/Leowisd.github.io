---
title: TrieTree
tags: [Trie, Tree]
mathjax: true
date: 2019-10-16 11:49:35
permalink:
categories: Algorithms
description: 
image:
---
<p class="description"></p>

<img src="https://" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Implementation

```java
Class TrieNode{
    boolean isEnd;
    TreeNode[] sons;
    public TrieNode(){
        sons = new TreeNode[26];
    }
}

public void addWord(String s, TrieNode root){
    TreeNode cur = root;
    for (char ch: s.toCharArray()){
        if (cur.sons[ch - 'a'] == null) cur.sons[ch - 'a'] = new TrieNode();
        cur = cur.sons[ch -'a'];
    }
    cur.isEnd = true;
}

public boolean search(String s, TrieNode root){
    TrieNode cur = root;
    for (char ch: s.toCharArray()){
        if (cur.sons[ch - 'a'] == null) return false;
        cur = cur.sons[ch - 'a'];
    }
    if (cur.isEnd) return true;
    return false; 
}

public void main(){
    TrieNode root = new TrieNode();
    String word = "Congratulations";
    addWord(word, root);
    if (search(word, root)) System.out.println("Congratuations!");
}
```

## 

##

<hr />