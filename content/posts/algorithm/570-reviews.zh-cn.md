---
title: "570 Reviews"
date: 2021-11-29T20:11:38-08:00
draft: false
math:
  enable: true
tags: ["Algorithm"]
categories: ["CSCI-570 Analysis of Algorithm"]
---
570 复习

<!--more-->

## Week1

### Stable Matching Problem

给定n个男生和n个女生，每个男生都有一个对所有女生的排名，每个女生也有一个对所有男生的排名

Perfect matching: 男女一对一

Instability：假设m和w匹配，m'和w'匹配，如果m更喜欢w‘，w’更喜欢m，这个时候称（m，w‘）为instability

Matching S is stable if

* it is perfect
* there are no instabilities.

**Gale-Shapley Algorithm**:

* 男生求婚版本：从没有匹配的男生集合中挑选一个男生，从他的列表上排名最高且他没有求过婚的女生开始选，如果这个女生已经和另一个男生匹配了，比较这两个男生在女生心中的优先级，让女生和她更喜欢的男生匹配，淘汰的男生放入没有匹配的男生的集合中
* 女生求婚版本

结论：

* 如果一个女生匹配了，那么当她engaged后，她会一直保持engaged
* 算法会在最大$n^2$次迭代后终止
* 在$O(1)$的时间复杂度比较两个男生在女生心中的排序，把男生的序号变成index，排名变成value
* valid partner：能够在一个stable matching中存在pair(m, w)，那么m和w称为互相的valid partner
* 每一次G-S算法都会得到同样的stable matching，无论男生求婚的顺序如何。在男生求婚的版本中，男生最后都会和他的best valid partner结婚，女生都会和他的worst valid partner结婚

## Week2

### Asymptotic Notation

* O(g(n)) = {f(n) | there exist positive constant C and $n_0$ such that 0<=f(n)<=Cg(n) for all n>=$n_0$}
* $\Omega$(g(n)) = {f(n) | there exist positive constant C and $n_0$ such that 0<=Cg(n)<=f(n) for all n>=$n_0$}
* $\Theta$(g(n)) = {f(n) | there exist positive constant $C_1$ and $C_2$ and $n_0$ such that 0<=$C_1$g(n)<=f(n)<=$C_2$g(n) for all n>=$n_0$}

在比较Asymptotic Notation的大小的时候，Exponential > Polynomial > logarithmic

不能通过简单的Asymptotic Notation来比较算法的快慢，要考虑到数据量的大小。

### BFS & DFS

* 在一个图的BFS tree中，如果在在图中两个节点是相连的，那么在BFS Tree中这两个节点在同一层或者相差一层

**判断一个图是否是bipartite**

* 如果图中有一个环有奇数个节点，那么这个图不可能是bipartite
* 先通过运行BFS把BFS Tree中相邻层的节点标记为Red和Blue，然后遍历边，如果有一条边的两个端点是同一个颜色，说明不是bipartite。整个的算法复杂度是$O(m+n)$

**判断一个 `有向图`是否是Strong Connected**：

* If there is a path from any point to any other point in the graph, 那么这个图就叫有向图
* 先任选一个点s运行BFS或者DFS，判断是不是所有的其他点都可以到达。再将图中所有的边反转，又从s点运行DFS或者DFS，判断是不是所有的其他点都可以到达

**判断在DAG中是否存在一条Path访问所有的节点**：

* 现在O(m+n)的时间复杂度内得到这个 `有向图`的拓扑排序，然后判断拓扑顺序中相邻两个节点之间是否有边

### Interval Scheduling Problem

给定n个间隔，求出最大的不向冲突的间隔个数

* 将这些间隔按照结束时间排好序，遍历这些间隔，把不冲突的间隔选入。时间复杂度是$O(nlogn)$
* 证明方法：证明每一步都不会比optimal solution差

## Week 3

### Scheduling to Minimize Lateness

给定n个任务，完成每个任务需要一点时间，每个任务都有一个ddl。安排这些任务，minimize the maximum lateness

* 将这些任务按照ddl大小没有间隔地安排
* 证明方法：
  * 定义inversion：先安排ddl晚的任务
  * 我们的solution没有inversion
  * 消除inversion不会影响optimality，所有的optimal solution都可以转化为我们的solution

### Priority Queue

* Full Binary Tree：二叉树全满
* Complete Binary Tree：二叉树除了最后一行全满，且最后一行左边全满
* Binary Heap各种操作实现
  * Find Max O(1)
  * insert，先把要插入的元素放在最末尾，然后上滤 O(logn)
  * Delete，把最后一个元素放在要删去的元素的位置，上滤或者下滤把元素放在合适的位置 O(logn)
  * Dcrease-key O(logn)
  * 可以用O(n)的时间复杂度建立堆
  * 合并两个binary heap需要O(N)的时间
* 用binary heap找一个数组中第k大的值 O(nlogk)
* binomial heap各种操作的实现

### Amortized Cost Analysis

Aggregate Analysis:算出n个操作总过耗费T(n)，那么每个操作的amortized cost是T(n)/n

Accounting Method:给一些操作更多change，多出来的change作为credit，credit可以用来弥补之后change比实际少的操作

![截屏2021-11-30 14.47.24](/Users/shuaiqifeiyang/Library/Application Support/typora-user-images/截屏2021-11-30 14.47.24.png)

## Week4

对于每条边的w都大于等于0的无向图，找出起点到终点的最短路径

### Dijkstra Algorithm

* 算法过程
  * Start with a set S of vertices whose final shortest path we already know
  * At each step, find a vertex u$\in$V-S with shortest distance from s
  * Add u to S and repeat
* 证明方法: 用induction+contradiction的方法证明每次加到S中的点都找到了最短路径
* 算法复杂度分析，Dijkstra用了n次ExtractMins和m次DecreaseKeys，对应的时间复杂度

![截屏2021-11-30 16.44.40](/Users/shuaiqifeiyang/Library/Application Support/typora-user-images/截屏2021-11-30 16.44.40.png)

### Minimum Spinning Tree

Spinning Tree是包含图中所有节点的Tree

Minimum Spinning Tree是所有edge权重加起来最小的Spinning Tree

*Assume that all edge costs are distinct. Let C be any cycle in G, and let edge e* = (*v*, *w*) *be the most expensive edge belonging to C. Then e does not belong to any minimum spanning tree of G.*

#### Kruskal's Algorithm

将所有edge按照cost排序，依次把edge加入Spinning Tree中如果加入这个edge后不会成环

Kruskal中用Union-Find数据结构判断两个点是否已经连起来了。

* 给边排序O(mlogm)
* 对于每条边，利用Union-Find检查是否成环O(mlogn)
* 总共的时间复杂度是O(mlogm)

#### Pims's Algorithm

类似于Dijkstra算法，每次加入集合的不是离起点最近的节点，而是和set相连的距离最近的节点

#### Reverse-Delete

将所有的edge按照cost排序，从cost大的开始删除图中的边，直到最后的结果是一个树

* 假设所有边的cost都是不一样的，Let S be any subset of nodes that is neither empty nor equal to all of V, and let edge e=(v, w) be the min cost edge with one end in S and the other end in V-S. Then every MST contains the edge e.

### Clustering

* 把一个集合U分为k个集合称为k-clustering of U
* spacing of a k-clustering是minimum distance between any pair of points lying in different clusters
* Given a set of n objects, find a k-clustering with maximum spacing
* 先找出来最小生成树，再删除最小生成树的k-1个most expensive edges
* 证明方法：contradiction，如果有另外一个k-cluster，那么我们现有的一个cluster必然在新的k-cluster里面会被拆开，那么这时的space会变小

### Discussion

* 反转道路的方向
* 当有多个起点的时候引入一个新的起点，然后将新的起点指向多个原来的起点
