# Crates and Imports

Organization and using code in a project always take a little bit to get used to. Rust overall is very clean in how it organizes projects/cargo/code. We will try to provide a brief overview here, but you likely will want to read the [Rust Book's chapter on this](https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html)

If you want to use a crate (external or as part of a workspace), the crate needs to be added to the `Cargo.toml` file (under `[dependencies]`).

Within a crate, modules (no relation to our use of module in this primer) organize code and provide privacy/visibility. The keyword `mod` is what creates a module. This can either be as a code block or as a file/folder. By default, Rust/Cargo looks a main.rs (for binary crates) or lib.rs (for library crates). Within this default file, additional modules are imported/added to the crate. If we are in lib.rs, a line like `mod supercode;` tells rust to look for a file supercode.rs in the same directory as lib.rs or for folder supercode/ with mod.rs file in it. Within this crate (or other crates if we make the module public via `pub mod supercode;`) we can now `use` code in this module (with the right visibility).

Within a rust file to use any function, struct, or variable defined in another crate, part of the rust standard library, or a module in the crate you need bring it into scope with keyword `use`. 

```rust
// use a function defined in the module supercode in this crate
use crate::supercode::my_spec_fn;

// use hashmap from the standard library
use std::collections::HashMap;

// use code from a crate common
use common::great_struct;

my_spec_fn();
let a = great_struct::GS;
```