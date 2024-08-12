# Rust

## Table of contents
- [Free tutorials](#Free-tutorials)
- [Resources](#Resources)

## Free tutorials
### Introduction
Rust is useful in allowing one to 'dip down' into lower-level control without risking crashes or security holes. But it is not limited to low-level systems programming, it can also be used to make command-line-interface apps and web servers.<br>
High-level ergonomics and low-level control are often at odds in programming language design, Rust challenges that conflict. Rust gives you the option to control low-level details (such as memory usage) without all the hassle traditionally associated with such control.<br>
Rust provides speed and stability. Speed both in terms of writing and executing.<br>
Rust basically is a general-purpose, high-level programming language with detailed control as found in a low-level programming language. Thus Rust tries to be it all. 

To create a 'Hello, world!' program, first create a source file named 'main.rs'. Then use the following code.<br>
```
fn main() {
    println!("Hello, world!"); # Using a ! means that we are calling a macro instead of a normal function
}
```
Complile the file `rustc main.rs` and execute `./main`. If you have a C or C++ background, you’ll notice that this is similar to gcc or clang. After compiling successfully, Rust outputs a binary executable.

Cargo is Rust’s build system and package manager. Cargo handles a lot of tasks, such as building your code, downloading the libraries your code depends on, and building those libraries (We call the libraries that your code needs dependencies).<br>
You can create a new directory/project with `cargo new projectName`. Inside that *projectName* directory you will find a 'Cargo.toml' configruation file and a 'src' directory with a 'main.rs' file. The main file should contain a main function which indicates the start of the program.<br>
With a Cargo project you can use `cargo build` to create an executable file in 'target/debug/projectName'.


## Resources
[The Rust Programming Language](https://doc.rust-lang.org/book/title-page.html)
