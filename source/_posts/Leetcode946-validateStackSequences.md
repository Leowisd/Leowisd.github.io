---
title: Leetcode946-validateStackSequences
categories: leetcode
tags: [Stack, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 17:07:24
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given two sequences pushed and popped with distinct values, return true if and only if this could have been the result of a sequence of push and pop operations on an initially empty stack.

## Example
**Example 1:**
```
Input: pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
Output: true
Explanation: We might do the following sequence:
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```
**Example 2:**
```
Input: pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
Output: false
Explanation: 1 cannot be popped before 2.
```
**Note:**

1. 0 <= pushed.length == popped.length <= 1000
2. 0 <= pushed[i], popped[i] < 1000
3. pushed is a permutation of popped.
4. pushed and popped have distinct values.

## Solution

**Solution 1:** Simulating

Time: O(n)

Space: O(n)
```java
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        Stack<Integer> st = new Stack<>();
        int idx = 0;
        for (int num: pushed){
            st.push(num);
            while(!st.isEmpty() && st.peek() == popped[idx]){
                idx++;
                st.pop();
            }
        }
        return st.isEmpty();
    }
}
```
**Solution 2: Used pushed as stack, change the input array**

Time: O(n)

Space: O(1)
```java
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        int i = 0, j = 0;
        for (int num: pushed){
            pushed[i++] = num;
            while(i > 0 && pushed[i - 1] == popped[j]){
                i--;
                j++;
            }
        }
        return i == 0;
    }
}
```
<hr />