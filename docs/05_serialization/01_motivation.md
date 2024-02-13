# Serialization Basics

## The Problem and Motivation

We start this module by motivating the problem of serialization and deserialization. For that, suppose you have implemented a program that implements a function ```mysterious(a: u32, b:u32) -> u64```.  

We use it in a program as follows:

```rust
let a = 5;
let b = 10;
let c = mysterious(a, b);
```

It does not matter what the function does, but we know that a call to `mysterious(2, 3)` will take about 3 hours to complete. After 3 hours we obtain a result. Because it is so expensive to run ```mysterious``` I may wish to store it (checkpoint) somewhere. That way, if my program crashes immediately after calling mysterious, or the lights go off, I do not need to repeat the computation again because I can just read the checkpoint. This is a common reason for one to *want to represent a value computed at runtime in durable storage*. There are other reasons. Perhaps, we would like to share that result with someone else. *Why* would we want to do that? and *How* do we do it?

### Why

There are many reasons. You may want to make `c` available to a process living in a different memory space (e.g., a different machine in the Internet), in which case you would like to store the content of `c` on disk, so they can access it from there. Or you may send the data directly to a different machine via the network. In general, you will work with programs that produce data that needs to be shared with someone else. The opposite is also true, you will work with programs that want to obtain data from an external source, such as disk or via the network, and work on that data. Databases are an example of such programs, but there are many many more.

### How

The following is a ***bad*** way of achieving the goal above of storing a value computed at runtime. If I want to make sure I keep the results of c after the program above finishes, I could print its value to the terminal and write it down on a piece of paper. Next time, if I want to use that value, I can make a program ask me for the value, and then I'll just copy it back from my piece of paper. This sounds awful. What if instead of one value I have multiple gigabytes of data? (you can roughly fit 678000 pages of text in one gigabyte -- that would be a lot of writing). And even if I write it, how do I send it to a different machine? What if I have many different variables that I would like to save instead of just one number? Doing this all manually sounds cumbersome and it is clearly not the way to go. The way to go is to use serialization and deserialization, which we explore next. 

## Serialization / Deserialization

Serialization consists of taking the contents of translating a data structure (or in its simplest form a variable, such as `c`) into a different format that can be interpreted by: i) the same program but during a different execution (e.g., after a crash or reboot); ii) a different program (e.g, to which we send the data via network, disk, or other); iii) a human. In addition, they may interpret this in the same machine or not.

### Human-readable serialization

We talk about human-readable serialization when we translate the contents of a program into a format that humans can interpret and understand. For example, I could obtain a string representation of the value `c` above and write that string into a file.txt that my operating system can open for me. Then, later, if a program wants to access the value of `c` *and it knows* that such a value is stored in file.txt, *and it knows* how to interpret the data stored inside file.txt, then it could read the content (as a string) and cast it into, e.g., a u32.

There are many other human-readable serialization formats. Take a look at JSON, YAML for some examples. The advantage of these formats is that they offer a bit of structure, so multiple different programs, written by different people, can read and write data and exchange it. This is exactly the goal we had initially.

### More efficient serialization

Human-readable serialization formats are easy to use by humans but less efficient to process by machines. The efficiency loss takes different dimensions. First, it often takes more space to store data in a human-readable way than not. Second, it often takes more time to translate data into human-readable formats and from human-readable formats, than not. If this is not clear, don't worry; we will briefly explore this at an intuitive level below.

Let's get hands-on and explore these ideas.






## Databases

Database management systems are in charge of, among many other things, storing and retrieving data efficiently. It follows that serializing and deserializing data is one of the most basic operations databases will perform. We will see a lot and you will deal with this a lot, so spend time ensuring you followed this module end to end.

## Post-credits Scene

Please review the notes from module 3 on result and option and pass the tests in crate result_option.

----
***ATTENTION: We introduce the third-party crate [serde], but you should not add any additional crates (e.g., do not modify the cargo.toml file) to pass the tests in this primer.***
