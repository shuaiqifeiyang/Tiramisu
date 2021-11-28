---
title: "Approximation"
date: 2021-11-23T21:21:19-08:00
draft: false
math:
    enable: true
---
Approximation Algorithm
<!--more-->
## Load Baancing Problem
m resources with equal processing power
n jobs where job j takes $t_j$ to process
assignment of jobs to resources such that the maximum load on any machine is minimized.

直接贪心，每次都在最小的上面加：2-approximation
先从大到小排序，然后用贪心算法：1.5-approximation

## Vertex Cover
Vertex Cover的decision version没有appximation solution   approximation solution是针对optimazition version的。  
每次循环都把没有覆盖到的边的两个点都加到集合里面去，这是一个2-approximation的算法。  
Vertex Cover的2-appoximation解法不能推出independent set 2-approximation(0.5-approximation)解法  

Vertex Cover $\leq_p$ Set Cover
如果Set Cover有2-approximation的解法，那么也可以得到Vertex Cover的2-approximation解法

### MAX-3SAT






