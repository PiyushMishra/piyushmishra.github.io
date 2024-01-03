
---
layout: post
title: 'Syntax difference between Scala 3 and Rust while writing higher order functions.'
date: 2024-01-02 19:24 +0800
---

Many of the new languages emerged out with functional programming inspiration from Scala. 
Today we will see how we can write functions like map, flatmap, filter, reduce, fold 
in Scala 3 as well as in Rust and compare style of writing.

Scala 3, unlike Scala 2 has a very concise syntax for writing the functions as it support braceless
and indentation based syntax. Scala 3 support backward compatibility with Scala 2.13 code.

## In Scala 3

### map

---
```scala
val list = List(1,2,3)

// Scala 2 style
list.map(x => x + 1)
list.map(_ + 1) 

// Also it can be written in Scala 3
list.map:
    x => x + 1
```
---

### flatMap
---
```scala
val list = List(1,2,3)
list.flatMap(x => 1 to x)

```
---

---
```scala
list.flatMap(1 to _)

//Scala 3 syntax
list.flatMap:
     x => 1 to x
```
---

### filter
---
```scala
val list = List(1,2,3)
// filter numbers greater than one
list.filter(_ > 1)
list.filter(x => x > 1)

// Scala 3 syntax
list.filter:
    x => x > 1
```
---

### reduce
---
```scala
val list = List(1,2,3)
list.reduce(_+_)
list.reduce((x, y) => x + y)

//Scala 3 Syntax
list.reduce:
    (x, y) => x + y
```
---

### foldLeft
---
```scala
val list = List(1,2,3)
list.fold(0)(_+_)
list.fold(0)((x, y) =>  x+ y)

// Scala 3 syntax
list.fold(0):
    (x, y) =>  x + y
```
---

## In Rust
Now see how rust does all of above. Rust does not have support type inference while collecting the result as compiler does not know how do you want to collect the information. It holds the iteration variables within pipes
like |x|. Consider ownership and borrowing fundamentals while writing code in rust wherever applicable. 

Here we are using into_iter as it better knows about the context and may return object, reference
or mutable reference depending on the context. Basically it creates a new collection and take ownership of it.

### map
---
```rust
let vec_list = vec![1,2,3];
let output: Vec<i32> = vec_list.into_iter().map(|x| x + 1).collect();
println!("{:?}", output);
```
---

### flat_map
---
```rust
let vec_list = vec![1,2,3];
let output: Vec<i32> = vec_list.into_iter().flat_map(|x| 1..x+1).collect();
println!("{:?}", output);
```
---

### filter
---
```rust
let numbers: Vec<i32> = vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let even_numbers = numbers.into_iter().filter(|n| n % 2 == 0).collect::<Vec<i32>>();
println!("{:?}", even_numbers);
```
---

### reduce
---
```rust
let numbers: Vec<i32> = vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let num:i32 = numbers.into_iter().reduce(|a, b| a+b).unwrap();
println!("{:?}", num);
```
---

### fold
---
```rust
let numbers: Vec<i32> = vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let num:i32 = numbers.into_iter().fold(1, |a, b| a+b);
println!("{:?}", num);
```
---

Thanks for reading through the article. Enjoy!
