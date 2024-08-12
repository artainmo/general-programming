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
    println!("Hello, world!"); // Using a ! means that we are calling a macro instead of a normal function
}
```
Complile the file `rustc main.rs` and execute `./main`. If you have a C or C++ background, you’ll notice that this is similar to gcc or clang. After compiling successfully, Rust outputs a binary executable.

Cargo is Rust’s build system and package manager. Cargo handles a lot of tasks, such as building your code, downloading the libraries your code depends on, and building those libraries (We call the libraries that your code needs dependencies).<br>
You can create a new directory/project with `cargo new projectName`. Inside that *projectName* directory you will find a 'Cargo.toml' configruation file and a 'src' directory with a 'main.rs' file. The main file should contain a main function which indicates the start of the program.<br>
With a Cargo project you can use `cargo build` to create an executable file in 'target/debug/projectName' and then execute that with `cargo run`. `cargo check` can be used to verify if code compiles without creating an executable. Another advantage of Cargo is that the commands are the same no matter the operating system. When the project is ready for release, you can use `cargo build --release` to compile it with optimizations for the Rust code to run faster, the executable will sit in 'target/release'.<br>
With simple projects, Cargo doesn’t provide a lot of value over just using rustc, but once programs grow to multiple files or need a dependency, it’s much easier to let Cargo coordinate the build.

### Common programming concepts
By default, variables are immutable, however, the option exists to make them mutable adding `mut` in front of the variable name.<br>
Constants are always immutable, they use the 'const' keyword instead of 'let' and do not accept the 'mut' keyword. When using 'const' you also need to indicate the variable's data type. Rust’s naming convention for constants is to use all uppercase with underscores between words such as `const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;`.<br>
You can declare a new variable with the same name as a previous variable. Rustaceans say that the first variable is 'shadowed' by the second, which means that the second variable is what the compiler will see when you use the name of the variable.<br>
```
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}"); // Outputs 12
    }

    println!("The value of x is: {x}"); // Outputs 6 because outside scope of one equal to 12
}
```
Shadowing is different from marking a variable as 'mut' because we’ll get a compile-time error if we accidentally try to reassign to this variable without using the 'let' keyword. The other difference between 'mut' and 'shadowing' is that because we’re effectively creating a new variable when we use the 'let' keyword again, we can change the type of the value but reuse the same name.

Rust is a statically typed language, which means that it must know the types of all variables at compile time. The compiler can usually infer what type we want to use. In cases when many types are possible, we must add a type annotation, like this `let guess: u32 = "42".parse().expect("Not a number!");` where 'u32' refers to an unsigned 32 bit integer.<br>
A scalar type represents a single value. Rust has four primary scalar types: integers, floating-point numbers, Booleans, and characters. For integers different types exist depending on the amount of bits and if unsigned or not such as 'i8', 'u16', 'i32', 'u64'... Floating-point numbers are indicated with 'f32' or 'f64'. Booleans are indicated with 'bool' and equal 'true' or 'false'. 'char' is used as alphabetic type, we specify them with single quotes, as opposed to string literals which use double quotes.<br>
Compound types can group multiple values into one type. Rust has two primitive compound types: tuples and arrays. A tuple is a general way of grouping together a number of values with a variety of types into one compound type. Tuples have a fixed length: once declared, they cannot grow or shrink in size. Unlike a tuple, every element of an array must have the same type. Unlike arrays in some other languages, arrays in Rust have a fixed length. Arrays are useful when you want your data allocated on the stack rather than the heap or when you want to ensure you always have a fixed number of elements. A vector is a similar collection type provided by the standard library that is allowed to grow or shrink in size.

We define a function in Rust by entering fn followed by a function name and a set of parentheses. The 'main' function is the entry point of the program. In function signatures, you must declare the type of each parameter.

Functions contain multiple lines of code, those can be statements or expressions. Statements don't return a value while expressions do. For example `let x = 3` is a statement and `let x = 5 + 7` is a statement containing an expression (5+7).
```
fn main() {
    let y = { // Will equal to 4.
        let x = 3;
        x + 1 // Expressions do not include ending semicolons. If you add a semicolon to the end of an expression, you turn it into a statement, and it will then not return a value.
    };
    println!("The value of y is: {y}");
}
```
Functions can return values to the code that calls them. We don’t name return values, but we must declare their type after an arrow (->).
```
fn five() -> i32 {
    5 // Because we do not use a semi-colon this is an expression that returns.
    // Alternatively to return we can use 'return 5;'
}
```

In Rust, the idiomatic comment style starts a comment with two slashes, and the comment continues until the end of the line. For comments that extend beyond a single line, you’ll need to include // on each line, like this:
```
// So we’re doing something complicated here, long enough that we need
// multiple lines of comments to do it! Whew! Hopefully, this comment will
// explain what’s going on.
```


## Resources
[The Rust Programming Language](https://doc.rust-lang.org/book/title-page.html)
