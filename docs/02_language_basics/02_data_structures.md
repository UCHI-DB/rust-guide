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
The Hashmap data structure is a common data structure that allows you to store
key-value pairs and look up values by key, typically in constant time. 
Rust features a built-in hashmap data structure (`HashMap`) 
that is part of the standard library. 

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

// Inserting Values into the HashMap
scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

// Accessing Values in the HashMap
let team_name = String::from("Blue");
let score = scores.get(&team_name).copied().unwrap_or(0);
```

While the access example above may seem a bit complex, it is a common pattern in Rust. 
The `get` function returns an `Option<&V>` type, which is a Rust `enum` that can be either `Some` or `None`.
If a value exists, a pointer (`&V`) to the value is returned, and we can make a copy of the value using the `copied` function.
Finally, we use the `unwrap_or` function to provide a default value if the key is not in the hashmap.


You will learn more about `Option` and enums in the [next module](enums).

More information on hashmaps is in the [Rust Book](https://doc.rust-lang.org/book/ch08-03-hash-maps.html)