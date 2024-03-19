# Hello World

Once you have installed the Rust development environment on your computer,
We can explain the process of creating a Rust project, writing a simple 
"Hello, World!" program, compiling it, and running it.

## Cargo
[Link to Rust documentation for cargo](https://doc.rust-lang.org/book/ch01-03-hello-cargo.html)

[Cargo]() is Rust's build system and package manager. It allows you to:

- Build your software
- Declare software dependencies your project needs
- Download those dependencies automatically

If you come from Python, and are familiar with  `pip` or `conda` or other environments to manage your dependencies, you'll find Cargo extremely useful. If you come from a JVM-based language such as Java or Scala, you'll find Cargo does much of what Maven/Gradle/Ant does for JVM languages, an all-in-one environment. 
And, if you come from C or C++ you may enjoy not having to deal with Makefile anymore :)

To make sure you have cargo installed, enter the following command into the terminal:
``` cargo --version ```

### Creating a Project (crate) with Cargo

To create a project with cargo, run the following commands, which create a `crate`. A crate is a package of code that can either be a binary (executable) or a library.

:::{warning}
Please run the following commands in a fresh directory, 
and not in your homework/project directory that already has code in it. 
Do not commit these files to your repository.
:::

```
cargo new hello_cargo
cd hello_cargo
```

In this example, we will be working with a new (binary) crate named hello_cargo. When you cd into the directory,
you should see that Cargo has generated two files:
- `Cargo.toml`
- `main.rs` file inside the src directory

Open `Cargo.toml` in a text editor. You should see the configuration information for the package, and the information that Cargo needs to compile your program. Make sure your name and email are correct.

```{code} toml
:filename: Cargo.toml
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Name <email@uchicago.edu>"]
edition = "2021"

[dependencies]
```

:::{note}
A few things to note:
- On newer versions of Rust, you will have to manually add the `authors` field.
- `edition` is the version of the Rust language that you are using.
:::

Next, open `src/main.rs`. You should see that Cargo has generated a Hello World program for you. 

```{code} rust
:filename: src/main.rs

fn main() {
    println!("Hello, world!");
}
```

### Building and Running a Cargo Project

 - To build your cargo project run: ``` cargo build ```
 - To build your cargo and run tests (and compile tests) run ```cargo test```
 - If you crate is a binary you can run it (and compile it) with: ``` cargo run ```
 - If you just want to check your code to see if it compiles, but don't want to run it, you can run ``` cargo check ```
 - To build your code with a higher level of optimization run ``` cargo build --release ``` This will take longer but result in 'faster' code. 

### Building a crate in a workspace

For our project, we are using a workspace, which is a collection of related crates. When code repositories grow large, workspaces are a great way of organizing code to make reading and modifying it easier. If you want to execute the build, test, run, etc. for a particular crate you add `-p <crate_name>` after the command. For example: `cargo test -p memstore` would just compile and execute the tests in the memstore crate (you'll soon what that is in the context of CrustyDB). If memstore depends on other crates (external or in the workspace), it would build them first.

Read more about Cargo in the [Rust Book](https://doc.rust-lang.org/book/ch14-00-more-about-cargo.html).