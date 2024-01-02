---
layout: post
title: 'Rust: Three ways to print struct infomartion'
date: 2024-01-02 13:59 +0800
---

Rust's struct are like classes/object in Java to model our programs in object oriented way. We often need to log state of the object for debugging. Let's see how can we do that in Rust.

Let's see below Person struct.

```rust
struct Person {
    name: String,
    age: i32,
    salary: i32
}
```

## There are three ways to print struct's information in Rust. 

### Implement ToString interface

We need to implement a ToString interface(typeclass) for Person. You can think it like Typeclass in Scala or extension method in Scala 3.

  ```rust
  impl ToString for Person {
        fn to_string(&self) -> String {
            return format!("name is {}, age is {}, salary is {}", &self.name, &self.age, &self.salary);
        }
  }
  ```

### Implement Display interface

we have another method i.e Implement display for the struct. The difference between Display and ToString is that you will have to call to_string() methon on struct object, but in case of display you don't need to call any method, Rust compiler will automatically infer.

  ```rust
  impl fmt::Display for Person {
      fn fmt(&self, f: &mut fmt::Formatter<'_>) -> fmt::Result {
          write!(f, "name is {}, age is {}, salary is {}", &self.name, &self.age, &self.salary)
      }
    }
```

### Use inbuilt macro.

Last we can use something concise i.e derive macro to annotate struct. 

```rust
  #[derive(Debug)]    
  struct Person {
    name: String,
    age: i32,
    salary: i32  
}
```

Rust is a system programming language but also used as developing web application. Rust offers memeory safety and best of programming languages world. It also support functional programming paradigm, concurrency etc.