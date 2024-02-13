# Implementations and Methods

## Implementations

The ```impl``` keyword is primarily used to define implementations on types. Both functions and consts can be defined in an implementation. For example, to implement a rectangle struct, we could do:

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}
```

This example allows us to call rectangle.area on an instance of the struct.

```rust
let rec = Rectangle{ 
    width=10,
    height=20,
};
println!("Rectangle Area: {}", rec.area());
```

## Methods

Methods are functions that are associated with a given type. Usually, the type is a ```struct```, and so you can think of methods as the functions you define to operate with the data represented by a struct. The first argument of methods will usually be a reference to the type on which they operate, via ```self, &self, or &mut self```. For example, if the method is defined over a struct, then self is the instance of the struct that the method is called on.

### Defining Methods

An example of how to define a method using the Rectangle struct is below.

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```
In this example, area is the function called in main, and used on ```rect1```, which we know is a Rectangle. Using & in front of our methods allows us to not take ownership, and rather borrow ```self``` immutably. 

Methods in an impl that do not take self as an argument are typically used for constructors, and return `Self` as a type. You invoke these functions by using the stuct name::function name (e.g. `Rectangle::new()`)

```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

    fn new_square_rect(n: u32) -> Self {
        Rectangle {
            width: n,
            height: n
        }
    }
}

let r = Rectangle::new_square_rect(4);
```

### Derive 

[Derive](https://doc.rust-lang.org/book/appendix-03-derivable-traits.html) is an annotation you can put on a struct that will automatically generate functions for the impl of the struct. Common derives will be debug (generate a string when called with {:?} in a string format), eq/partialEq (check equality), clone (create a deep copy), copy (stack only copy), hash (generate a hash code), and Ord/PartialOrd (comparing ordering).

If we wanted to generate equality checks and debug on our rectangle struct we would add

```
#[Derive(Debug, Eq, PartialEq)]
struct Rectangle {
    width: u32,
    height: u32,
}
```

and if r1 and r2 were Rectangles we could invoke code like:

```
if r1 == r2 {
    println!("Rectangles are the same {:?}", r1);
}
```