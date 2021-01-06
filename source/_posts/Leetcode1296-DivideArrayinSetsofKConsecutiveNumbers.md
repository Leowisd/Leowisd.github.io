---
title: Leetcode1296-Divide Array in Sets of K Consecutive Numbers
categories: leetcode
tags: [Array, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-05 22:14:33
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers nums and a positive integer k, find whether it's possible to divide this array into sets of k consecutive numbers
Return True if its possible otherwise return False.

## Example

**Example 1:**
```
Input: nums = [1,2,3,3,4,4,5,6], k = 4
Output: true
Explanation: Array can be divided into [1,2,3,4] and [3,4,5,6].
```
**Example 2:**
```
Input: nums = [3,2,1,2,3,4,3,4,5,9,10,11], k = 3
Output: true
Explanation: Array can be divided into [1,2,3] , [2,3,4] , [3,4,5] and [9,10,11].
```
**Example 3:**
```
Input: nums = [3,3,2,2,1,1], k = 3
Output: true
```
**Example 4:**
```
Input: nums = [1,2,3,4], k = 3
Output: false
Explanation: Each array should be divided in subarrays of size 3.
```

**Constraints:**
```
1 <= nums.length <= 10^5
1 <= nums[i] <= 10^9
1 <= k <= nums.length
```

Note: This question is the same as 846: https://leetcode.com/problems/hand-of-straights/

## Solution

### Solution 1: Basic

1. Count number of different cards to a map c
2. Loop from the smallest card number.
3. Everytime we meet a new card i, we cut off i - i + k - 1 from the counter.

* Time Complexity: $$O(Mlog^M + MK)$$
* Space Complexity: $$O(M)$$

```java
class Solution {
    public boolean isPossibleDivide(int[] nums, int k) {
        if (nums.length % k != 0) {
            return false; 
        }
        TreeMap<Integer, Integer> map = new TreeMap<>();
        for (int num : nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        
        for (int num : map.keySet()){
            if (map.get(num) > 0){
                for (int i = k - 1; i >= 0; i--){
                    if (map.getOrDefault(num + i, 0) < map.get(num)) return false;
                    map.put(num + i, map.getOrDefault(num + i, 0) - map.get(num));
                }
            }
        }
        return true;
    }
}
```

### Solution 2: Improved

1. Count number of different cards to a map c
2. Cur represent current open straight groups.
3. In a deque start, we record the number of opened a straight group.
4. Loop from the smallest card number.
```
For example, A = [1,2,3,2,3,4], k = 3
We meet one 1:
opened = 0, we open a new straight groups starting at 1, push (1,1) to start.
We meet two 2:
opened = 1, we need open another straight groups starting at 1, push (2,1) to start.
We meet two 3:
opened = 2, it match current opened groups.
We open one group at 1, now we close it. opened = opened - 1 = 1
We meet one 4:
opened = 1, it match current opened groups.
We open one group at 2, now we close it. opened = opened - 1 = 0
```
5. return if no more open groups.

* Time Complexity: $$O(Mlog^M + N)$$
* Space Complexity: $$O(M)$$

```java
class Solution {
    public boolean isPossibleDivide(int[] nums, int k) {
        if (nums.length % k != 0) {
            return false; 
        }
        TreeMap<Integer, Integer> map = new TreeMap<>();
        for (int num : nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        
        Queue<Integer> start = new LinkedList<>();
        int cur = 0;
        int pre = -1;
        for (int num : map.keySet()){
            if ((cur > 0 && num > pre + 1) || cur > map.get(num)) return false;
            start.add(map.get(num) - cur);
            pre = num;
            cur = map.get(num);
            if (start.size() == k) cur -= start.poll();
        }
        return cur == 0;
    }
}
```

### Solution 3: Fastest

* Time Complexity: $$O(N)$$, overall each element will be visited twice.
* Space Complexity: $$O(N)$$

```java
class Solution {
    public boolean isPossibleDivide(int[] nums, int k) {
        if (nums == null || nums.length == 0) return true;
        if (nums.length % k != 0) return false;
        Map<Integer, Integer> freqMap = new HashMap<>();
        for (int num : nums) freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
        
        for (int i = 0; i < nums.length; ++i) {
            if (!freqMap.containsKey(nums[i])) continue;    
            
            // Find the start of the sequence of consecutive numbers that nums[i] belongs to.
            int start = nums[i];
            while (freqMap.containsKey(start - 1)) {
                start--;
            }
            
            // Keep creating consecutive sequences of k numbers.
            for (int m = start; m <= nums[i]; ++m) {
                if (!freqMap.containsKey(m)) continue;
                int numOccurrences = freqMap.get(m);    // There must be this many sequences of length k that start with m.
                for (int j = 0; j < k; ++j) {
                    if (freqMap.containsKey(m + j) && numOccurrences <= freqMap.get(m + j)) {
                        freqMap.put(m + j, freqMap.get(m + j) - numOccurrences);
                        if (freqMap.get(m + j) == 0) freqMap.remove(m + j);
                    } else {
                        return false;   // We can't create numOccurrences sequences of consecutive numbers starting at m.
                    }
                }
            }
        }
        return true;
    }
}

```

<hr />