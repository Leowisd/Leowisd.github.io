---
title: Leetcode547-friendCircles
categories: leetcode
tags: [Union Find, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-26 21:47:24
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
There are N students in a class. Some of them are friends, while some are not. Their friendship is transitive in nature. For example, if A is a direct friend of B, and B is a direct friend of C, then A is an indirect friend of C. And we defined a friend circle is a group of students who are direct or indirect friends.

Given a N*N matrix M representing the friend relationship between students in the class. If M[i][j] = 1, then the ith and jth students are direct friends with each other, otherwise not. And you have to output the total number of friend circles among all the students.

## Example
**Example 1:**
```
Input: 
[[1,1,0],
 [1,1,0],
 [0,0,1]]
Output: 2
Explanation:The 0th and 1st students are direct friends, so they are in a friend circle. 
The 2nd student himself is in a friend circle. So return 2.
```
**Example 2:**
```
Input: 
[[1,1,0],
 [1,1,1],
 [0,1,1]]
Output: 1
Explanation:The 0th and 1st students are direct friends, the 1st and 2nd students are direct friends, 
so the 0th and 2nd students are indirect friends. All of them are in the same friend circle, so return 1.
```
**Note:**
N is in range [1,200].
M[i][i] = 1 for all students.
If M[i][j] = 1, then M[j][i] = 1.

## Solution
```java
class Solution {
    public int findCircleNum(int[][] M) {
        if (M == null || M.length == 0 || M[0].length == 0) return 0;
        
        int[] friends = new int[M.length];
        for (int i = 0; i < M.length; i++) friends[i] = i;
        for (int i = 0; i < M.length; i++)
            for (int j = 0; j < M.length; j++)
                if (i != j && M[i][j] == 1) union(friends, i, j);
            
        HashSet<Integer> set = new HashSet<>();
        for (int i = 0; i < M.length; i++)
            set.add(find(friends, i));
        return set.size();
    }
    
    private int find(int[] friends, int i){
        if (friends[i] != i)
            friends[i] = find(friends, friends[i]);
        return friends[i];
    }
    
    private void union(int[] friends, int i, int j){
        int si = find(friends, i);
        int sj = find(friends, j);
        if (si != sj) friends[si] = sj;
    }
}
```

<hr />