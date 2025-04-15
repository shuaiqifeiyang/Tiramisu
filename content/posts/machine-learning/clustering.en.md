---
title: "Clustering"
date: 2022-03-09T15:32:34-08:00
draft: true
---
Clustering: one important unsupervised learning problem.
<!--more-->

* supervised learning: aim to predict
* unsupervised learning: discover hidden and latent patterns and explore data

**Input**: data points $\vec x_1,\dots,\vec x_N\in\mathbb{R}^D$ and clusters $K$ we want

**Output**: group the data into $K$ clusters, which means: 

* find assignments $\gamma_{nk}\in\{0, 1\}$ for each data point. Only one in $\{\gamma_{n1},\gamma_{n2},\dots ,\gamma_{nK}\}$ is 1
* find the clusters centers $\vec \mu_1,\dots,\vec \mu_K\in\mathbb{R}^D$

**Clustering can be used to image compression**

* each pixel is a point
* perform clustering over these points
* replace each point by the center of the cluster it belongs to

**Use K-means to measure the quality of K Cluster**: $F(\{\gamma_{nk}, \{\vec \mu_k\}\})=\sum\limits_{n=1}^{N}\sum\limits_{k=1}^{K}\gamma_{nk}\parallel\vec x_n-\vec \mu_k\parallel_2^2$, the sum of distance of each point to its center

Finding the exact minimizer of K-means is NP-hard

Instead, use a heuristic that **alternatively minimizes over $\{\gamma_{nk}\}$ and $\{\vec \mu_k\}$**

For $t=1,2,...$

find $\{\gamma_{nk}^{(t+1)}\}=\mathop{argmin}\limits_{\{\gamma_{nk}\}}\ F(\{\gamma_{nk}, \{\vec \mu_k\}\})$, this step assigns each point to the closest center

find $\{\vec\mu_{k}^{(t+1)}\}=\mathop{argmin}\limits_{\{\vec\mu_k\}}\ F(\{\gamma_{nk}^{(t+1)}, \{\vec \mu_k\}\})$, average the points of each cluster

It will coverage in a finite number of iterations to **a local minimum**, it could take exponentially many iterations to converge.

Local minimum can be arbitrarily worse. Initialization matters a lot!



**Expectation-Maximization (EM) algorithm**

We want to come up with a probabilistic model $p$ to explain how the data is generated. That is, each point is an independent sample of $\vec x \thicksim p$

A GMM has the following density function: $p(\vec x)=\sum\limits_{k=1}^{K}w_kN(\vec x|\vec\mu_k,\Sigma_k)$

* $K$: the number of Gaussian components
* $w_1,\dots,w_K$: mixture weights, a distribution over $K$ components
* $\vec\mu_k$ and $\Sigma_k$: mean and covariance matrix of the $k$-th Gaussian
* $N$: the density function for a Gaussian

by introducing a latent variable $z\in[K]$

$p(\vec x)=\sum\limits_{k=1}^{K}p(\vec x, z=k)=\sum\limits_{k=1}^{K}p(z=k)p(\vec x|z=k)=\sum\limits_{k=1}^{K}\omega_kN(\vec x|\vec\mu_k,\boldsymbol{\Sigma_k})$

Learning GMM means finding all the parameters $\theta=\{\omega_k,\vec\mu_k,\boldsymbol\Sigma_k\}_{k=1}^{K}$

**maximum-likelihood estimation(MLE)**

$\mathop{\mathrm{argmax}}\limits_\theta\  \mathrm{ln}\prod\limits_{n=1}^Np(\vec x_n;\theta)=\mathop{\mathrm{argmax}}\limits_\theta\sum\limits_{n=1}^N\mathrm{ln}\ p(\vec x_n;\theta)$

This is called incomplete likelihood (since $z_n$ are unobserved), and is intractable in general (non-concave problem)

**Expectation-Maximization (EM) algorithm**

EM is a heuristic to solve MLE with latent variables

find the maximizer of $P(\boldsymbol\theta)=\sum\limits_{n=1}^N\mathrm{ln}\ p(\vec x_n;\boldsymbol\theta)=\sum\limits_{n=1}^N\mathrm{ln}\ \int_{z_n}p(\vec x_n,z_n;\boldsymbol\theta)dz_n$

* $\boldsymbol\theta$ is the parameters for a general probabilistic model
* $\vec x_n$ are observed random variables
* $z_n$ are latent variables

