---
title: Leetcode735-Asteroid Collision
categories: leetcode
tags: [Stack, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-04 22:39:02
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

We are given an array asteroids of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

## Example

**Example 1:**
```
Input: asteroids = [5,10,-5]
Output: [5,10]
Explanation: The 10 and -5 collide resulting in 10.  The 5 and 10 never collide.
```
**Example 2:**
```
Input: asteroids = [8,-8]
Output: []
Explanation: The 8 and -8 collide exploding each other.
```
**Example 3:**
```
Input: asteroids = [10,2,-5]
Output: [10]
Explanation: The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.
```
**Example 4:**
```
Input: asteroids = [-2,-1,1,2]
Output: [-2,-1,1,2]
Explanation: The -2 and -1 are moving left, while the 1 and 2 are moving right. Asteroids moving the same direction never meet, so no asteroids will meet each other.
``` 

**Constraints:**

* 1 <= asteroids <= 104
* -1000 <= asteroids[i] <= 1000
* asteroids[i] != 0

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Stack<Integer> st = new Stack<>();
        for (int asteroid: asteroids){
            if (asteroid > 0){
                st.push(asteroid);
            }
            else{              
                while (!st.isEmpty() && st.peek() > 0 && st.peek() < Math.abs(asteroid)){
                    st.pop();
                }
                if (!st.isEmpty() && st.peek() == Math.abs(asteroid)){
                    st.pop();
                }
                else if (st.isEmpty() || st.peek() < 0){
                    st.push(asteroid);
                }
            }
        }
        int[] res = new int[st.size()];
        for (int i = st.size() - 1; i >= 0; i--){
            res[i] = st.pop();
        }
        return res;
    }
}
```

<hr />