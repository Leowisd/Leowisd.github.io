---
title: Leetcode384-shuffleanArray
categories: leetcode
tags: [Design, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-13 22:25:04
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Shuffle a set of numbers without duplicates.

## Example
```
// Init an array with set 1, 2, and 3.
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// Shuffle the array [1,2,3] and return its result. Any permutation of [1,2,3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1,2,3].
solution.reset();

// Returns the random shuffling of array [1,2,3].
solution.shuffle();
```

## Solution
```java
class Solution {
    
    private int[] nums;
    private Random random;
    public Solution(int[] nums) {
        this.nums = nums;
        random = new Random();
    }
    
    /** Resets the array to its original configuration and return it. */
    public int[] reset() {
        return nums;
    }
    
    /** Returns a random shuffling of the array. */
    public int[] shuffle() {
        int[] res = new int[nums.length];
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++)
            map.put(i, nums[i]);
        for (int i = 0; i < nums.length; i++){
            int tmp = random.nextInt(nums.length);
            while (!map.containsKey(tmp)){
                tmp = random.nextInt(nums.length);
            }
            res[i] = nums[tmp];
            map.remove(tmp);
        }
        return res;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```

<hr />