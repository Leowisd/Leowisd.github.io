---
title: Leetcode398-randomPickIndex
categories: leetcode
tags: [Reservoir Sampling, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-12 12:02:20
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers with possible duplicates, randomly output the index of a given target number. You can assume that the given target number must exist in the array.

**Note:**
The array size can be very large. Solution that uses too much extra space will not pass the judge.

## Example
```
int[] nums = new int[] {1,2,3,3,3};
Solution solution = new Solution(nums);

// pick(3) should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
solution.pick(3);

// pick(1) should return 0. Since in the array only nums[0] is equal to 1.
solution.pick(1);
```

## Solution
```java
class Solution {
    HashMap<Integer, List<Integer>> map;
    Random random;
    public Solution(int[] nums) {
        random = new Random();
        map = new HashMap<>();
        for (int i = 0; i < nums.length; i++){
            if (!map.containsKey(nums[i]))
                map.put(nums[i], new ArrayList<Integer>());
            map.get(nums[i]).add(i);
        }
    }
    
    public int pick(int target) {
        int size = map.get(target).size();
        return map.get(target).get(random.nextInt(size));
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int param_1 = obj.pick(target);
 */
```

<hr />