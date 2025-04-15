---
title: "A Tour of Go Notes"
date: 2022-01-25T13:08:55-08:00
draft: true
---
## Basics

### Packages, variables and functions

* In Go, a name is exported if it begins with a capital letter. When importing a package, you can refer only to its exported names.
* the type comes after the variable name

  ```go
  package main

  import "fmt"

  func add(x int, y int) int {
  	return x + y
  }

  func main() {
  	fmt.Println(add(42, 13))
  }
  ```
* When two or more consecutive named function parameters share a type, you can omit the type from all but the last. `x int, y int` to `x, y int`
* Multiple results: a function can return any number of results.

  ```Go
  package main

  import "fmt"

  func swap(x, y string) (string, string) {
  	return y, x
  }

  func main() {
  	a, b := swap("hello", "world")
  	fmt.Println(a, b)
  }
  ```
* Named return values: These names should be used to document the meaning of the return values.

  ```go
  package main

  import "fmt"

  func split(sum int) (x, y int) {
  	x = sum * 4 / 9
  	y = sum - x
  	return // naked return should be used only in short functions
  }
  func main() {
  	fmt.Println(split(17))
  }
  ```
* `var` statement declares a list of variables

  ```go
  var c, python, java bool
  var i, j int = 1, 2
  var x, python, java = true, false, "no!"
  ```
* **In side a function**, the `:=` short assignment statement can be used in place of a var declaration with implicit type. Outside a function, every statement begins with a keyword (`var`, `func`, and so on) and so the construction is not available.
* Basic types:

  ```go
  bool

  string

  int  int8  int16  int32  int64
  uint uint8 uint16 uint32 uint64 uintptr

  byte // alias for uint8

  rune // alias for int32
       // represents a Unicode code point

  float32 float64

  complex64 complex128
  ```

  The `int`, `uint`, and `uintptr` types are usually 32 bits wide on 32-bit systems and 64 bits wide on 64-bit systems. When you need an integer value you should use `int` unless you have a specific reason to use a sized or unsigned integer type.
* Variables declared without an explicit initial value are given their **zero value.**
* Unlike in C, in Go **assignment between items of different type requires an explicit conversion**.
* Constants cannot be declared using the `:=` syntax
* An untyped constants takes the type needed by its context.

### Flow control statements: for, if, else, switch and defer

* for

  ```go
  sum:=0;
  for i:=0;i<10;i++ {
    sum+=i
  }
  for ; sum<1000; {
    sum+=sum
  }
  // Fo is Go's while
  for sum < 1000 {
    sum+=sum
  }
  ```
* If statement can start with a short statement to execute before the condition. Variables declared by the statement are only in scope until the end of the if.

  ```go
  if v := math.Pow(x, n); v < lim {
    return v
  }
  ```
* Variables declared inside an if short statement are also available inside any of the else blocks.
* In switch, `break` statement in each case is automatically provided. Go's switch cases need not be constants, and the values need not be integers.
* Switch without a condition is the same as `switch true`
* A defer statement defers the execution of a function until the surrounding function returns.
* Deferred function calls are pushed onto a stack.

### More types: structs, slices and maps
