---
title: "887 Super Egg Drop"
date: 2021-11-02T20:19:10-07:00
draft: false
---

<!--more-->
[887. Super Egg Drop](https://leetcode.com/problems/super-egg-drop/)  
## 题意
一个房子有n层楼，存在一个楼层f(0<=f<=n)，当从f层楼或者f层楼以下扔鸡蛋，鸡蛋不会摔碎。如果从f层楼之上扔鸡蛋，鸡蛋会摔碎。告诉你有k个鸡蛋并且楼房有n层楼，至少需要扔多少次鸡蛋可以找出楼层f。  
## 算法
动态规划解决。  
dp[M][K]表示给K个鸡蛋，扔鸡蛋M次，能够在dp[M][K]层楼中找到f  
初始状态：dp[0][k]=0(0<=k<=K)，表示给0个鸡蛋，无论扔多少次都只能找到0层楼中的f  
递推关系：dp[m][k]=dp[m-1][k-1]+1+dp[m-1][k]。  
这个递推的关系的意思是：最先从dp[m-1][k-1]+1层楼扔鸡蛋，如果鸡蛋碎了，证明需要在dp[m-1][k-1]+1的下面找f，如果鸡蛋没碎，证明需要在dp[m-1][k-1]+1上面找f。下面能够达到的最大的楼层是dp[m-1][k-1]，上面能够达到的最大的楼层是dp[m-1][k]。
## 代码
```C++
class Solution {
public:
    int superEggDrop(int k, int n) {
        vector<vector<int>> dp(k+1, vector<int>(n+1, 0));
        //int maxFloor=0;
        int dropCnt=0;
        while(dp[k][dropCnt]<n){
            dropCnt++;
            for(int eggCnt=1;eggCnt<=k;eggCnt++){
                dp[eggCnt][dropCnt]=dp[eggCnt-1][dropCnt-1]+1+dp[eggCnt][dropCnt-1];
                // maxFloor=max(maxFloor, dp[eggCnt][dropCnt]);
            }
        }
        return dropCnt;
    }
};
```
