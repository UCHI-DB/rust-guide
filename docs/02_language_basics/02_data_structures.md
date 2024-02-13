# Simple Data Structures

Rust has many useful data structures built into the language. Two common data structures you are likely to use / encounter are vectors and hashmaps. A vector (vec) is a growable list/array. A hashmap is an associative map that lets you insert and look up structs/variables by a key.

## Vec

Vectors allow you to insert elements into them (push), iterate through elements in the vector, get an element from the vector, and remove the last element (pop). See the [API](https://doc.rust-lang.org/std/vec/struct.Vec.html) for the full set of functions.

```rust
let mut v: Vec<i32> = Vec::new();    
v.push(5);
v.push(6);
v.push(7);
v.push(8);

//Use &v to borrow the vector -- we'll see in Module 2 what 'borrow' means in Rust
for x in &v {
    println!("{}", x);
}

// assert_eq! checks two values are equal. We will cover Some later.
assert_eq!(v.pop(), Some(8));
// Check the length of the vec
assert_eq!(v.len(), 3);
```

A macro, `vec!`, exists for quickly building a vector
`let mut v = vec![1, 2, 3];`

## Hashmap 

Read the documentation on hashmaps when you need to use them
https://doc.rust-lang.org/book/ch08-03-hash-maps.html