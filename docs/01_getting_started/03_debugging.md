# Debugging Rust Programs

Debugging is a crucial skill you should learn (if you don't know yet) in order
to become a more effective software developer. If you write software, your
software will contain bugs. Debugging is the process of finding those bugs,
which is necessary if you want to fix them.

### Debuggers

There are tools to help you debug software called debuggers. You may
have already heard about these. For example, in the C, C++ world, gdb and lldb
are two popular debuggers. gdb is used to debug programs that have been compiled
with gcc, while lldb is used to debug programs compiled with the LLVM toolkit.
What this means in practice, in 2020, is that if you work on a Linux platform,
you'll likely be using gdb. If you work on a Mac OS platform, you'll likely be
using lldb. If you work on a windows platform, then you may be using either one,
depending on your configuration.

### Debuggers in the IDE

A popular way of writing software is via IDEs (which we recommend you use to
develop crustyDB). IDEs for most languages come with a debugger preconfigured.
The situation for Rust is a little different. Only relatively recently IDE
developers have started incorporating debuggers for Rust, and the support is
still sparse. If you use Visual Studio Code (a lightweight and open source IDE),
you will be able to use a Rust debugger (based on gdb or lldb depending on the
underlying platform). You can easily find instructions online on how to set this
up.

Most other free IDEs do not have good support for the Rust debugger yet.

#### CLion

JetBrain's [CLion](https://www.jetbrains.com/clion/) IDE looks to have a solid Rust debugger with the Rust extension.
However CLion is not free, but it does offer academic licenses. [Apply here](https://www.jetbrains.com/community/education/#students)
if you want to access the tool (some restrictions on what you can use the tool for).
[Here are instructions on set up and using](https://blog.jetbrains.com/clion/2019/10/debugging-rust-code-in-clion/)
which worked for me out of the box on Ubuntu (with installing the Rust plugin).
One of our TAs uses CLion to debug Rust on OSX. The link also contains instructions for 
debugging on Windows, but it has not been tested by us.

#### VSCode

We have had some mixed success with using VSCode for debugging Rust
(although it is a great Rust IDE with the right extensions).  Using the
extensions `rust-analyzer` and CodeLLDB on Ubuntu has gotten debugging working on a set up.
We included the launch.json for running tests in a package.

### Alternative ways of debugging programs

You are already familiar with printing the values of variables in your programs
in order to understand program behavior and detect problems, i.e., in order to
debug your programs. Rust has its own println!() macro (and Crusty uses a
logging library). Rust also has a dbg!()
macro in its standard library, which will simply format the argument so its
printable along with the line where it's found.  A real debugger will give you
much more information, presented better, and in context, so it's a much more
powerful way of debugging programs, and the recommended way. However, in some
instances, the macros above may come in handy, especially as Rust's debuggers
support matures.
