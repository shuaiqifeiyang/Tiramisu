---
title: "Leetcode Frequency 41-60 Review"
date: 2021-11-30T23:25:26-08:00
draft: false
tags: ["Algorithm", "Leetcode"]
categories: ["Leetcode Frequency"]
math:
    enable: true
---
Leetcode Top 41-60 high-frequency problems: types, solutions, and summary

<!--more-->

## Trie

### 212. Word Search II

Hard
[212. Word Search II](https://leetcode.com/problems/word-search-ii/)
Trie Template Code

```C++
class Trie {
public:
    Trie* routes[26]={nullptr};
    string entireWord = "";
    Trie(){
        for(int i=0;i<26;i++){
            routes[i]=nullptr;
        }
    }
    void insert(const string& word, int pos){
        if(pos==word.size()){
            entireWord=word;
            return;
        }
        if(routes[word[pos]-'a']==nullptr){
            routes[word[pos]-'a']=new Trie();
        }
        routes[word[pos]-'a']->insert(word, pos+1);
    }
};
```

STL:

* isupper(), toupper(), tolower(): `toupper(board[x][y])` doesn't change the parameter, `board[x][y]=toupprt(board[x][y])` changes the value.

Tricks:

* use upper letters to denote the position has been visited
* set the entireWord to empty string after the word is matched to avoid duplicate words in res.

## Two Pointers

### 680. Valid Palindrome II

Easy
[680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/)

Use two pointers to check whether the string is Palindrome if delete at most 1 tiem in the string. Time complexity  is O(n)

Elegant Code:

```C++
bool validPalindrome(string s) {
  for (int i = 0, j = s.size() - 1; i < j; i++, j--)
    if (s[i] != s[j]) {
      int i1 = i, j1 = j - 1, i2 = i + 1, j2 = j;
      while (i1 < j1 && s[i1] == s[j1]) {i1++; j1--;};
      while (i2 < j2 && s[i2] == s[j2]) {i2++; j2--;};
      return i1 >= j1 || i2 >= j2;
    }
  return true;
}
```

### 11. Container With Most Water

Medium
[11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

```C++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left=0, right=height.size()-1;
        int res=0;
        while(left<right){
            res=max(res, min(height[left], height[right])*(right-left));
            if(height[left]<height[right]){
                left++;
            }else{
                right--;
            }
        }
        return res;
    }
};
```

## Sort

### 215. Kth Largest Element in an Array

Medium
[215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

The solution is similar to Quick Sort

### 973. K Closest Points to Origin

Medium
[973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)

The solution is similar to Quick Sort.

## Greedy

### 1326. Minimum Number of Taps to Open to Water a Garden

Hard
[1326. Minimum Number of Taps to Open to Water a Garden](https://leetcode.com/problems/minimum-number-of-taps-to-open-to-water-a-garden/)

Sort the intervals according to its start position. Traversal the array that stores the intervals, we make a variable indicate current furthest position can reach and make another variable indicate next furthest position can reach based on current furhtest position. Essentialy, it is a greedy algorithm, every time we choose the tap thay can reach furthest position.

## Tree

### 236. Lowest Common Ancestor of a Binary Tree

Medium
[236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

Post-Order Traversal the binary tree

## DFS

### 394. Decode String

Medium
[394. Decode String](https://leetcode.com/problems/decode-string/)

### 79. Word Search

Medium
[79. Word Search](https://leetcode.com/problems/word-search/)

## Heap

### 295. Find Median from Data Stream

Hard
[295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

Use two heaps, maxheap stores the smaller part of these numbers and minheap stores the larger part of these numbers.

## Stack

### 227. Basic Calculator II

Medium
[227. Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii/)

* string s only consists of operators +, -, *, /
* does not contain parentheses

### 224. Basic Calculator

Hard
[224. Basic Calculator](https://leetcode.com/problems/basic-calculator/)

* `s` consists of digits, `'+'`, `'-'`, `'('`, `')'`, and `' '`.

Usc stack to store operator.

## Hash

### 1396. Design Underground System

Medium
[1396. Design Underground System](https://leetcode.com/problems/design-underground-system/)

```C++
// "startStation->endStation": <totalTime, totalCnt>
unordered_map<string, pair<int, int>> journeyData;
//  CarID: <station, checkin Time>
unordered_map<int, pair<string, int>> checkinData;
```

## Simulation

### 696. Count Binary Substrings

Easy
[696. Count Binary Substrings](https://leetcode.com/problems/count-binary-substrings/)

We need to calculate the length of same-character contiguous block with the string.

### 443. String Compresssion

Medium
[443. String Compression](https://leetcode.com/problems/string-compression/)

### 12. Roman to Integer

Easy
[12. Roman to Integer]()
