# Rust Language Basics

## Variables

Rust contains many of the same types of variables used in other programming languages.
These variables include:
- integer: ```int``` ```(u8,i8,u16,i16...u64/usize)```
- floating-point ```f32,f64```
- boolean ```bool```
- character ```char```
- tuple ```tup```
- array (not frequently used though, Vector is much more common)

You will notice that, unlike higher-level languages like Python, Rust has many
different types of integers. The first letter indicates the sign (`u` for
unsigned, `i` for signed), and the number indicates the number of bits.
Therefore, `u8` is an unsigned 8-bit integer, `i32` is a signed 32-bit integer,
and so on. `usize` is a special type that is the same size as the memory address
of the computer, and is used for indexing into arrays and vectors.


By default, variables are immutable, which means that once you assign a value
you cannot modify (mutate) it anymore. However, you have the option to make your
variables mutable by adding ```mut``` in front of the variable name. 

When defining a variable, sometimes the compiler can infer the type.

`let x = 14;`

Other times it cannot and requires you provide the type

`let x: u8 = 14;`

Read more in the [Rust Book](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html)

## Functions

Functions in Rust are defined as:

```rust
fn main() {
    //expression;
}
```

Functions are private by default. To make them public, add ```pub``` before ```fn```.
A function can be called from another file if it is public. 

```rust
pub fn main() {
    //expression;
}
```

Functions can have a return type that is indicated with -> after the name. For example `fn square(n: u64) -> u64`

The return can be explicitly given with `return [expression or variable];` or it can be the last line of a function with no semicolon:

```rust
fn square(n: u64) -> u64 {
    return n * n;
}
```

or

```rust
fn square(n: u64) -> u64 {
    n * n
}
```

Read more in the [Rust Book](https://doc.rust-lang.org/book/ch03-03-how-functions-work.html)

## Control Flow

### ```if``` Expressions:

- An ```if``` expression allows you to run code depending on conditions. Optionally, we can include an ```else``` expression, which will execute the code if the condition evaluates to false. 
- You can handle multiple conditions by using an ```else if``` expression
- ```if``` expressions can also be used in a ```let``` statement to assign a variable dependent on conditions
- Example:
```rust
fn main() {
    let number = 10;
    
    if number % 5 == 0 {
        println!("number is divisble by 5");
    } else {
        println!("number is not divisble by 5");
    }
}
```

### ``` loop```

- ```loop``` allows you to execute a block of code repeatedly forever, or until you explicitly tell it to stop. 
- You can use the ```break``` keyword within the loop to tell the program when to stop executing the loop
    - If you want to have the ```loop``` return a value, you can add the value you want returned after the ```break``` expression
- Example:
```rust
fn main() {
    let mut counter = 0;

    loop { 
        counter += 1
        if counter == 10 {
            break counter;       // will break the loop and return counter value
        }
    }
}
```

### ``` while``` conditional loop

- A ```while``` loop allows you to run the loop while the condition is true, and when the condition ceases to be true, the loop will break
- Example:
```rust
fn main() {
    let mut number = 5;
    while number > 0 {
        println!(number);
        number -= 1
    }
}
```

### ``` for``` loop

- A ```for``` loop executes code for each item in a collection. When you want to *iterate* through a list of elements, 
this is the most common way to do so. [for loops](https://doc.rust-lang.org/reference/expressions/loop-expr.html#iterator-loops)
Note later you will need to learn more about iterators which allow for loops to iterate through the values. 
When you learn about ownership, you will want to learn about different types of iterators.

```rust
fn main() {
    let v = &["apples", "cake", "coffee"];

    for text in v {
        println!("I like {}.", text);
    }
}
```

You can also iterate through a series of integers.
```rust 
fn main() {
    let mut sum = 0;
    for n in 1..11 {
        sum += n;
    }
    assert_eq!(sum, 55);
}
```

## Rust Macros

Rust has a powerful macro system that consists of two major types of macros:
- **Declarative Macros** with `macro_rules!`. These are similar to C macros.
- **Procedural Macros** with `#[derive]` and `#[proc_macro]` and others. These are more powerful
and resemble decorators in Python.

You have already seen declarative macros in `println!`, `assert_eq!`.
They are built into the language and support _metaprogramming_, which allows you 
to write more condensed code that expands into more verbose code at compile time.
Macros are defined for functions such as `println!` to allow for variable arguments,
a language feature that is not possible with plain functions in Rust. 

Procedural macros are more advanced; you will see a version of them in the [Object-Oriented Features](derive) module. 

Read more in the [Rust Book](https://doc.rust-lang.org/book/ch19-06-macros.html)

