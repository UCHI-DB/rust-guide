# Enums and Pattern Matching

# Enums
An ```enum``` is a data type that allows you to define a type by enumerating its possible variants. The options of an enum can optionally hold variables (primitive types, structs, or a tuple of values).  

Consider we have a message type that can either be a hello, goodbye, body, or wait. The body type has a string associated with it, and wait has an integer that specifies how long to wait.

```rust
enum Message {
    Hello,
    Goodbye,
    Body(String),
    Wait(String,u32)
}
```

Therefore when dealing with a message enum/variable you know it *must* be one of these four options, and if it is a body it must have a string and if it is a wait, it must have a u32.

```rust
let m1 = Message::Hello;
let m2 = Message::Body(String::from("Meet me at Medici"));
let m3 = Message::Wait(String::from("Seconds"), 10);
let m4 = Message::Goodbye;
```

# Match

If you are not used to languages with a pattern-matching feature, you'll love the transition to Rust. Match expressions allow you to compare a value against a series of patterns. 

For example, this match expression would print "three"

```rust
let x = 3;

match x {
    1 => println!("one"),
    2 => println!("two"),
    3 => println!("three"),
    4 => println!("four"),
    5 => println!("five"),
    _ => println!("something else"),
}
```

Rust also has a pattern we can use to match any value. The ```_``` pattern will match all possible cases that aren't specified before it. For example:

```rust
let x = 52;

match x {
    1 => println!("one"),
    2 => println!("two"),
    3 => println!("three"),
    4 => println!("four"),
    5 => println!("five"),
    _ => println!("something else"),
}
```

This would print "something else" because 52 does not match the other patterns listed.

Matching is common with enums as it ensures that all possible matches are accounted for (or at least a wildcard captures cases). Using our message example a match function like the following will cause an error as we do not match Message::{Goodbye,Wait,Body}

```rust
fn print_msg(m: Message) {
    match m {
        Message::Hello => {
            println!("Hi");
        }
    }
}
```

Instead we would want to match all Messages as follows. A few things to note, the code after the arm (=>) can be a code block { } or a single line, but both are followed by a , that separates the matches.  Also note that on the match of enum types that have store values, the values are available in a variable named after the type (e.g. `Message::Body(msg)` extracts the String which is available in the variable `msg` for the code block.).

```rust
fn print_msg(m: Message) {
    match m {
        Message::Hello => {
            println!("Hi");
        },
        Message::Goodbye => println!("Bye"),
        Message::Body(msg) => {
            println!("{}",msg);
        },
        Message::Wait(time,len) => println!("Waiting for {} {}",len,time)
    }
}
```

In the next module we will explore two common enums Option and Result.

### if let

Sometimes you want to only check a single condition, in this case writing an `if let` can be concise.

```rust
if let Message::Wait(time,len) = m3 {
    println!("Waiting for {} {}",len,time);
}
```

Matches are a powerful tool. You can use them when assigning variables or for returning from a function.

Read more about enums and matching in the [Rust Book](https://doc.rust-lang.org/book/ch06-00-enums.html)
