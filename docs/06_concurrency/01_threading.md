# Threading in Rust

Similar to C, C++ and Java, Rust provides the ability to write multi-threaded programs which allows for concurrent execution of program code, and threads have the ability to read and write shared data, as we shall see soon. 

Threading in rust is handled via the `std::thread` library, which provides the 
ability to `spawn` threads. The thread `thread::spawn` function call takes in a function `closure`, which is an anonmyous function with associated context that can be saved in a variable and passed to other functions. The following example spawns a single thread which prints 10 lines, while the main thread prints 5 lines, and these can run concurrently. The closure is defined as a parameter to `thread::spwan` using the `|| {}` notation. 

```rust
use std::thread;
use std::time::Duration;

fn main() {
    let handle = thread::spawn(|| {
        for i in 1..10 {
            println!("hi number {} from the spawned thread!", i);
            thread::sleep(Duration::from_millis(1));
        }
    });

    for i in 1..5 {
        println!("hi number {} from the main thread!", i);
        thread::sleep(Duration::from_millis(1));
    }

    handle.join().unwrap();
}

```

[Read more about closures in the Rust book](https://doc.rust-lang.org/book/ch13-01-closures.html)

The example also shows the use of `thread:sleep` to force a thread to stop its execution for sometime. 

A call to the `thread::spawn` function returns a variable of type `JoinHandle`. This variable gives us a handle to the thread which we can use to interact with the thread and call the thread `join()` function. `join` forces the calling thread to wait for the execution of the thread pointed to by the handle to finish executing. In rust, when the main thread is done executing, the program exits, irrespective of any threads that have not finished executing, unless you force the execution to wait until all spawned threads have been joined using `join`. 

[Read more about Threads in the Rust book](https://doc.rust-lang.org/book/ch16-01-threads.html)