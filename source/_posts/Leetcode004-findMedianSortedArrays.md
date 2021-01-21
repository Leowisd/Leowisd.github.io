---
title: Leetcode004-findMedianSortedArrays
tags: [Binary Search, Google, Bloomberg, TikTok]
mathjax: true
date: 2019-01-22 09:36:28
categories: leetcode
description: Solution Report of LeetCode Acceptted
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.

## Example

### Example 1

nums1 = [1, 3]

nums2 = [2]

The median is 2.0

### Example 2

nums1 = [1, 2]

nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5

## Solution

### Solution 1: Divide and Conquer

**Time Complexity:** $$O(log(M + N))$$

**Space Complexity:** $$O(1)$$

```
    把两个array A,B各分成左右两半
    left_part     | right_part
    A[0] - A[i-1] | A[i] - A[m-1]
    B[0] - B[j-1] | B[j] - B[n-1]
    保证
    1) len(left_part) == len(right_part)
    2) max(left_part) <= min(right_part)
    即
    (1) i + j == m - i + n - j (or: m - i + n - j + 1) 
        if n >= m, we just need to set: i = 0 ~ m, j = (m + n + 1)/2 - i (n>=m为了保证j>=0)
    (2) B[j-1] <= A[i] and A[i-1] <= B[j]
    这样中位数就是maxLeft或(maxLeft+minRight)/2
```

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        if(m > n){  //to ensure m <= n
            int[] temp = nums1; 
            nums1 = nums2;
            nums2 = temp;
            int tmp = m; 
            m = n;
            n = tmp;
        }
        //二分找i 使B[j-1] <= A[i] and A[i-1] <= B[j]
        int iMin = 0;
        int iMax = m;
        while(iMin <= iMax){
            int i = (iMin + iMax) / 2;
            int j = (m + n + 1) / 2 - i;
            
            if(i < iMax && nums2[j-1] > nums1[i]){  //i is too small
                iMin = i + 1;
            }else if(i > iMin && nums1[i-1] > nums2[j]){    //i is too big
                iMax = i - 1;
            }else{  //i is perfect
                int maxLeft = 0;
                if(i == 0){
                    maxLeft = nums2[j-1];
                }else if(j == 0){
                    maxLeft = nums1[i-1];
                }else{
                    maxLeft = Math.max(nums2[j-1], nums1[i-1]);
                }
                if((m+n) % 2 == 1){
                    return maxLeft;
                }
                int minRight = 0;
                if(i == m){
                    minRight = nums2[j];
                }else if(j == n){
                    minRight = nums1[i];
                }else{
                    minRight = Math.min(nums1[i], nums2[j]);
                }
                return (maxLeft + minRight) / 2.0;
            }
        }
        return 0.0;
        
    }
}

```

### Solution 2
 
convert to find the Kth number in m + n, each time ignore k/2 numbers

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {        
        int m = nums1.length, n = nums2.length;
        int l = (m + n + 1) / 2; //left half of the combined median
        int r = (m + n + 2) / 2; //right half of the combined median
        // If the nums1.length + nums2.length is odd, the 2 function will return the same number
        // Else if nums1.length + nums2.length is even, the 2 function will return the left number and right number that make up a median
        return (getKth(nums1, 0, nums2, 0, l) + getKth(nums1, 0, nums2, 0, r)) / 2.0;
    }
    
    private double getKth(int[] nums1, int start1, int[] nums2, int start2, int k) {
        // This function finds the Kth element in nums1 + nums2
        
        // If nums1 is exhausted, return kth number in nums2
        if (start1 > nums1.length - 1) return nums2[start2 + k - 1];        
        // If nums2 is exhausted, return kth number in nums1
        if (start2 > nums2.length - 1) return nums1[start1 + k - 1];
        // If k == 1, return the first number
        // Since nums1 and nums2 is sorted, the smaller one among the start point of nums1 and nums2 is the first one
        if (k == 1) return Math.min(nums1[start1], nums2[start2]);

        int mid1 = Integer.MAX_VALUE;
        int mid2 = Integer.MAX_VALUE;
        if (start1 + k / 2 - 1 < nums1.length) mid1 = nums1[start1 + k / 2 - 1];
        if (start2 + k / 2 - 1 < nums2.length) mid2 = nums2[start2 + k / 2 - 1];        
        // Throw away half of the array from nums1 or nums2. And cut k in half
        if (mid1 < mid2) {
            return getKth(nums1, start1 + k / 2, nums2, start2, k - k / 2); //nums1.right + nums2
        } else {
            return getKth(nums1, start1, nums2, start2 + k / 2, k - k / 2); //nums1 + nums2.right
        }
    }
}
```

<hr />