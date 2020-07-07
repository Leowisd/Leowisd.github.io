---
title: Leetcode1209-removeAllAdjacentDuplicatesInStringII
categories: leetcode
tags: [Stack, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 00:26:05
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string s, a k duplicate removal consists of choosing k adjacent and equal letters from s and removing them causing the left and the right side of the deleted substring to concatenate together.

We repeatedly make k duplicate removals on s until we no longer can.

Return the final string after all such duplicate removals have been made.

It is guaranteed that the answer is unique.

## Example
**Example 1:**
```
Input: s = "abcd", k = 2
Output: "abcd"
Explanation: There's nothing to delete.
```
**Example 2:**
```
Input: s = "deeedbbcccbdaa", k = 3
Output: "aa"
Explanation: 
First delete "eee" and "ccc", get "ddbbbdaa"
Then delete "bbb", get "dddaa"
Finally delete "ddd", get "aa"
```
**Example 3:**
```
Input: s = "pbbcggttciiippooaais", k = 2
Output: "ps"
```

**Constraints:**

* 1 <= s.length <= 10^5
* 2 <= k <= 10^4
* s only contains lower case English letters.

## Solution

**Solution 1: used two stacks, the slowest, 18ms**

```java
class Solution {
// slowest method: used two stacks, O(N), 18ms
    public String removeDuplicates(String s, int k) {
        if (s == null || s.length() == 0) return s;
        
        Stack<Character> st = new Stack<>();
        Stack<Integer> counter = new Stack<>();
        int cur = k - 1;
        for (char ch : s.toCharArray()){
            if (st.isEmpty() || ch != st.peek()){
                cur = k - 1;
                st.push(ch);
                counter.push(cur);
            }
            else if (ch == st.peek()){
                cur--;
                if (cur == 0){
                    for (int i = 0; i < k - 1; i++){
                        st.pop();
                        counter.pop();
                    }
                    if (!counter.isEmpty())
                        cur = counter.peek();
                }
                else{
                    st.push(ch);
                    counter.push(cur);
                }
            }
        }
        StringBuilder res = new StringBuilder();
        while(!st.isEmpty())
            res.append(st.pop());
        return res.reverse().toString();
    }
}
```

**Solution 2: Basic method, used one stack to store char with count,  10ms**
```java
class Solution {
// Used one stack to store char with count, 10ms, O(N)
    class Pair{
        public char ch;
        public int count;
        public Pair(char ch, int count){
            this.ch = ch;
            this.count = count;
        }

    }
    public String removeDuplicates(String s, int k) {
        if (s == null || s.length() == 0) return s;
        
        Stack<Pair> st = new Stack<>();
        for (char ch: s.toCharArray()){
            if (st.isEmpty()||ch != st.peek().ch){
                st.push(new Pair(ch, 1));
            }
            else if (ch == st.peek().ch){
                if (st.peek().count + 1 == k){
                    st.pop();
                }
                else{
                    st.peek().count++;
                }
            }
        }
        StringBuilder res = new StringBuilder();
        while(!st.isEmpty()){
            Pair top = st.pop();
            for (int i = 0; i < top.count; i++)
                res.append(top.ch);
        }
        return res.reverse().toString();
    }
```

**Solution 3: two pointers, the fastest, 3ms**
```java
class Solution {
//  Two Pointers, O(N), 3ms
    public String removeDuplicates(String s, int k) {
        int i = 0, n = s.length(), count[] = new int[n];
        char[] stack = s.toCharArray();
        for (int j = 0; j < n; ++j, ++i) {
            stack[i] = stack[j];
            count[i] = i > 0 && stack[i - 1] == stack[j] ? count[i - 1] + 1 : 1;
            if (count[i] == k) i -= k;
        }
        return new String(stack, 0, i);
    }
}
```
<hr />