## Shared Ownership

One of the unique characteristics of Rust as a programming language, [is its notion of ownership](https://doc.rust-lang.org/book/ch04-00-understanding-ownership.html). In Rust, if you want to share a variable, (e.g., passing it as argument, using it to compute another variable, or using it as the return value of a function), you will have to think about ownership. There are a few concepts that we use in crustyDB and that are related to how we handle references in Rust. We give an overview of those here.

A key thing to keep in mind for the discussion that follows is that whenever you allocate a variable, you want to keep track of all existing references to that variable so that when there are no more references left, you can deallocate the variable. While in some languages, such as Java and C#, there is a garbage collector that takes care of counting and handling references automatically and transparently for you, in Rust there is no garbage collector. This means that someone must take care of incrementing the reference counter when new references are created, and ensuring the data is dropped only when the reference counter is zero. In Rust, the compiler will take care of doing this for you, as long as you give it enough information. If you create a reference in Rust, it'll get deallocated, by default, when the reference goes out of scope.  If you want to keep that reference around, (e.g., because you've shared it), how do you achieve that? The types we discuss below give you some primitives and tools to handle this. While we do not expect you to understand all the details of these types right now, we hope this guide will help you become a bit more familiar with them, so you will understand and interpret them when you find them in crustyDB.


## Rc 

'[Rc](https://doc.rust-lang.org/book/ch15-04-rc.html)' stands for reference counted. 'Rc' is a type, ```Rc<T>```, that provides *shared* ownership of a value of type T. ```Rc<T>``` automatically deferences to T, and you can call any of T's methods on a value of type ```Rc<T>```.  For example, consider a scenario where we have ```Objects``` that are owned by a given ```Owner```. We want to have our ```Objects``` point to their ```Owner```. We can't do this with ownership because one or more ```Objects``` could belong to the same owner. In this scenario, ```Rc``` allows us to share ownership over multiple ```Objects```. 

```rust
use std::rc::Rc;

struct Owner {
    name: String,
    // ...other fields
}

struct Object {
    id: i32,
    owner: Rc<Owner>,
    // ...other fields
}

fn main() {
    // Create a reference-counted `Owner`.
    let object_owner: Rc<Owner> = Rc::new(
        Owner {
            name: "name".to_string(),
        }
    );

    // Create `Object`s belonging to `object_owner`. Cloning the `Rc<Owner>`
    // gives us a new pointer to the same `Owner` allocation, incrementing
    // the reference count in the process.
    let object1 = Object {
        id: 1,
        owner: Rc::clone(&object_owner),
    };
    let object2 = Object {
        id: 2,
        owner: Rc::clone(&object_owner),
    };


    println!("Object {} owned by {}", object1.id, object1.owner.name);
    println!("Object {} owned by {}", object2.id, object2.owner.name);

}
```

## Arc 

```Arc``` stands for Atomic Reference Counted, and is similar to ```Rc```, ```Arc``` lets you share data across different owners. In contrast to Rc, Arc allows you to share references across *threads* and ensures that the reference lives as long as the last owner survives--as opposed to the reference being deallocated when it gets out of scope. A quick way of choosing between Arc and Rc is the following: will you use the reference across threads? if the answer is yes, you probably want to use Arc, if the answer is no then you probably want to use Rc.