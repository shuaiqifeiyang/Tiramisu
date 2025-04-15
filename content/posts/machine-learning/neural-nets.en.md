---
title: "Neural Nets"
date: 2022-02-17T13:17:26-08:00
draft: true
---

Neural Nets

<!--more-->

Linear model as a one layer neural net

$o=h(\vec w^T\vec x)$, $h(a)=a$ for linear model

To create non-linearity, can use

* Rectified Linear Unit (ReLU): $h(a)=\mathrm{max}\{0, a\}$
* sigmoid function: $h(a)=\frac{1}{1+e^{-a}}$
* TanH: $h(a)=\frac{e^a-e^{-a}}{e^a+e^{-a}}$

**An L-layer neural net can be written as**

$\boldsymbol{f}(\vec x)=\boldsymbol{h_L}(\boldsymbol{W_Lh_{L-1}}(\boldsymbol{W_{L-1}}\cdots\boldsymbol{h_1}(\boldsymbol{W_1}\vec x)))$

* $\boldsymbol h$ is called the activation function

  * can use $h(a)=1$ for one neuron in each layer to incorporate bias term
  * output neuron can use $h(a)=a$

* this is a **feedforward, fully connected** neural net, there are many variants

* To ease notation, for a given input $\vec x$, define recursively

  $\vec {o_0}=\vec x, \vec{a_l}=\boldsymbol{W}_l\vec o_{l-1},\vec o_l=\boldsymbol h_l(\vec a_l)$

  * $\boldsymbol{W}_l\in\mathbb{R}^{D_l\times D_{l-1}}$ is the weights for layer $l$
  * $D_0=D,D_1,\cdots,D_L$ are numbers of neurons at each layer
  * $\vec a_l\in\mathbb{R}^{D_l}$ is input to layer $l$
  * $\vec o_l\in\mathbb{R}^{D_l}$ is output to layer $l$
  * $\boldsymbol h:\mathbb{R}^{D_l}\rightarrow\mathbb{R}^{D_l}$ is activation functions at layer $l$

**How powerful are neural nets**

* **Universal approximation theorem**: a feedforward neural net with a single hidden layer can approximate any continuous functions, although it might need a huge number of neurons and depth helps.

**Optimization target**:

$\varepsilon(\boldsymbol W_1,\dots,\boldsymbol W_L)=\sum\limits_{n=1}^N\varepsilon_n(\boldsymbol W_1,\dots,\boldsymbol W_L)$

* $\varepsilon_n(\boldsymbol W_1,\dots,\boldsymbol W_L)=\parallel\boldsymbol f(\vec x_n)-\vec y_n\parallel_2^2$ for regression
* $\varepsilon_n(\boldsymbol W_1,\dots,\boldsymbol W_L)=\mathrm{ln}(1+\sum_{k\neq y_n}e^{f(\vec x_n)_k-f(\vec x_n)_{y_n}})$

**Chain rule**:

* for $f(g(w))$, $\frac{\partial f}{\partial w}=\frac{\partial f}{\partial g}\frac{\partial g}{\partial w}$
* for $f(g_1(w), g_2(w),\dots,g_d(w))$, $\frac{\partial f}{\partial w}=\sum\limits_{i=1}^d\frac{\partial f}{\partial g_i}\frac{\partial g_i}{\partial w}$

**The derivative of $\varepsilon_n$ to $w_{ij}$**

$\frac{\partial\varepsilon_n}{\partial w_{l,ij}}=\frac{\partial\varepsilon_n}{\partial a_{l,i}}o_{l-1,j}$

