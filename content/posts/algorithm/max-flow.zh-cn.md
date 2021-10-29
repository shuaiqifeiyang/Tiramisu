---
title: "最大流"
date: 2021-10-24T09:06:32-07:00
draft: false
tags: ["Algorithm"]
categories: ["CSCI-570 Analysis of Algorithm"]
description: "Max Flow问题"
math:
  enable: true
---

这篇文章介绍了Max Flow问题  

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

Time Complexity of Fork-Fulkerson Algorithm is $O(m^2log_2C)$



