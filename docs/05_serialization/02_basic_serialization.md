# String and Byte Serialization

### Part 1: The very basics

Take a look at the crate `serde1` we include with this module. It is very simple, if you set the variable `serialize` to `true`, then it will take an integer, 33, and will serialize it. When serializing it, it will do it in two different ways. First, by casting 33 into a string, a human-readable representation. Second, by obtaining the bytes that represent the integer 33. After serializing the data, it will write it to disk. Instead, we could have chosen to send it over the network or to send it to another process, and many more: once data is represented as bits, *anyone who knows* how to interpret those bytes can translate them into variables again, in what is called deserialization.

This crate is extremely simple, feel free to play around, modify the code, and start honing your Rust programming skills. Also, these are the steps you should follow and questions you should answer (we indicate with to-submit answer you actually have to submit for the autograder to test your code):

* Implement the functions `serialize_to_string`, `serialize_to_bytes`, `deserialize_from_bytes` without changing the provided signature. (to-submit)
* After running the program once (for the first time), inspect the files that the program produces. What differences do you see between the files?
* Look at the comment on the `serialize_to_string` function. There is a question: what's the difference between casting into a string and serializing into a string? can you answer it?
* Investigate and try out alternative ways to serialize data in human-readable format, for example, in JSON. Instead of doing such a thing manually, you can look into existing libraries to achieve the goal.
* Above we explained some differences between human-readable serialization formats and more efficient ones (such as writing content in bytes), do you understand the difference now? can you explain it to someone else?
* What happens if you change the type of the integer? Try with `u16`, `i32`, `u8`... and observe its representation on disk. Make sure you understand the behavior.

The crux of serializing a data structure is to find a byte representation of the same. Different computer architectures, however, will interpret bits within a byte differently. Refresh your memory between the differences between *little endian* and *big endian*. You can find your computer architecture book or take a quick look at [the Wikipedia article on Endianness](https://en.wikipedia.org/wiki/Endianness).