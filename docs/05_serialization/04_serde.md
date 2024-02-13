# The `serde` crate

Now, we have understood how serialization and deserialization works. You can imagine, however, how quickly serializing and deserializing complicated data structures (think nested structs, multiple data types) may become. Let's design and implement a great serde crate in part 3!! ... No panic, we don't have to [reinvent the wheel](https://en.wikipedia.org/wiki/Reinventing_the_wheel). You can see how critical is to perform this serde task correctly (so we can recover the data), and efficiently (in space and time), and how complicated. For that reason, most programming languages will have their own libraries for performing these tasks (sometimes the PL provides it in its standard library, othertimes there are external libraries, and often you will find both). Rust is no exception.

We introduce the [serde crate](https://crates.io/crates/serde), a **framework** for serializing and deserializing Rust data structures. It supports various data formats like [JSON](https://github.com/serde-rs/json), [Bincode](https://github.com/bincode-org/bincode), [CBOR](https://github.com/enarx/ciborium), [etc](https://serde.rs/#data-formats). You will find that we use serde crate to serialize logical query plans as json and tuples as vector in CrustyDB.

In the `serde3` crate, which is the final crate in this module, you need to import and use this external crate to serialize and deserialize JSON and CBOR data formats:

* Recalling the above questions, we have a collection of objects that represent universities, with attributes such as name, undergraduate_enrollment, schools (a list of school names), acceptance_rate, how would you serialize and deserialize this data to/from JSON format using serde crate? (to-submit)

* What if we need to do serialization and deserialization between CBOR and JSON?

After you finish the tasks, consider this open-end question:

* You probably have noticed the generality of serde crate, but what about efficiency? Find a way to compare the performance between serde create and your implementations in serde1&2.

[Read more about serde crate](https://serde.rs/)