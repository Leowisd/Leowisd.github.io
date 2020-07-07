---
title: Leetcode912-sortAnArray
categories: leetcode
tags: [Sort, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 21:35:55
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers nums, sort the array in ascending order.

## Example
**Example 1:**
```
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
```
**Example 2:**
```
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```

**Constraints:**

* 1 <= nums.length <= 50000
* -50000 <= nums[i] <= 50000

## Solution
```java
class Solution {
    
    Random random = new Random();
    public List<Integer> sortArray(int[] nums) {
        // selectionSort(nums);
        
        quickSort(nums, 0, nums.length - 1);
        
        // mergeSort(nums, 0, nums.length - 1);
        
        List<Integer> res = new ArrayList<>();
        for (int num: nums) res.add(num);
        return res;
    }
    
    private void selectionSort(int[] nums){
        for (int i = 0; i < nums.length; i++){
            int minIdx = i;
            for (int j = i + 1; j < nums.length; j++){
                if (nums[j] < nums[minIdx]){
                    minIdx = j;
                }
            }
            int temp = nums[i];
            nums[i] = nums[minIdx];
            nums[minIdx] = temp;
        }
    }
    
    private void quickSort(int[] nums, int left, int right){
        if (left >= right) return;
        int p = left + random.nextInt(right - left + 1);
        int temp = nums[p];
        nums[p] = nums[left];
        nums[left] = temp;
        int i = left;
        int j = right;
        int x = nums[i];
        while(i < j){
            while(i < j && nums[j] > x) j--;
            nums[i] = nums[j];
            while(i < j && nums[i] <= x) i++;
            nums[j] = nums[i];
        }
        nums[i] = x;
        quickSort(nums, left, i - 1);
        quickSort(nums, i + 1, right);
    }
    
    private void mergeSort(int[] nums, int left, int right){
        int[] cur = (int[])nums.clone();
        if (left < right){
            int mid = (left + right)/2;
            mergeSort(cur, left, mid);
            mergeSort(cur, mid + 1, right);
            mergeSortHelper(cur, left, mid, right, nums);
        }
    }
    private void mergeSortHelper(int[] cur, int left, int mid, int right, int[] nums){
        int i = left;
        int j = mid + 1;
        int k = left - 1;
        while(i <= mid && j <= right){
            k++;
            if (cur[i] <= cur[j]){
                nums[k] = cur[i];
                i++;
            }
            else{
                nums[k] = cur[j];
                j++;
            }
        }
        while(i <= mid){
            k++;
            nums[k] = cur[i];
            i++;
        }
        while(j <= right){
            k++;
            nums[k] = cur[j];
            j++;
        }
    }
    
}
```

<hr />