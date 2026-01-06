# Installation

The `rustup` installer and version management tool is the best way to download, 
install, and maintain the rust programming environment. Using the `rustup` 
command after installation will help you 
check for updates and update your Rust environment when necessary.

Depending on your operating system, you can install `rustup` by following the
instructions below:


::::{tab-set}
:::{tab-item} Linux or macOS
:sync: tab1
Enter the following command in terminal:

```bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```
:::

:::{tab-item} Windows
:sync: tab2
We recommend working with the Windows Subsystem for Linux (WSL) to install Rust on Windows.
Please follow the instructions from [Microsoft](https://learn.microsoft.com/en-us/windows/wsl/install).

Once you have WSL installed, open a WSL terminal and enter the following command:

```bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

:::{warning}
If you are unable to use WSL, you can install Rust directly on Windows by 
following the instructions on the 
[Rust website](https://www.rust-lang.org/tools/install). Our recommendation is 
to use WSL, as it will provide a more consistent experience with the rest of 
the guide.
:::
::::



<!-- ### Install ```rustup``` on Linux or macOS

### Install ```rustup``` on Windows


The rust installation scripts will typically generate a lot of terminal output.
A successful installation will return: 

```
Rust is installed now. Great! -->
<!-- ``` -->

## Update existing Rust environment

You can run:

```bash
rustc --version
```

to both check if you already have Rust installed, and if so, which version. If you don't have it installed, go above and follow the instructions to install it. If you already have a Rust environment installed, then you can update the version by doing:

```
rustup update
```


(rustlings-label)=
## Rustlings

[Rustlings](https://github.com/rust-lang/rustlings) is a collection of small exercises designed to help you get familiar with reading and writing Rust code. Throughout this guide, you'll find references to specific Rustlings exercises that complement the topics being discussed.

To install Rustlings, make sure you have Rust installed (see above), then run:

```bash
cargo install rustlings
```

Once installed, initialize Rustlings in a directory of your choice (make sure its not in any of your course homework or project folders):

```bash
rustlings init
```

This will create a `rustlings` directory with all the exercises.

To start rustlings, simply enter the following command within the ``rustlings`` folder:

```bash
rustlings
```

:::{admonition} Practicing Specific Rustlings Exercises
:class: tip

As you read the rust guide, you will find references to individual rustlings practice exercises, and they are not in the original order
of the rustlings exercises. If you'd like to run individual practice
problems, first start rustlings:

```bash
rustlings
```

And you can then hit the ``l`` key to **l**ist all the rustlings exercises and choose the relevant exercise.

Each exercise refers to a specific Rust (`.rs`) file within the `rustlings`
folder. Navigate to that specific Rust file and edit it, given the instructions
and the compiler message. 

When you save the file, rustlings will automatically
compile and run the file and check the output against the expected output. If 
your code is correct, it will respond with a success message. If not, the
compiler error or test result is provided to you, and you can fix your code to
complete the exercise gradually. 

It is recommended that you open the rustlings folder in VSCode and run the
rustlings command within a terminal session in VSCode. Any references to Rust 
files within the VSCode terminal can be visited by `Ctrl`-clicking (or `Cmd`-clicking on a Mac), making navigation and completing the rustlings exercises that much smoother.



For more information, as well as a live demo of the rustlings process, visit the [Rustlings Website](https://rustlings.rust-lang.org/).
:::
