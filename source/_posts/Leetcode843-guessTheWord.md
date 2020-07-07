---
title: Leetcode843-guessTheWord
categories: leetcode
tags: [Random, Minimax, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 15:31:32
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

This problem is an interactive problem new to the LeetCode platform.

We are given a word list of unique words, each word is 6 letters long, and one word in this list is chosen as secret.

You may call master.guess(word) to guess a word.  The guessed word should have type string and must be from the original list with 6 lowercase letters.

This function returns an integer type, representing the number of exact matches (value and position) of your guess to the secret word.  Also, if your guess is not in the given wordlist, it will return -1 instead.

For each test case, you have 10 guesses to guess the word. At the end of any number of calls, if you have made 10 or less calls to master.guess and at least one of these guesses was the secret, you pass the testcase.

Besides the example test case below, there will be 5 additional test cases, each with 100 words in the word list.  The letters of each word in those testcases were chosen independently at random from 'a' to 'z', such that every word in the given word lists is unique.

## Example
```
Example 1:
Input: secret = "acckzz", wordlist = ["acckzz","ccbazz","eiowzz","abcczz"]

Explanation:

master.guess("aaaaaa") returns -1, because "aaaaaa" is not in wordlist.
master.guess("acckzz") returns 6, because "acckzz" is secret and has all 6 matches.
master.guess("ccbazz") returns 3, because "ccbazz" has 3 matches.
master.guess("eiowzz") returns 2, because "eiowzz" has 2 matches.
master.guess("abcczz") returns 4, because "abcczz" has 4 matches.

We made 5 calls to master.guess and one of them was the secret, so we pass the test case.
```
**Note:**  Any solutions that attempt to circumvent the judge will result in disqualification.

## Solution

**Solution 1: Guess a Random Word**

All words are generated randomly.

So why not we also guess a random word and let it be whatever will be.

**Solution 2: Minimax**

Generally, we will get 0 matches from the master.guess. As a result, the size of wordlist reduces slowly.

Recall some math here, the possiblity that get 0 matched is:
$$(25/26) ^ 6 = 79.03%$$

That is to say, if we make a blind guess,
we have about 80% chance to get 0 matched with the secret word.

To simplify the model,
we're going to assume that,
we will always run into the worst case (get 0 matched).

In this case,
we have 80% chance to eliminate the candidate word
as well as its close words which have at least 1 match.

Additionally, in order to delete a max part of words,
we select a candidate who has a big "family",
(that is, the fewest 0 matched with other words.)
**We want to guess a word that can minimum our worst outcome.**

So we compare each two words and count their matches.
For each word, we note how many word of 0 matches it gets.
Then we guess the word with minimum words of 0 matches.

In this solution, we apply a minimax idea.
We minimize our worst case,
The worst case is _max(the number of words with x matches)_,
and we assume it equal to "the number of words with 0 matches"

**Solution 3: Count the occurrence of characters**

In the previous solution, we compaired each two words.
This make the complexity O(N^2) for each turn.

But actually we don't have to do that.
We just need to count the occurrence for each character on each position.

If we can guess the word that not in the wordlist,
we can guess the word based on the most frequent character on the position.

Here we have to guess a word from the list,
we still can calculate a score of similarity for each word,
and guess the word with highest score.

```java
/**
 * // This is the Master's API interface.
 * // You should not implement it, or speculate about its implementation
 * interface Master {
 *     public int guess(String word) {}
 * }
 */
class Solution {
    public void findSecretWord(String[] wordlist, Master master) {
//      Solution 1: Randomly guess, Time: O(N), Space: O(N)
        // for (int i = 0; i < 10; i++){
        //     String guess = wordlist[new Random().nextInt(wordlist.length)];
        //     int x = master.guess(guess);
        //     if (x < 6){
        //         List<String> temp = new ArrayList<>();
        //         for (String word: wordlist){
        //             if (match(word, guess) == x)
        //                 temp.add(word);
        //         }
        //         wordlist = temp.toArray(new String[temp.size()]);
        //     }
        // }
//      Solution 2: Minimax guess, Time: O(N^2), Space: O(N)
//         for (int i = 0; i < 10; i++){
//             HashMap<String, Integer> count = new HashMap<>();
//             for (String word1: wordlist)
//                 for (String word2: wordlist)
//                     if (match(word1, word2) == 0)
//                         count.put(word1, count.getOrDefault(word1, 0) + 1);
            
//             String guess = "";
//             int min = Integer.MAX_VALUE;
//             for (String word: wordlist){
//                 if (min > count.getOrDefault(word, 0)){
//                     guess = word;
//                     min = count.getOrDefault(word, 0);
//                 }
//             }
            
//             int x = master.guess(guess);
//             List<String> temp = new ArrayList<>();
//             for (String word: wordlist){
//                 if (match(guess, word) == x)
//                     temp.add(word);
//             }
//             wordlist = temp.toArray(new String[temp.size()]);
//         }
//      Solution 3: Count the occurance of each characters, Time O(N), Space O(N)
        for (int i = 0; i < 10; i++){
            int[][] count = new int[6][26];
            for (String word: wordlist)
                for (int k = 0; k < 6; k++)
                    count[k][word.charAt(k) - 'a']++;
            
            String guess = wordlist[0];
            int max = 0;
            for (String word: wordlist){
                int score = 0;
                for (int k = 0; k < 6; k++)
                    score += count[k][word.charAt(k) - 'a'];
                
                if (score > max){
                    max = score;
                    guess = word;
                }
            }
            
            int x = master.guess(guess);
            List<String> temp = new ArrayList<>();
            for (String word: wordlist)
                if (match(guess, word) == x)
                    temp.add(word);
            wordlist = temp.toArray(new String[temp.size()]);
        }
    }
//  Used to count the number of matches between two words
    private int match(String s1, String s2){
        int count = 0;
        for (int i = 0; i < s1.length(); i++){
            if (s1.charAt(i) == s2.charAt(i))
                count++;
        }
        return count;
    }
}
```

<hr />