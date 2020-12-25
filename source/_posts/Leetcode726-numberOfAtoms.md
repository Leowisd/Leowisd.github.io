---
title: Leetcode726-Number Of Atoms
categories: leetcode
tags: [Recursion, Hash Table, String, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-12-25 01:18:50
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a chemical formula (given as a string), return the count of each atom.

The atomic element always starts with an uppercase character, then zero or more lowercase letters, representing the name.

One or more digits representing that element's count may follow if the count is greater than 1. If the count is 1, no digits will follow. For example, H2O and H2O2 are possible, but H1O2 is impossible.

Two formulas concatenated together to produce another formula. For example, H2O2He3Mg4 is also a formula.

A formula placed in parentheses, and a count (optionally added) is also a formula. For example, (H2O2) and (H2O2)3 are formulas.

Given a formula, return the count of all elements as a string in the following form: the first name (in sorted order), followed by its count (if that count is more than 1), followed by the second name (in sorted order), followed by its count (if that count is more than 1), and so on.

## Example
**Example 1:**
```
Input: formula = "H2O"
Output: "H2O"
Explanation: The count of elements are {'H': 2, 'O': 1}.
```
**Example 2:**
```
Input: formula = "Mg(OH)2"
Output: "H2MgO2"
Explanation: The count of elements are {'H': 2, 'Mg': 1, 'O': 2}.
```
**Example 3:**
```
Input: formula = "K4(ON(SO3)2)2"
Output: "K4N2O14S4"
Explanation: The count of elements are {'K': 4, 'N': 2, 'O': 14, 'S': 4}.
```
**Example 4:**
```
Input: formula = "Be32"
Output: "Be32"
``` 

**Constraints:**

* 1 <= formula.length <= 1000
* formula consists of English letters, digits, '(', and ')'.
* formula is always valid.

## Solution

* Time Complexity: $$O(N)$$ or $$O(Mlog^M)  M = numOfAtomTypes$$
* Space Complexity: $$O(N)$$

```java
class Solution {
    private int i;
    public String countOfAtoms(String formula) {
        if (formula == null || formula.length() == 0) return "";

        StringBuilder res = new StringBuilder();
        Map<String, Integer> count = helper(formula.toCharArray());
        for (String atom: count.keySet()){
            res.append(atom);
            if (count.get(atom) > 1){
                res.append(Integer.toString(count.get(atom)));
            }
        }
        return res.toString();
    }
    
    private Map<String, Integer> helper(char[] formula){
        Map<String, Integer> res = new TreeMap<>();
        while(i < formula.length){
            if (formula[i] == '('){
                i++;
                Map<String, Integer> tmp = helper(formula);
                int count = getCount(formula);
                for (String atom: tmp.keySet()){
                    res.put(atom, res.getOrDefault(atom, 0) + tmp.get(atom) * count);
                }
            }
            else if (formula[i] == ')'){
                i++;
                return res;
            }
            else{
                String name = getName(formula);
                res.put(name, res.getOrDefault(name, 0) + getCount(formula));
            }
        }
        return res;
    }
    
    private String getName(char[] formula){
        StringBuilder name = new StringBuilder();
        name.append(formula[i++]);
        while(i < formula.length && formula[i] >= 'a' && formula[i] <='z'){
            name.append(formula[i++]);
        }
        return name.toString();
    }
    
    private int getCount(char[] formula){
        int res = 0;
        while(i < formula.length && formula[i] >= '0' && formula[i] <= '9'){
            res = res * 10 + (formula[i++] - '0');
        }
        return res == 0 ? 1 : res;
    }
}
```

<hr />