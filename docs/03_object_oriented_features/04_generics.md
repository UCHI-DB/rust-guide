# Generics, Option and Result

Generics, or generic programming, or generic data types in Rust (as opposed to concrete data types, which are the ones you are most used to) are a super useful feature of modern (actually not-so-modern, programming languages like ML implemented generics in the 70s!) programming languages. You will see that crustyDB uses generic data types quite extensively, so you probably want to make sure you understand this well. Before defining them, let's start with the motivation for generic data types.

### Why Generics?

Suppose we want to represent the concept of a point in a 2-dimensional space. We can represent a point by using its *x* and *y* coordinates. In Rust, we can represent a point with a simple struct such as:

```rust
struct Point {
    x: u32,
    y: u32,
}
```

in that struct above, the concrete data types of *x* and *y* are integers (u32). Now, suppose that in addition to representing points with integer coordinates we want to represent points with floating point coordinates as well. We cannot mix the concrete types, and if we cast the values when creating the Point structures, we will lose information when downcasting from floating points to integer points. Instead, we could just simply have two different structs, one for integer coordinates and one for floating point coordinates, like this:

```rust
struct IntPoint {
    x: u32,
    y: u32,
}

struct FloatPoint {
    x: f32,
    y: f32,
}
```

That solves our problem, but it introduces a bunch of other inconveniences. For example, every time we want to write some functionality for a point, we have to write it for IntPoint and for FloatPoint, even though the logic of what we want to write may be very similar. Ideally, we'd like to not specify the concrete data types of the coordinates until we know them. Generic data types help us achieve that.

### Generic Data Types in Rust

With generic data types we can parameterize types, i.e., we can say that the type of a concrete data type will be given later. In our running example, we could create a structure Point that takes a parameter that indicates the concrete data type of its coordinates. In Rust, we do that like this:

```rust
struct Point<T> {
    x: T,
    y: T,
}
```

In the example, *T*, is called *type parameter* and indicates between angle brackets. What the struct above says is that a Point has two coordinates, x and y with data type T, which is not concrete yet. This means that at this point the coordinate data types are generic. 

This allows us to declare the specific type when we populate the struct, instead of when defining it. An example:

```rust
fn main() {
    let intX: u32 = 5;
    let intY: u32 = 10;
    let intPoint: Point = Point { x: intX, y: intY };

    let floatX: f32 = 1.0;
    let floatY: f32 = 4.0;
    let float = Point { x: floatX, y: floatY };
}
```

We are creating two Point structures using the same struct. However, the first one is populated with coordinates of type u32, while in the second one we use f32. Generic data types allows us to do this in Rust.

Consider this other example:

```rust
struct Point<T> {
    x: T,
    y: T,
}

fn main() {
    let integer = Point { x: 5, y: 6.0 };   // error
}
```

This would throw an error because we are saying that the type of both *x* and *y* is T. However, when populating the struct we are giving two different types, a u32 for *x* and a f32 for *y*. Generic data types let us declare the type when populating the structure, but type T refers to exactly 1 type. If we wanted to use different types for coordinates *x* and *y* we could just define the Point struct with two type parameters, like this:

```rust
struct Point<T, U> {
    x: T,
    y: U,
}

fn main() {
    let integer = Point { x: 5, y: 6.0 };   // now this will work
}
```

There is a lot more to generic data types than this brief introduction. We encourage you to [take a look at 10.1 in the Rust book](https://doc.rust-lang.org/book/ch10-01-syntax.html) to learn how to parameterize things beyond structs, such as functions!

Now, let's look at Option and Result, two generic types in Rust that we used a lot throughout crustyDB.

## Option and Result

Option and Result are two generic data types which are extremely important in Rust and that we naturally use a lot in crustyDB. You really want to master these two!

### Option

```option``` is a generic enum in Rust, (we saw above generic structs, now you'll see generic enums) and it is useful when dealing with Null Values (or in place of nulls). The enum of ```Option<T>``` is defined by the std as:

```rust
enum Option<T> {
    Some(T),
    None,
}

let absent_number: Option<i32> = None;

//or

let y: Option<i8> = Some(5);
```

Overall, the option enum allows us to implement code that handles each variant:
- Use Some when you want code to run only why you have a ```Some(T)``` value
- Use ```None``` if you want code to run if you have a ```None``` value.

[Read more about Option in the Rust Book](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html?highlight=option#the-option-enum-and-its-advantages-over-null-values).

### Result

Result is similar to Option in that you are specifying an optional value, but instead of None we associate the result with an error type (which can indicate more about the error). 
```
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

[Read more about Result in the Rust Book](https://doc.rust-lang.org/book/ch09-02-recoverable-errors-with-result.html)

## unwrap(), the ? operator, and the panic! macro

In Rust, if you call panic!(), you will force the execution of the program to stop. You can optionally give panic!() a message that will be printed to standard output (e.g., your terminal or other output device you use to look at the code), like this:

```rust
fn test() {
  panic!("Not implemented!");
}
```

If you call the function test(), it will call panic!, which will in turn stop the execution of the program. In this case, we wrote panic!() because the function is not implemented and we wanted to indicate that in a rather dramatic way, by making sure the caller of test() notices it.

Note there is a way to recover or unwind from a panic, but we will not be using this in the class. Assume calling panic! will crash the program.

### unwrap and the ? operator

Suppose you call a function that returns a Result<T,E> type. How do you handle the result? If your Result<T,E> is in a variable named *result*, you can certainly handle that result using pattern matching:

```rust
match result {
    Ok(v) => { /* all good */},
    Err(e) => { /* some error occurred */},
}
```

And you could similarly handle a type Option<T> using pattern matching. However, pattern matching every Result and Option types in your code can get tedious if you use them often. unwrap and the ? operator will help you shorten the code.

When you use the *?* operator on a variable *result* of type Result<T,E>, this is roughly equivalent to:

```rust
match result {
    Ok(v) => v,
    Err(e) => return Err(e.into()),
}
```

so, if the result was Ok, then you just get the T variable. If there was an error, then you propagate the error to the caller of your function.

What about unwrap? if you call unwrap() on result, this is what happens:

```rust
match result {
    Ok(v) => v,
    Err(e) => panic!("Fatal error"),
}
```

So, if things go well, then both the ? operator and unwrap() will return the type the wrap. The crucial difference is that if things go wrong, if there is an error, the ? operator will return the error, hoping that the caller will handle it. The unwrap() function, on the other hand, will just panic!. unwrap() is assuming nobody can handle the error, so it stops the program execution.

Reasonable code will make use of both the ? operator and unwrap depending on how errors are handled. 

<!-- In crustyDB, we are very much still figuring out the best way of doing error handling, so you'll find both of these operators throughout. For now, you should just know what they mean, so you can interpret crusty's code and so you can use them when needed.

*Please note that this is the second iteration of CrustyDB, so the code is not yet mature. This means you may see differences in usage of Option, Result, unwrap, ?, etc. Sometimes this is intentional, sometimes not.* -->