---
title: "Maximum Flow"
date: 2021-10-25T09:37:16-07:00
draft: false
tags: ["Algorithm"]
categories: ["CSCI-570 Analysis of Algorithm"]
math:
  enable: true
---

This article introduces the maximum flow problem.

<!--more-->
## 1. Problem Statement
**Flow Networks**：a directed graph $G=(E, V)$ with the following features:  
*  Associated with each edge *e* is a *capacity*, which is nonnegative number that we denote $c_e$.
*  There is a single source node $s\in V$.
*  There is a single sink node $t\in V$.

**Assumptions about the flow networks we deal with**:  
*   No edge enters the source $s$ and no edge leaves the sink $t$.
*   At least one edge incident to each node.
*   All capacities are integers

**Flow**:  
An *s-t flow* is a function f that maps each edge e to a nonnegative real number, $f : E \to \mathbf{R} ^+$; the value $f(e)$ intuitively represents the amount of flow carried by edge $e$. A flow f must satisfy the following two properties.  
1. (Capacity conditions) For each $e\in E$, we have $0\leq f(e)\leq c_e$.
2. (Conservation conditions) For each node $v$ other than $s$ and $t$, we have 
$$\sum_{e\ into\ v} f(e)=\sum_{e\ out\ of\ v} f(e)$$

**The value of a flow**, denoted $v(f)$, is defined to be the amount of flow generated at the source:
$$v(f)=\sum_{e\ out\ of\ s} f(e)$$

**The Maximum-Flow Problem:**
Given a flow network, find a flow of maximum posiible value.

## 2. Present a Solution 
**The Residual Graph:**
Given a flow network $G$, and a flow $f$ on $G$, we define the residual graph $G_f$ of G with repect to f as follows.  
*   The node set of $G_f$ is the same as that of $G$.
*   For each edge $e=(u,v)$ of $G$, if $f(e)<c_e$, it indicages that there are $c_e-f(e)$ "leftover" units of capacity on which we could try pushing flow forward. So we include the edge $e=(u,v)$ in $G_f$, with a capacity of $c_e-f(e)$. We will call edges included this way *forward edges*.
*   For each edge $e=(u,v)$ of $G$ on which $f(e)>0$, there are $f(e)$ units of flow that we can “undo” if we want to, by pushing flow backward. So we include the edge $e^\prime = (v, u)$ in $G_f$ , with a capacity of $f(e)$. Note that $e^\prime$ has the same ends as $e$, but its direction is reversed; we will call edges included this way *backward edges*.

**Augmenting Paths in a Residual Graph**  
Assume we have a flow of a network, we want to increase the value of the flow. The method is to find a s-t path $P$ in $G_f$, we define $bottleneck(P,f)$ to be the minimum residual capacity of any edge on $P$. For each edge belong to $P$, if it's a forward edge, increase $f(e)$ by $bottleneck(P, f)$, if it's a backward edge, decrease $f(e)$ in $G$ by $bottleneck(P, f)$.  

**Ford-Fulkerson Algorithm**  
>Max-Flow  
&emsp; Initially $f(e) = 0$ for all $e$ in $G$  
&emsp; While there is an s-t path in the residual graph $G_f$  
        &emsp;&emsp;Let $P$ be a simple s-t path in $G_f$  
        &emsp;&emsp;$f^\prime$ = augment($f$, $P$)  
        &emsp;&emsp;Update $f$ to be $f^\prime$  
        &emsp;&emsp;Update the residual graph $G_f$ to be $G_f^\prime$  
    &emsp;Endwhile  
Return $f$

## 3. Prove Crectness
**definition**:  
1. **s-t cut**: a partition (A, B) of the vertex set V, so that $s\in A$ and $t\in B$  
2. **the capacity of a cut(A, B):** $c(A, B)=\sum_{e\ out\ of\ A}c_e$  
  

**some conclusions**:
1. *Let $f$ be any s-t flow, and (A, B) any s-t cut. Then $v(f) = f^{out}(A) − f^{in}(A)=f^{in}(B) − f^{out}(B)$.*
2. *Let f be any s-t flow, and (A, B) any s-t cut. Then $v(f ) \leq c(A, B)$.*  

**important conclusions:**  
If $f$ is an s-t flow such that there is no s-t path in the residual graph $G_f$, then there is an s-t cut $(A^\ast, B^\ast)$ in $G$ for which $v(f) = c(A^\ast, B^\ast)$. Consequently, $f$ has the maximum value of any flow in $G$, and $(A^\ast, B^\ast)$ has the minimum capacity of any s-t cut in $G$.  
When Fork-Furkerson Algorithm terminates, let $A^*$ denote the set of all nodes v in G for which there is an s-v path in $G_f$. Let $B^\ast$ denote the set of all other nodes: $B^\ast = V − A^\ast$.

## 4. Analysis of Time Complexity
**definition**:  
$C=\sum_{e\ out\ of\ s}c_e$  
**some conclusion**:  
1. Suppose, as above, that all capacities in the flow network $G$ are integers. Then the Ford-Fulkerson Algorithm terminates in at most $C$ iterations of the While loop.
2. All capacities in the flow network $G$ are integers. Then the Ford-Fulkerson Algorithm can be implemented to run in $O(mC)$ time.

**Scaling Fork-Fulkerson Algorithm**  
When choosing augmenting paths wisely, the Fork-Fulkerson Algorithm can be accelerated.  
Let $G_f(\Delta)$ be the subset of the residual graph consisting only of edges with residual capacity of at least $\Delta$.  
>Scaling Max-Flow  
&emsp;Initially f(e) = 0 for all e in G  
&emsp;Initially set $\Delta$ to be the largest power of 2 that is no larger than the maximum capacity out of s: $\Delta \leq max_{e\ out\ of\ s} c_e$  
&emsp;&emsp;While $\Delta\geq1$  
&emsp;&emsp;&emsp;While there is an s-t path in the graph $G_f(\Delta)$  
&emsp;&emsp;&emsp;&emsp;Let P be a simple s-t path in $G_f(\Delta)$  
&emsp;&emsp;&emsp;&emsp;$f^\prime$ = augment(f , P)  
&emsp;&emsp;&emsp;&emsp;Update f to be $f^\prime$ and update $G_f(\Delta)$  
&emsp;&emsp;&emsp;Endwhile  
&emsp;&emsp;&emsp;$\Delta=\Delta/2$  
&emsp;&emsp;Endwhile  
&emsp;Return f  

Time Complexity of scaling version of Fork-Fulkerson Algorithm is $O(m^2log_2C)$



## 5. Applications of Maximum Flow
### 5.1. The Bipartite Matching Problem
**Definition**:
1. bipartite graph $G = (V , E)$ is an undirected graph whose node set can be partitioned as $V = X \cup Y$, with the property that every edge $e \in E$ has one end in $X$ and the other end in $Y$.
2. A matching $M$ in $G$ is a subset of the edges $M \subseteq E$ such that each node appears in at most one edge in $M$.
3. The Bipartite Matching Problem is that of finding a matching in $G$ of largest possible size.

**Turn this problem into a maximum flow problem**:  
![](https://raw.githubusercontent.com/shuaiqifeiyang/Tiramisu/main/content/posts/algorithm/img/max-flow1.png)
**Proof**:  
To prove this we should show that $G^\prime$ will have a max flow of value k **if and only if** $G$'s maximum size of matching is k.

### 5.2. Edge-Disjoint Path in Directed and Undirected Graph
**Edge-Disjoint Path in Directed Graph**: Delete the edges ending at source and edges begining at sink.

**Edge-Disjoint Path in Undirected Graph**: Transfer the original undirected edge to two directed edges with reverse directions. Then this problem is similar to Edge-Disjoint Path in Directed Graph. However, we should pay attention to a case: one path uses directed edge (u, v) and another path uses directed edge (v, u). It is not hard to see that there always exists a maximum flow in any network that uses at most one out of each pair of oppositely directed edges.  
![](https://raw.githubusercontent.com/shuaiqifeiyang/Tiramisu/main/content/posts/algorithm/img/max-flow2.png)
 
### 5.3. Node-Disjoint Path
![](https://raw.githubusercontent.com/shuaiqifeiyang/Tiramisu/main/content/posts/algorithm/img/max-flow3.png)

### 5.4. Circulations with Demands
**Definition**:  
**Circulation Network**:
*   We are given a directed graph $G=(V,E)$ with capacities on edges
*   Associated with each node $v\in V$ a demand $d_v$
    *   If $d_v>0$, node v has demand of $d_v$ as a sink.
    *   If $d_v<0$, node v has supply of $d_v$ as a source.
    *   If $d_v=0$, v is neither a sink and source.


**Circulation**:
*   We say that a circulation with demands {dv} is a function f that assigns a nonnegative real number to each edge and satisfies the following two conditions.
    1. (Capacity conditions)For each $e\in E$, we have $0\leq f(e)\leq c_e$.
    2. (Demand conditions)For each $v\in V$, we have v, $f^{in}(v)−f^{out}(v)=d_v$.  

Our problem is if there is a feasible circulation in a circulation network.  

**Solution**:
![](https://raw.githubusercontent.com/shuaiqifeiyang/Tiramisu/main/content/posts/algorithm/img/max-flow4.png)

### 5.5 Circulation with Demands and Lower Bounds
**Definition**:
 1. (Capacity conditions)For each $e\in E$, we have $l_e\leq f(e)\leq c_e$.
 2. (Demand conditions)For each $v\in V$, we have v, $f^{in}(v)−f^{out}(v)=d_v$.  

**Solution**:  
Satisfying lower bounds first, then the problem is similar to Circulation with Demands
![](https://raw.githubusercontent.com/shuaiqifeiyang/Tiramisu/main/content/posts/algorithm/img/max-flow5.png)

