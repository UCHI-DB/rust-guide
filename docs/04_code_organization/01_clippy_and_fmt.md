# Linting Tools

## Clippy

A lint program (you will hear many people referring to these programs as linters) will inspect the code that you write in order to identify patterns that are problematic. What patterns are problematic? Generally, those that may lead to errors when you run your program. Notice, however, the crucial difference between a compiler, and a linter. The compiler will catch errors that make your program incorrect syntactically. The linter will complain even of syntactically correct programs (another difference is that the compiler will produce other code as output, while the linter will generally just indicate the improvement opportunities it has identified). The linter will offer suggestions to change your code to make it more readable and to get rid of problematic patterns that may be nevertheless syntactically correct.

In Rust, the main linter is [clippy](https://github.com/rust-lang/rust-clippy), which includes a collection of rules that will be tested against your code to indicate potential mistakes. You install clippy by doing:

``` 
rustup component add clippy
```

To run: ```cargo clippy```

Pay attention to the output. Clippy gives fairly detailed comments on your code, indicating the files and lines in those files where the problem is identified. In many cases, it will also suggest fixes. You should consider all these suggestions when working on your code.

## Rust Format

Rust format, ```rustfmt```, will take your code as input and reformat it so it follows a series of *style guidelines*. While would you want to follow somebody else's style guidelines? Well, one argument for it is that if everybody follows the same style guidelines, then all codes will look more alike, and as a consequence, it will be easier for everybody to understand each other's code. Because software engineering is a team effort, this seems a very compelling reason. Of course, what specific set of style guidelines to implement is a hotly-debated issue in each programming language community. Rust made a call and if you use rustfmt you will be following those style guidelines. You can install rustfmt by doing:

```
$ rustup component add rustfmt
```

Then, to reformat your code based on rustfmt's style guidelines simply do:
```
$ cargo fmt
```

After you have written some code, we encourage you to compare the before and after running rustfmt. Hint: use git diff (or the github visual tool) for large codebases.

In addition to rust format, there is another tool that may help you fix some compiler warnings. You can run:

```
$ cargo fix
```

These features can be very helpful, but it's important to make sure you are aware that it will update your code. 