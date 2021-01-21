---
title: Leetcode347-topKFrequentElements
categories: leetcode
tags: [Hash Table, Heap, Quick Select, Amazon, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-18 22:34:41
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty array of integers, return the k most frequent elements.

## Example

**Example 1:**
```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```
**Example 2:**
```
Input: nums = [1], k = 1
Output: [1]
```
**Note**:
* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

## Solution

### Solution 1: Heap

**Time Complexity:** $$O(Nlogk)$$

**Space Complexity:** $$O(N)$$

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int x:nums){
            if (map.containsKey(x)){
                map.put(x, map.get(x)+1);
            }
            else map.put(x, 1);
        }

        PriorityQueue<Note> pq = new PriorityQueue<>(k, new Comparator<Note>(){
            @Override
            public int compare(Note a, Note b){
                return a.freq-b.freq;
            }
        });
        for (int x: map.keySet()){
            pq.offer(new Note(x, map.get(x)));
            if (pq.size() > k){
                pq.poll();
            }
        }

        List<Integer> res = new ArrayList<>();
        while (!pq.isEmpty()){
            res.add(pq.poll().val);
        }
        return res;
    }
    
    public class Note{
        int val;
        int freq;
        public Note(int val, int freq){
            this.val = val;
            this.freq = freq;
        }
    }

}
```

### Solution 2: Quick Select

**Time Complexity:** $$O(N)$$, worest case $$O(N)$$

**Space Complexity:** $$O(N)$$
```java
class Solution {
    Map<Integer, Integer> map = new HashMap<>();
    public int[] topKFrequent(int[] nums, int k) {
        for (int num: nums)
            map.put(num, map.getOrDefault(num,0) + 1);
        
        nums = map.keySet().stream().mapToInt(i->i).toArray();
        int start = 0, end = nums.length - 1;
        while(start < end) {
            int partitionIndex = partition(nums, start, end);
            if(partitionIndex < k - 1) 
                start = partitionIndex + 1;
            else if(partitionIndex > k - 1)
                end = partitionIndex - 1;
            else 
                break;
        }
        
       return Arrays.copyOfRange(nums,0,k);
    }

    // Randomized Quick Partition....
    private int partition(int[] nums, int start, int end) {
        int partitionIndex = start;
        int randomIndex = ThreadLocalRandom.current().nextInt(start, end);
        swap(nums, start , randomIndex);
        int pivot = map.get(nums[end]);
        
        for(int i = start; i < end; i++) {
            int cur = map.get(nums[i]);
            if(cur >= pivot) 
                swap(nums, i, partitionIndex++);
        }
        
        swap(nums, partitionIndex, end);
        return partitionIndex;
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

<hr />