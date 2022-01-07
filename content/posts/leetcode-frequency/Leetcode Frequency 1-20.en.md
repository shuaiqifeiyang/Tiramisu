---
title: "Leetcode Frequency 1-20 Review"
date: 2021-10-26T20:05:37-07:00
draft: false
tags: ["Algorithm", "Leetcode"]
categories: ["Leetcode Frequency"]
---
Leetcode Top 20 high-frequency problem: types, solutions, and summary

<!--more-->

## Hash Table

### 1. Two Sum

Easy
[1. Two Sum](https://leetcode.com/problems/two-sum/)

### 146. LRU Cache

Medium
[146. LRU Cache](https://leetcode.com/problems/lru-cache/)
We use a double linked list to store keys and values in nodes, we put the recently used node at the head of the double linked list. In this way, we can move a node in the middle of linkedlist to the begin of linkedlist in O(1) time, if we know the position of node. So we use a hashmap to store key and the key's postion, in C++, a node's position in a double linked list is iterator.

If we want to get key's value from LRU Cache, firstly we check the hash map. If the key not exists, we return -1. If the key exists, we get the value in double linked list. Then, we move the node to the head of linked list.

If we want to put key's value in the LRU Cache, firstly we still check the hash map. If the key exists, we erase the key in double linked list. Then, we insert a new node with new value in the head of the double linked list. Last but not least, if the size of LRU Cache, which equals to the size of hash map exceeds the capacity, we delete the last node in doule linked list, and erase the node's key in hash map.

### 560. Subarray Sum Equals K

Medium
[560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
Use hash table to store the prefix sum that has been present. Current sum minus prefix sum is the subarray's sum.

## Sorting

### 56. Merge Intervals

Medium
[56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

## Binary Search

### 4. Median of Two Sorted Arrays

Hard
[4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

## Two Pointers

### 42. Trapping Rain Water

Hard
[42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/solution/)
Firstly, Find maximum of height of bar from the left end up to an index i in the array left_max.
Secondly, find maximum of height of bar from the right end up to an index i in the array right_max.
Iterate over the height array and add min(left_max[i], right_max[i])
Time Complexity: O(N)
Space Complexoty: O(N)
Acatually, there is another algorithm space efficiently.

```C++
class Solution {
public:
    int trap(vector<int>& height) {
        int left=0, right=height.size()-1;
        int maxLeft=0, maxRight=0;
        int res=0;
        while(left<=right){
            if(height[left]<=height[right]){
                maxLeft=max(height[left], maxLeft);
                res+=maxLeft-height[left];
                left++;
            }else{
                maxRight=max(height[right], maxRight);
                res+=maxRight-height[right];
                right--;
            }
        }
        return res;
    }
};
```

## DFS

### 200. Number of Islands

Medium
[200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
A trick: it's not necessary to set a "visited" array, we can change the value in the array to indicate whether the position has been visited.

## Linked List

### 2. Add Two Numbers

Medium
[2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
The idea is simple, but it's not that easy to wirte elegant code to this problem.

## Math

### 1041. Robot Bounded In Circle

Medium[1041. Robot Bounded In Circle](https://leetcode.com/problems/robot-bounded-in-circle/)
What we should concerned about is the final direcion and the final position after the robot executes these instructions.

1. If the final direction and the initial direction is the same
   1. If the final position and the initial position is the same. Clearly, the robot is bounded in a circle.
   2. If the final position is not the initial position. Clearly, the robot is not bounded in a circle because the offset will repeat after next round so and so on.
2. If the final direction and the initial direction is different, there must be a circle. After at most four rounds, the robot will return to the initial position with initial direction. The instructions in these four rounds will cancel each other out.

### 7. Reverse Integer

Medium
[7. Reverse Integer](https://leetcode.com/problems/reverse-integer/)
In this problem, we should be concerned about integer overflow

```C++
class Solution {
public:
    int reverse(int x) {
        // -2147483648 ~ 2147483647
        int res=0;
        while(x!=0){
            int pop=x%10;
            x /=10;
            if(res>INT_MAX/10||(res==INT_MAX/10 && pop>7)) return 0;
            if(res<INT_MIN/10||(res==INT_MIN/10 && pop<-8)) return 0;
            res=res*10+pop;
        }
        return res;
    }
};
```

### 423. Reconstruct Original Digits from English

[423. Reconstruct Original Digits from English](https://leetcode.com/problems/reconstruct-original-digits-from-english/)
It's an interesting math problem testing our ability to observe. We should notice that some letters are only present in specific number.

## DP

### 1235. Maximum Profit in Job Scheduling

Hard
[1235. Maximum Profit in Job Scheduling](https://leetcode.com/problems/maximum-profit-in-job-scheduling/)
This is a problem combining DP and binary search. We should make use of `upper_bound` in STL to make our code more concise.

```C++
class Solution {
public:
    int jobScheduling(vector<int>& startTime, vector<int>& endTime, vector<int>& profit) {
        vector<vector<int>> jobs;
        int n=startTime.size();
        vector<int> dp(n, 0);
        int maxProfit=0;
        for(int i=0;i<n;i++){
            jobs.push_back({endTime[i], startTime[i], profit[i]});
        }
        sort(jobs.begin(), jobs.end());
        dp[0]=jobs[0][2];
        for(int i=1;i<n;i++){
            int start=jobs[i][1], end=jobs[i][0], curprofit=jobs[i][2];
            vector<int> t={start, INT_MAX, INT_MAX};
            auto it_start=upper_bound(jobs.begin(), jobs.begin()+i, t);
            auto it=it_start-1;
            if(it_start==jobs.begin()){
                dp[i]=max(jobs[i][2], dp[i-1]);
            }else{
                dp[i]=max(dp[it-jobs.begin()]+jobs[i][2], dp[i-1]);
            }
            maxProfit=max(maxProfit, dp[i]);
        }
        return maxProfit;
    }
};
```

### 53. Maximum Subarray

Easy[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)It's an interesting DP problem.

* dp[0]=nums[0];
* dp[i]=max(dp[i-1], 0)+nums[i];
* res=max(dp[i]) (0<=i<=nums.size()-1)

## Simulation

### 121. Best Time to Buy and Sell Stock

Easy
[121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
Iterate the array and use a variable as the minimum value from the left to the current position in the array. So the current max profit is currrent value minus the minimum value.

### 5. Longest Palindromic Substring

Medium
[5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)
A palindrome can be expanded from its center. Use global variable to make code more concise and readable

### 14. Longest Common Prefix

Easy
[14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)
Brute force is OK for this problem.

## Stack

### 20. Valid Parentheses

Easy
[20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
If we meet the left part of brace, square brackets or parenthese, push it to the stack. If we meet right part, check the top of stack. If the top of the stack is the corresponding left part, pop out the top of the stack. Otherwise, it's not a valid parenthese. Finally, if there are some items left in the stack, it's also not a valid string.

## Sliding Window

### 3. Longest Substring Without Repeating Characters

Medium
[3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
We use a hashset to store the characters in current window. We slide the right bound of the window to right until there are duplicate characters in current window. Then we slide left bound of current window until there are not duplicate characters in window.

## Heap

### 253. Meeting Rooms II

[253. Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/)
This is a very interesting problem about heap. Use a min-heap to store the end time. If current start time is greater than the minimum end time, we don't need to add a new room. If the current start time is less than the minimum end time, we need to add a new room. Final result is the size of the heap.
