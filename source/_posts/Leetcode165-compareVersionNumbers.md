---
title: Leetcode165-compareVersionNumbers
tags: [leetcode, Math, String, Amazon]
mathjax: true
date: 2019-09-11 23:45:23
categories: leetcode
description: Solution Report of LeetCode Acceptted
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Compare two version numbers version1 and version2.

If version1 > version2 return 1; if version1 < version2 return -1;otherwise return 0.

You may assume that the version strings are non-empty and contain only digits and the . character.

The . character does not represent a decimal point and is used to separate number sequences.

For instance, 2.5 is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

You may assume the default revision number for each level of a version number to be 0. For example, version number 3.4 has a revision number of 3 and 4 for its first and second level revision number. Its third and fourth level revision number are both 0.

## Example


**Example 1:**
```
Input: version1 = "0.1", version2 = "1.1"
Output: -1
```
**Example 2:**
```
Input: version1 = "1.0.1", version2 = "1"
Output: 1
```
**Example 3:**
```
Input: version1 = "7.5.2.4", version2 = "7.5.3"
Output: -1
```
**Example 4:**
```
Input: version1 = "1.01", version2 = "1.001"
Output: 0
Explanation: Ignoring leading zeroes, both “01” and “001" represent the same number “1”
```
**Example 5:**
```
Input: version1 = "1.0", version2 = "1.0.0"
Output: 0
Explanation: The first version number does not have a third level revision number, which means its third level revision number is default to "0"
``` 

**Note:**
```
Version strings are composed of numeric strings separated by dots . and this numeric strings may have leading zeroes.
Version strings do not start or end with dots, and they will not be two consecutive dots.
```

## Solution

```java
class Solution {
    // public List<String> convert(String version){
    //     char[] v = version.toCharArray(); 
    //     String seperateTemp = "";
    //     List<String> tempNum = new ArrayList<String>(); 
    //     for (char ch : v){
    //         if (seperateTemp.length() == 0 && ch == '0') continue;
    //         if (ch == '.' && seperateTemp.length() > 0){
    //             tempNum.add(seperateTemp);
    //             seperateTemp = "";
    //         }
    //         else if (ch == '.' && seperateTemp.length() == 0){
    //             tempNum.add("0");
    //         }
    //         else seperateTemp += ch;
    //     }
    //     if (seperateTemp.length() == 0) tempNum.add("0");
    //     else tempNum.add(seperateTemp);
    //     return tempNum;
    // }
       
    public int compareVersion(String version1, String version2) {
//         stupid method      
//         List<String> num1 = new ArrayList<String>(convert(version1));
//         List<String> num2 = new ArrayList<String>(convert(version2));
        
        
//         while (num1.size() > num2.size()){
//             num2.add("0");
//         }
//         while (num1.size() < num2.size()){
//             num1.add("0");
//         }

//         for (int i = 0; i < num1.size(); i++){
//             int a = Integer.parseInt(num1.get(i));
//             int b = Integer.parseInt(num2.get(i));
//             if (a > b) return 1;
//             else if (a < b) return -1;
//         }
//         return 0;
        
//      method 2: but if 1.11111111111111111111111.1??
//             String[] levels1 = version1.split("\\.");
//     String[] levels2 = version2.split("\\.");
    
//     int length = Math.max(levels1.length, levels2.length);
//     for (int i=0; i<length; i++) {
//     	Integer v1 = i < levels1.length ? Integer.parseInt(levels1[i]) : 0;
//     	Integer v2 = i < levels2.length ? Integer.parseInt(levels2[i]) : 0;
//     	int compare = v1.compareTo(v2);
//     	if (compare != 0) {
//     		return compare;
//     	}
//     }
    
//     return 0;
        
//   Method 3: final good method
        String[] levels1 = version1.split("\\.");
        String[] levels2 = version2.split("\\.");
    
        int length = Math.max(levels1.length, levels2.length);
        for (int i=0; i<length; i++) {
    	    String v1 = i < levels1.length ? levels1[i] : "0";
    	    String v2 = i < levels2.length ? levels2[i] : "0";
    	    while (v1.charAt(0) == '0' && v1.length() > 1) v1 = v1.substring(1, v1.length());
            while (v2.charAt(0) == '0' && v2.length() > 1) v2 = v2.substring(1, v2.length());
            if (v1.length() > v2.length()) return 1;
            else if (v1.length() < v2.length()) return -1;
            
            for (int j=0; j < v1.length(); j++){
                if (v1.charAt(j) > v2.charAt(j)) return 1;
                else if (v1.charAt(j) < v2.charAt(j)) return -1;
            }
            
        }
    
        return 0;
    }
}
```

<hr />