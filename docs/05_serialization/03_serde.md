# Serialization Formats

Through the previous sections, we have provided a glimpse into serialization and deserializaiton concerns. Now, consider a complex structure type that consists of many varied fields and, possibly, nested data types. You can imagine, however, how quickly serializing and deserializing such a complex datatype may become. 

Fortunately, we do not have to reinvent the wheel. We can instead rely on common serialization formats, which many programming languages support either through standard, or third-party libraries. Typical serialization formats are classified into two categories:

- Human-readable serialization formats (e.g., JSON, YAML) - As the name suggests, these formats are easy to read and write for humans. They are often used for configuration files, and data interchange between systems. JSON is particularly popular for web applications, and YAML is often used for configuration files.

- Binary / Compressed serialization formats (e.g., Bincode, CBOR) - These formats are less "verbose" than human readable formats, and can more efficiently store and transmit data. They are often used in high-performance applications, and in systems where storage and bandwidth are at a premium.`


## The `serde` crate

The [serde crate](https://crates.io/crates/serde), is a **framework** for serializing and deserializing data structures into common formats in Rust. It supports various data formats like [JSON](https://github.com/serde-rs/json), [Bincode](https://github.com/bincode-org/bincode), [CBOR](https://github.com/enarx/ciborium), [etc](https://serde.rs/#data-formats). You will find that we use serde crate to serialize logical query plans as json and tuples as vector in CrustyDB.

[Read more about serde crate](https://serde.rs/)