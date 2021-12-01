---
title: "Leetcode Frequency 21-40 Review"
date: 2021-10-29T22:55:16-07:00
draft: false
tags: ["Algorithm", "Leetcode"]
categories: ["Leetcode Frequency"]
math:
    enable: true
---
Leetcode Top 21-40 high-frequency problem: types, solutions, and summary
<!--more-->
## Hash
### 811. Subdomain Visit Count
Medium  
[811. Subdomain Visit Count](https://leetcode.com/problems/subdomain-visit-count/)  
Use hash table to count the number of subdomain. Use STL `int` string.find() and string.substr(int start)

### 49. Group Anagrams
Medium  
[49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)  
For each strings, we count the number of occurrences of each letter. Then we transfer the data to a string, which will be the key in hash map. For example, a string "abab", it's key wtring is "a#2#b#2". As a result, we can group anagrams in hash table.

### 41. First Missing Positive
Hard  
[41. First Missing Positive](https://leetcode.com/problems/first-missing-positive/)  
Use original array as the hash map. However, I think the idea of this question is not practical in real production. It's not a good habit to change the parameter passed in from outside.
```C++
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        // Check if 1 exists
        int oneExists = false;
        for(int i=0;i<nums.size();i++){
            if(nums[i]==1){
                oneExists = true;
            }
            if(nums[i]<=0 || nums[i]>=nums.size()+1){
                nums[i]=1;
            }
        }
        if(!oneExists) return 1;
        
        for(int i=0;i<nums.size();i++){
            nums[abs(nums[i])-1]=nums[abs(nums[i])-1]>0?-nums[abs(nums[i])-1]:nums[abs(nums[i])-1];
        }
        for(int i=0;i<nums.size();i++){
            if(nums[i]>0){
                return i+1;
            }
        }
        return nums.size()+1;
    }
};
```
## Stack
### 1249. Minimum Remove to Make Valid Parentheses
Medium  
[1249. Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)  
To make the string valid with minimum removals, we need to get rid of all parentheses that do not have a matching pair. We use stack to mark removed parentheses with '*', and erase all of them in the end. 
*   The stack store the index of left parenthesis.
*   Extra item in stack presents the left parenthesis that don't have corresponding right parenthesis.
*   `s.erase(remove(s.begin(), s.end(), '*'), s.end()); `
    *   `remove` returns an iterator to the element that follows the last element not removed.

## Simulation
### 68. Text Justification
Hard  
[68. Text Justification](https://leetcode.com/problems/text-justification/)  
A complicated simulation. The idea is simple, but the implementation is hard.
### 54. Spiral Matrix
Medium  
[54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)  


### 273. Integer to English Words
Hard  
[273. Integer to English Words](https://leetcode.com/problems/integer-to-english-words/)  
```C++
class Solution {
private:
    vector<pair<int, string>> pron={
        {1000000000, "Billion"}, {1000000, "Million"}, {1000, "Thousand"},
        {100, "Hundred"}, {90, "Ninety"}, {80, "Eighty"}, {70, "Seventy"},
        {60, "Sixty"}, {50, "Fifty"}, {40, "Forty"}, {30, "Thirty"}, {20, "Twenty"},
        {19, "Nineteen"}, {18, "Eighteen"}, {17, "Seventeen"}, {16, "Sixteen"},
        {15, "Fifteen"}, {14, "Fourteen"}, {13, "Thirteen"}, {12, "Twelve"},
        {11, "Eleven"}, {10, "Ten"}, {9, "Nine"}, {8, "Eight"}, {7, "Seven"},
        {6, "Six"}, {5, "Five"}, {4, "Four"}, {3, "Three"}, {2, "Two"}, {1, "One"}
    };
public:
    string numberToWords(int num) {
        if(num==0) return "Zero";
        for(int i=0;i<pron.size();i++){
            if(pron[i].first>num){
                continue;
            }
            string pre=pron[i].first>=100?numberToWords(num/pron[i].first)+" ":"";
            string post=num%pron[i].first==0?"":" "+numberToWords(num%pron[i].first);
            return pre+pron[i].second+post;
        }
        return "";
    }
};
```
## Math
### 31. Next Permutation
Medium  
[31. Next Permutation](https://leetcode.com/problems/next-permutation/)  
```C++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int i=nums.size()-1, j=nums.size()-1;
        while(i>0 && nums[i-1]>=nums[i]){
            i--;
        }
        if(i==0){
            reverse(nums.begin(), nums.end());
            return;
        }
        while(j>=0 && nums[j]<=nums[i-1]){
            j--;
        }
        swap(nums[i-1], nums[j]);
        reverse(nums.begin()+i, nums.end());
        return;
    }
};
```
### 829. Consecutive Numbers Sum
Hard  
[829. Consecutive Numbers Sum](https://leetcode.com/problems/consecutive-numbers-sum/)  
$N = (x+1)+(x+2)+\cdots+(x+k)$  
$N = xk+\frac{(1+k)k}{2}$  
$x$ must be an integer and $x$ is positive.
```C++
class Solution {
public:
    int consecutiveNumbersSum(int n) {
        int res=0;
        int limit=sqrt(2*n);
        for(int k=1;k<limit+1;k++){
            if((n-(1+k)*k/2)%k==0) res++;
        }
        return res;
    }
};
```
## Two Pointers
### 809. Expressive Words
Medium  
[809. Expressive Words](https://leetcode.com/problems/expressive-words/)  
It takes experience to make the code of this problem readable.
```C++
class Solution {
public:
    int expressiveWords(string s, vector<string>& words) {
        int res=0;
        for(string& word: words){
            if(isStretchy(s, word)){
                res++;
            }
        }
        return res;
    }
    bool isStretchy(string stretchy, string str){
        int i=0, j=0;
        while(i<stretchy.size() && j<str.size()){
            if(stretchy[i]!=str[j]) return false;
            int iLen=getRepeatedLength(stretchy, i);
            int jLen=getRepeatedLength(str, j);
            i+=iLen;
            j+=jLen;
            if(iLen<3 && iLen==jLen){
                continue;
            }else if(iLen>=3 && iLen>=jLen){
                continue;
            }else{
                return false;
            }
        }
        return i==stretchy.size() && j==str.size();
    }
    int getRepeatedLength(string& str, int idx){
        char curChar=str[idx];
        int res=0;
        for(int i=idx;i<str.size();i++){
            if(str[i]==curChar) res++;
            else break;
        }
        return res;
    }
};
```

## DFS
### 22. Generate Parentheses
Medium  
[22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)  
We use two parameters `left` and `right` to indicate the number of left parenthese and the number of right parentheses in current string.  
If left < n, we can add a '('.  
If left > right, we can add a ')'.  
When the size of string is 2*n, we store this one in our result array.

## Deque
### 239. Sliding Window Maximum
Hard  
[239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)  
Use deque to store the index. Iterate over the array. At each step :
* Clean the deque :
  * Keep only the indexes of elements from the current sliding window.
  * Remove indexes of all elements smaller than the current one, since they will not be the maximum ones.
* Append the current element to the deque.
* Append deque[0] to the output.

```C++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> DQ;
        vector<int> res;
        for(int i=0;i<nums.size();i++){
            while(!DQ.empty() && DQ.front()<i-k+1){
                DQ.pop_front();
            }
            while(!DQ.empty() && nums[DQ.back()]<nums[i]){
                DQ.pop_back();
            }
            DQ.push_back(i);
            if(i>=k-1) res.push_back(nums[DQ.front()]);
        }
        return res;
    }
};
```
## BFS
### 127. Word Ladder
hard  
[127. Word Ladder](https://leetcode.com/problems/word-ladder/)  
The trick is enumerating the next word and check whether it is unvisited instead of compare the currrent word to all unvisited word and check whether they are connected. 

## Sort
### 215. Kth Largest Element in an Array
Medium  
[215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)  

## Binary Search
### 33. Search in Rotated Sorted Array
medium  
[33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)  
When the target is in the left part of the array:
*   `nums[left]<=target && target<nums[mid]` (left part is in order)
*   `nums[left]>nums[mid] && (target>=nums[left] || target<=nums[mid])` (left part is not in order)

