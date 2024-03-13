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



## Rust Playground 
The [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021) is a web interface to try out small code snippets 