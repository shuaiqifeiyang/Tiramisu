---
title: "Leetcode Frequency 41-60"
date: 2021-11-30T23:25:26-08:00
draft: true
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

* isupper(), toupper(), tolower()

Tricks:   

* use upper letters to denote the position has been visited
* set the entireWord to empty string after the word is matched to avoid duplicate words in res.

## Two Pointers

### 680. Valid Palindrome II

Easy  
[680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/)

Use two pointers to check whether the string is Palindrome. Time complexity  is O(n)

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

## Sort

### 973. K Closest Points to Origin

Medium  
[973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)

## Greedy



