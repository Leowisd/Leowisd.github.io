---
title: Leetcode846-handOfStraights
categories: leetcode
tags: [Array, Hash Table, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 16:28:16
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Alice has a hand of cards, given as an array of integers.

Now she wants to rearrange the cards into groups so that each group is size W, and consists of W consecutive cards.

Return true if and only if she can.

## Example
**Example 1:**
```
Input: hand = [1,2,3,6,2,3,4,7,8], W = 3
Output: true
Explanation: Alice's hand can be rearranged as [1,2,3],[2,3,4],[6,7,8].
```
**Example 2:**
```
Input: hand = [1,2,3,4,5], W = 4
Output: false
Explanation: Alice's hand can't be rearranged into groups of 4.
```

**Note:**
1. 1 <= hand.length <= 10000
2. 0 <= hand[i] <= 10^9
3. 1 <= W <= hand.length

## Solution
**Solution 1: Basic**
1. Count number of different cards to a map c
2. Loop from the smallest card number.
3. Everytime we meet a new card i, we cut off i ~ i + W - 1 from the counter.

**Time Complexity:** $$O(MlogM + MW)$$

```java
class Solution {
    public boolean isNStraightHand(int[] hand, int W) {
        Map<Integer, Integer> map = new TreeMap<>();
        for (int card: hand)
            map.put(card, map.getOrDefault(card, 0) + 1);
        for (int card: map.keySet()){
            if (map.get(card) > 0){
                for (int i = W - 1; i >= 0; i--){
                    if (map.getOrDefault(card + i, 0) < map.get(card)) return false;
                    map.put(card + i, map.get(card + i) - map.get(card));
                }
            }
        }
        return true;
    }
}
```

**Solution 2: Improved**
1. Count number of different cards to a map c
2. Cur represent current open straight groups.
3. In a deque start, we record the number of opened a straight group.
4. Loop from the smallest card number.

**Time Complexity:** $$O(MlogM + N)$$

```java
class Solution {
    public boolean isNStraightHand(int[] hand, int W) {
        Map<Integer, Integer> map = new TreeMap<>();
        for (int card: hand)
            map.put(card, map.getOrDefault(card, 0) + 1);
        Queue<Integer> start = new LinkedList<>();
        int cur = 0;
        int pre = -1;
        for (int card: map.keySet()){
            if (cur > 0 && card > pre + 1 || cur > map.get(card)) return false;
            start.add(map.get(card) - cur);
            pre = card;
            cur = map.get(card);
            if (start.size() == W) cur -= start.poll();
        }
        return cur == 0;
    }
}
```

**Solution 3: Fastest**

**Time Complexity:** $$O(N)$$, overall each element will be visited twice.

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