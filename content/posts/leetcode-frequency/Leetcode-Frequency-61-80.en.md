---
title: "Leetcode Frequency 61-80"
date: 2021-12-12T12:33:04-08:00
draft: true
---
Leetcode Top 61-80 high-frequency problems: types, solutions, and summary

`<!--more-->`

## Hash

### 1010. Pairs of Songs With Total Durations Divisible by 60

Medium
[1010. Pairs of Songs With Total Durations Divisible by 60](https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/)

This problem is similar to 2 sum. However, in this problem, we don't only have one target number. All numbers that are divisible by 60 are target numbers. We use a hash to store the count of number existed in the array. For every target number, we check if target number minus current number is existed in the array.

### 460. LFU Cache

Hard
[460. LFU Cache](https://leetcode.com/problems/lfu-cache/)

Use 3 hash tables

```C++
unordered_map<int, pair<int, int>> key2ValueAndFrequency;
unordered_map<int, list<int>::iterator> key2Node;
unordered_map<int, list<int>> frequency2Key;
```

## Greedy

### 134. Gas Station

Medium
[134. Gas Station](https://leetcode.com/problems/gas-station/)

The problem emphasizes "If there exists a solution, it is guaranteed to be unique". We use two variables: `total` and `cur`.

* `total` indicates if the sum of gas greater than the sum of cost. If and only if the sum of gas greater than the sum of cost, can we find a start position travel around the circuit.
* `cur` is the remaining gas when we choose a candidate start position. If cur is negative, the candidate start position is invalid and all position between current postion and candidate start position are also invalid.

```C++
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int total=0, cur=0, res=0;
        for(int i=0;i<gas.size();i++){
            total+=gas[i]-cost[i];
            cur+=gas[i]-cost[i];
            if(cur<0){
                cur=0;
                res=i+1;
            }
        }
        return total<0?-1:res;
    }
};
```

## Sort

### 347. Top K Frequent Elements

Medium
[347. Tok K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

Use a hash map to store the frequency of all elements. Record the maximum frequency and create a buckets. Each bucket stores the elements with same frequency.

## Topological Sort

### 210. Course Schedule II

Medium
[210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)

Standard Topological Sort

## Two Pointers

### 18. 4Sum

Medium
[18. 4Sum](https://leetcode.com/problems/4sum/)

The difficult point is how to avoid collecting duplicate number.

## LinkedList

### 21. Merge Two Sorted Lists

Easy
[21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

### 1570. Dot Product of Two Sparse Vectors

Medium
[1570. Dot Product of Two Sparse Vectors](https://leetcode.com/problems/dot-product-of-two-sparse-vectors/)

## DFS

### 529. Minesweepper

Medium
[529. Minesweeper](https://leetcode.com/problems/minesweeper/)

### 297. Serialize and Deserialize Binary Tree

Hard
[297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

### 526. Beautiful Arrangement

Medium
[526. Beautiful Arrangement](https://leetcode.com/problems/beautiful-arrangement/)

## DP

### 139. Word Break

Medium
[139. Word Break](https://leetcode.com/problems/word-break/)

### 174. Dungeon Game

Hard
[174. Dungeon Game](https://leetcode.com/problems/dungeon-game/)

Go from bottom right to top left

## Two Pointers

### 244. Shortest Word Distance II

Medium
[244. Shortest Word Distance II](https://leetcode.com/problems/shortest-word-distance-ii/)

If we have two sorted array, there is a linear time method to calculate the minimum difference between two element from the two array seperately.

## Binary Search

### 981. Time Based Key-Value Store

Medium
[981. Time Based Key-Value Store](https://leetcode.com/problems/time-based-key-value-store/)

The ASCII code of '{' is greater than all letters.

## Stack

### 71. Simplify Path

Medium
[71. Simplify Path](https://leetcode.com/problems/simplify-path/)

STL string find('\\\', idx), idx is the first postion to search. If find doesn't a match, return `string::pos==-1`

## Heap

### 759. Employee Free Time

Hard
[759. Employee Free Time](https://leetcode.com/problems/employee-free-time/)

There are two approach to this problem. One is sort all interval, and the time complexity is O(NlogN). The other one is make use of that every Employee's interval is sorted, so we use priority heap to sort all intervals and the time complexity is O(NlogK), K is the number of employee.

## Math

### 9. Palindrome Number

Easy
[9. Palindrome Number](https://leetcode.com/problems/palindrome-number/)

```C++
bool isPalindrome(int x) {
    if(x<0 || (x%10==0 && x!=0)) return false;
    int revertNumber=0;
    // A way to avoid overflow
    while(x>revertNumber){
        revertNumber=revertNumber*10+x%10;
        x/=10;
    }
    return x==revertNumber || x==revertNumber/10;
}
```

## Topological Sort

### 269. Alien Dictionary

Hard
[269. Alien Dictionary](https://leetcode.com/problems/alien-dictionary/)

Lots of edge cases:

* `['abs', 'ab']`, there is no solution
*
