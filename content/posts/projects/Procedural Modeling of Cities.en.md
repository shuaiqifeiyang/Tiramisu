---
title: "Procedural"
date: 2021-11-08T11:24:37-08:00
draft: true
math:
    enable: true
---
The implementation of Siggraph01 Procedural Modeling of Cities

<!--more-->

$\omega: R(0, initialRuleAttr) ?I(initRoadAttr, UNASSIGNED)$

$p1: R(del, ruleAttr): del<0 \rightarrow \varepsilon$

$p2: R(del, ruleAttr)>?I(roadAttr, state): state==SUCCEED{globalGoals(ruleAttr, roadAttr) creates\ the\ parameters for pDel[0-2], }$