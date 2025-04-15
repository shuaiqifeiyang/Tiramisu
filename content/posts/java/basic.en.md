---
title: "Basic"
date: 2022-03-07T12:53:08-08:00
draft: true
---

1. switch
```Java
int price = switch(coffee){
  case "Espresso", "Americano" -> 15;
  case "Latte", "Macchiato" -> 20;
  default -> 0;
}
```