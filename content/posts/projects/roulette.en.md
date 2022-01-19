---
title: "Roulette"
date: 2022-01-19T12:59:22-08:00
draft: false
tags: ["React"]
categories: ["Projects"]
---
Simulation of Roulette in Las Vegas Casinos

<!--more-->

## Introduction

You can play it [online](https://shuaiqifeiyang.github.io/roulette/build/index.html).

[Github Repository](https://www.github.com/shuaiqifeiyang/roulette)

This game is developed with ReactJS.

## Implementation

### How to implement the layout in Roulette Table?

Where we put chips like this:

![](https://raw.githubusercontent.com/shuaiqifeiyang/Tiramisu/main/content/posts/projects/img/roulette1.png)

In CSS, Grid layout perfectly fits out needs. We use `grid-template-areas` divide each area. Then we use `grid-area` place blocks to corresponding area.

### How to draw circle using CSS?

```CSS
div{
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
```



