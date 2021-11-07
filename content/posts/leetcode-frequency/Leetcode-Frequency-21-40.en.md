---
title: "Leetcode"
date: 2021-10-29T22:55:16-07:00
draft: true
---
Leetcode Top 21-40 high-frequency problem: types, solutions, and summary
<!--more-->
## Hash
### 811. Subdomain Visit Count
Medium  
[811. Subdomain Visit Count](https://leetcode.com/problems/subdomain-visit-count/)  
Use hash table to count the number of subdomain. Use STL string.find() and string.substr(int start)

### 49. Group Anagrams
Medium  
[49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)  
For each strings, we count the number of occurrences of each letter. Then we transfer the data to a string, which will be the key in hash map. For example, a string "abab", it's key wtring is "a#2#b#2". As a result, we can group anagrams in hash table.

## Stack
### 1249. Minimum Remove to Make Valid Parentheses
Medium  
[1249. Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)  
To make the string valid with minimum removals, we need to get rid of all parentheses that do not have a matching pair. We use stack to mark removed parentheses with '*', and erase all of them in the end. 
*   The stack store the index of left parenthesis.
*   Extra item in stack presents the left parenthesis that don't have corresponding right parenthesis.
*   `s.erase(remove(s.begin(), s.end(), '*'), s.end()); `

## Simulation
### 68. Text Justification
Hard  
[68. Text Justification](https://leetcode.com/problems/text-justification/)  
A complicated simulation.

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

