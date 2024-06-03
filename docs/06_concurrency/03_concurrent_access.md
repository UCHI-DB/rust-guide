# Concurrent Access

If you build a multi-threaded application, and multiple threads want to access the same data, many things can go wrong. You will want to synchronize and control the access to that data. Rust provides several types to indicate how you want to handle concurrency. We explain a few of those types below.

First, let us take a look at how you can provide a thread with ownership of a variable:

```rust
use std::thread;

fn main() {
    let v = vec![1, 2, 3];

    let handle = thread::spawn(move || {
        println!("Here's a vector: {:?}", v);
    });

    handle.join().unwrap();
}
```

The example contains a spawned thread which accesses a vector `v` inside the thread. Note that we have used the keyword `move` along with the function closure to indicate to the rust compiler to automatically take ownership any used values from the outer context. Once a value has been owned by the thread, it can no longer be used in the calling context (i.e. the main thread). However, we can use specialized primitives to share and protect access to data across threads, as will be demonstrated next. 

[Read more about move closures in the Rust book](https://doc.rust-lang.org/book/ch16-01-threads.html#using-move-closures-with-threads)

## mutex 

```Mutex``` is a mutual exclusion primitive useful for protecting shared data. With a mutex, you can make sure that only 1 thread access a piece of data at a time. Anything that wants to operate on the variable held by a mutex, must first acquire the mutex (lock). The mutex is valid for the scope it is defined/acquired. The mutex can be initialized or created with a ```new``` constructor.  For example: 

```rust
use std::sync::{Arc, Mutex}; 
use std::thread; 
use std::time::Duration; 
fn main()  
{ 
    let primes = Arc::new(Mutex::new(vec![1,2,3,5,7,9,13,17,19,23])); 
 
    for i in 0..10  
    { 
        let primes = primes.clone(); 
        thread::spawn(move ||  
        {  
            let mut data = primes.lock().unwrap(); 
            data[0] += i;  
        }); 
    } 
    thread::sleep(Duration::from_millis(50)); 
} 
```

We are creating 10 threads in the example above. Each thread has a reference to the vector primes. Because we have multiple references, we tell Rust to reference count them. Because these references are shared across different threads, we use Arc to indicate that. 

In addition, we want only 1 thread accessing the data at a time. To achieve that, we create a Mutex on the primes variable.

## RwLock

Imagine you have many threads that are reading a variable. You may let them read concurrently (as long as they do not modify the data, this may work for your application). However, if one wants to modify the contents (i.e., write), you want to make sure nobody is reading at the same time. If you were to use a Mutex only one thread could access the data, whether for reading or writing. To allow for concurrent reads, Rust provides a RwLock.

```RwLock``` stands for Reader-Writer lock. This type of lock allows a number of readers or at most one writer at any point in time. The write portion of this lock allows modification of the underlying data and the read portion allows for read-only shared access. For example:

```rust
use std::sync::RwLock;

let lock = RwLock::new(5);

// many reader locks can be held at once
{
    let r1 = lock.read().unwrap();
    let r2 = lock.read().unwrap();

} // read locks are dropped at this point

// only one write lock may be held, however
{
    let mut w = lock.write().unwrap();
    *w += 1;
} // write lock is dropped here
```

In this example, RwLock allowed us to have many reader locks, while only allowing access to one write lock. Most of the time when you have a RwLock, it will be wrapped in an Arc, as it meant to be shared across threads.

## Other Concurrency Primitives/ Tools

We are not covering them here, but in addition to `RwLocks`, Rust uses [`AtomicPrimitives`](https://doc.rust-lang.org/std/sync/atomic/) for safe concurrent access along with channels to use message passing between threads.


## Interior Mutability

From the Rust book '*Interior mutability is a design pattern in Rust that allows you to mutate data even when there are immutable references to that data; normally, this action is disallowed by the borrowing rules.*'  Using a variable like `Arc<RwLock<T>>` can allow you to use interior mutability on a struct, and within CrustyDB there will be points you may want to use such an approach.