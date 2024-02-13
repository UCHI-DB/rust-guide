# Ownership

## Understanding Memory Allocation

All programs need to allocate memory to do computation. In higher-level,
byte-code based or scripting languages such as Java, Python and Javascript, code
is interpreted and memory is automatically managed during the lifetime of the
program. In lower-level languages such as C, you will be familiar with
the `malloc` (memory allocation) function to achieve that goal. As a reminder,
if you want to dynamically allocate memory in C, you would use `malloc()` to request
a pointer to a block of memory of a specified size. When you are done 
with the memory block, you are expected to use `free()` to release the memory
block pointed to by the pointer.

If a program allocates memory and never 'frees' it after using it, it will soon exhaust the
machine's memory leading to a crash. In C-like environments developers are in charge
of allocating memory and freeing it when no longer necessary. This gives
developers full control at the expense of increased complexity. Reducing that
complexity is not just a matter of convenience, but of security and safety as
well. In response to the complexity of manual memory allocation, some language
runtimes incorporate a garbage collector. With a garbage collector, developers
no longer need to allocate and free memory explicitly. Instead, memory is
allocated on demand as you declare variables, and the garbage collector will
search for references to memory that is no longer used and free them
transparently to the developer. This increased convenience comes at the cost of
performance.

Improper memory management can also lead to security vulnerabilities such as buffer
overflows, use-after-free, and memory leaks. These vulnerabilities can be
exploited by attackers to execute arbitrary code, crash the program, or leak
sensitive information. This was the primary motivation for the development of
the Rust programming language, by Mozilla Research.

## Rust's Memory Ownership Model

Rust aims to help developers write safe programs without using a garbage collector. Striking a balance between convenience and performance. Developers only need to learn a few additional concepts to take full advantage of Rust's powerful model. The concept of ownership is at the center of it all.

To recap: Ownership is one of the most important and unique features of Rust; it allows Rust to be memory-safe and efficient without needing a garbage collector. 

In Rust, whether the value is on the stack or the heap is important to understand how Rust behaves as a language. This is where ownership comes in. 

:::{hint} Ownership Rules:
- Each value in Rust is bound to variable that's called its **owner**
- There can only be one **owner** at a time
- When the **owner** goes out of scope, the value will be dropped

:::

For example, when you assign a value to a variable, that variable becomes the value's sole owner.

```rust
fn main() {
    let x = String::from("hello");
}
```

Now, let's say we define a new owner of x's values:

```rust
fn main() {
    let x = String::from("hello");
    let y = x;
}
```

This reassignment of ownership is known as a **move**. A move causes the former assignee to become uninitialized, and therefore cannot be usable in the future.

The last rule of ownership deals with scope. When a variable goes out of scope, its associated value is dropped. For as long as a variable remains in scope, the value it owns will never be dropped. For example:

```rust
fn main() {
    {
        let x = 24;
    }
    println!("x: {}", x);  //ERROR: x is no longer in scope
}
```

## References and borrowing

References and borrowing allows developer to use variables without taking ownership.

### Borrowing

To **borrow** a value without taking ownership of a value, you can add an 
ampersand (`&`) to the value. 
Remember that `!vec` is a macro that creates a new vector.

```rust
fn main() {
    let numbers = vec![1, 2, 3, 4];
    // Borrow the numbers by using &numbers
    let borrowed_numbers = &numbers; 
    // Now, you are able to use borrowed_numbers with no error
    for number in borrowed_numbers.iter() {
        println!("Number: {}", number);
    }

}
```

### References

Rust lets us pass values to functions by reference, or by copying the value itself.

1. If a value implements a Copy and is not borrowed, it will be passed by value (copied)
2. If a value implements a Copy and is borrowed, it will be passed by reference
3. If a value does not implement a Copy, it must be borrowed to be passed by reference

For example, consider different ways of checking whether a number is negative or a vector empty using references and copies:

```rust
fn pass_number_by_reference(number_arg: &i8) -> bool {
    number_arg.is_negative()
}

fn pass_number_by_value(number_arg: i8) -> bool {
    number_arg.is_negative()
}

fn pass_vec_by_reference(vec: &Vec<i8>) -> bool {
    vec.is_empty()
}

fn main() {
    // numbers implement Copy, and so can be passed by value or reference
    let number = 42;

    // pass by reference
    // does not move number because of borrow
    let is_negative_by_ref = pass_number_by_reference(&number);
    
    // pass by value
    // the `number` is copied to `number_arg`
    // so `number` and `number_arg` are two independent variable at two places in memory.
    let is_negative_by_value = pass_number_by_value(number);

    // copy not implemented - must be passed by reference
    let vec = vec![];

    // does not move vec
    let is_empty = pass_vec_by_reference(&vec);
}
```

As you can see, the comments above the functions are a good description of the relationship between ownership, referencing, and borrowing. 

### Dereference

Now that we saw how to reference values, you may wonder how to do the opposite, to *dereference*. In Rust, we dereference using the `*` operator. Let's look at some examples.

```rust
fn main() {
    let number = 42;
    let r = &number;  // `r` is a reference to `number`
    assert!(*r == 42);  // explicitly dereference `r`
}
```

Using a `&` (also called "shared reference") allows us to read its referent by dereferencing (using the `*` operator). But to both read and modify a value, we need to have a *mutable reference* to the value. For example:

```rust
fn main() {
    let mut number = 42;  // number is now mutable
    let m_r = &mut number;  // `m_r` is a mutable reference to `number`
    *m_r += 10;  // dereference m_r to set a new value to `number`
    assert!((*m_r == 52) && (number == 52));  // check `number`'s new value
}
```

Read more in the [Rust book](https://doc.rust-lang.org/stable/book/ch15-02-deref.html).

### The Slice Type

Rust also allows you to reference values using slicing. Slicing applies to collection types such as string, or list. From the Rust book "*Another data type that does not have ownership is the slice. Slices let you reference a contiguous sequence of elements in a collection rather than the whole collection.*"

For example:
 
```rust
let s = String::from("hello");

// You can slice from a range
let slice = &s[0..2];

// Or you can slice the whole string
let slice = &s[..];
```

## Lifetimes

Any reference has a lifetime that indicates how long the reference is valid. Most of the time this will be inferred by the rust compiler, but it can be explicitly given. We have avoided using lifetimes when possible in our project to simplify the code. This results in using smart pointers more than is ideal. You can read more about lifetimes [here](https://doc.rust-lang.org/book/ch10-03-lifetime-syntax.html), so you are familiar with the idea by the time you encounter them in Crusty's codebase.


## References
- Rust Documentation
    - [Ownership](https://doc.rust-lang.org/book/ch04-00-understanding-ownership.html)
