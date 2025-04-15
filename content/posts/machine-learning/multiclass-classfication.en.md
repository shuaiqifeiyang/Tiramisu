---
title: "Multiclass Classfication"
date: 2022-02-10T12:37:13-08:00
draft: true
---
Multiclass Classificaion

<!--more-->

**Linear models for multiclass classification**

$\mathcal{F}=\{f(\vec x)=\mathop{\mathrm{argmax}}\limits_{k\in[C]}\ \vec w_k^T\vec x|\vec w_1,...,\vec w_C\in\mathbb{R}^D\}$

$=\{f(\vec x)=\mathop{\mathrm{argmax}}\limits_{k\in[C]}(\boldsymbol W\vec x)_k|\boldsymbol{W}\in\mathbb{R}^{C\times D}\}$

🔺Think of $\vec w^t\vec x$ as a score for class k

For binary logistic regression, with $\vec w=\vec w_1-\vec w_2$

$\mathbb{P}(y=1|\vec x,\vec w)=\sigma(\vec w^T\vec x)=\frac{1}{1+e^{-\vec w^T\vec x}}=\frac{e^{\vec w_1^T\vec x}}{e^{\vec w_1^T\vec x}+e^{\vec w_2^T\vec x}}\propto e^{\vec w_1^T\vec x}$

Naturally, for multiclass:

$\mathbb{P}(y=k|\vec x;\boldsymbol{W})=\frac{e^{\vec w_k^T\vec x}}{\sum_{k^\prime\in[C]}e^{\vec w_{k^\prime}^T\vec x}}\propto e^{\vec w_k^T\vec x}$

**Applying MLE again**
