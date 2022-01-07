---
title: "ReactJS"
date: 2020-01-03T22:28:15-08:00
draft: false
---
Notes of ReactJS document
`<!--more-->`

# JSX

* Embedding Expressions in JSX using curly braces

  ```jsx
  const name = 'Josh Perez';
  const element = <h1>Hello, {name}</h1>;
  ```

* We split JSX over multiple lines for readability. While it isn’t required, when doing this, we also recommend wrapping it in parentheses to avoid the pitfalls of [automatic semicolon insertion](https://stackoverflow.com/q/2846283).

* JSX is an expression too

* Specifying Attributes with JSX

  ```jsx
  const element = <div tabIndex="0"></div>;
  const element = <img src={user.avatarUrl}></img>;
  ```

* Empty tag ends in `/>`

  ```jsx
  const element = <img src={user.avatarUrl} />;
  ```

* JSX Prevents Injection Attacks: Everything is converted to a string before being rendered.
* JSX represents objects. 

# Rendering Elements

* Elements are the smallest building blocks of React apps.
* 
