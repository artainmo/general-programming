# Rust

## Table of contents
- [Free tutorials](#Free-tutorials)
    - [Introduction](#introduction)
    - [Common programming concepts](#Common-programming-concepts)
    - [Understanding Ownership](#Understanding-Ownership)
    - [Using Structs to structure related data](#Using-Structs-to-structure-related-data)
    - [Enums and pattern matching](#Enums-and-pattern-matching)
    - [Managing growing projects with Packages, Crates, and Modules](#managing-growing-projects-with-packages-crates-and-modules)
    - [Common Collections](#Common-Collections)
    - [Error Handling](#Error-Handling)
    - [Generic Types, Traits, and Lifetimes](#generic-types-traits-and-lifetimes)
    - [Writing automated tests](#Writing-automated-tests)
    - [Functional Language Features: Iterators and Closures](#functional-language-features-iterators-and-closures)
    - [More About Cargo and Crates.io](#more-about-cargo-and-cratesio)
    - [Smart pointers](#Smart-pointers)
    - [Fearless Concurrency](#Fearless-Concurrency)
    - [Object-Oriented Programming Features of Rust](#object-oriented-programming-features-of-rust)
    - [Patterns and Matching](#Patterns-and-Matching)
    - [Advanced Features](#Advanced-Features)
        - [Unsafe Rust](#Unsafe-Rust)
        - [Advanced Traits](#Advanced-Traits)
        - [Advanced Types](#Advanced-Types)
        - [Advanced Functions and Closures](#Advanced-Functions-and-Closures)
        - [Macros](#Macros)
    - [Appendix](#Appendix)
        - [Appendix A: Keywords](#appendix-a-keywords)
        - [Appendix B: Operators and Symbols](#appendix-b-operators-and-symbols)
        - [Appendix C: Derivable Traits](#appendix-c-derivable-traits)
        - [Appendix D: Useful Development Tools](#appendix-d-useful-development-tools)
        - [Appendix E: Editions](#appendix-e-editions)
        - [Appendix G: How Rust is Made and “Nightly Rust”](#appendix-g-how-rust-is-made-and-nightly-rust)
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
Compile the file `rustc main.rs` and execute `./main`. If you have a C or C++ background, you’ll notice that this is similar to gcc or clang. After compiling successfully, Rust outputs a binary executable.

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

An if expression allows you to branch your code depending on conditions.
```
if number % 4 == 0 {
    println!("number is divisible by 4");
} else if number % 3 == 0 {
    println!("number is divisible by 3");
} else if number % 2 == 0 {
    println!("number is divisible by 2");
} else {
    println!("number is not divisible by 4, 3, or 2");
}
```
'if' is an expression, we can use it on the right side of a let statement to assign the outcome to a variable. For example `let number = if true { 5 } else { 6 };`.

Rust has three kinds of loops: loop, while, and for.<br>
The loop keyword tells Rust to execute a block of code over and over again forever or until you explicitly tell it to stop.<br>
```
fn main() {
    loop {
        println!("again!");
    }
}
```
Fortunately, Rust also provides a way to break out of a loop using code. You can place the `break` keyword within the loop to tell the program when to stop executing the loop. `continue` in a loop tells the program to skip over any remaining code in the current iteration of the loop and go to the next iteration.<br>
The result of a loop can be given to a variable.
```
let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };
```
If you have loops within loops, break and continue apply to the innermost loop at that point. You can optionally specify a loop label on a loop that you can then use with break or continue to specify that those keywords apply to the labeled loop instead of the innermost loop.
```
'counting_up: loop { // We use one single quote to indicate the loop label.
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
```
The 'while' loop runs as long as the condition is true.
```
let mut number = 3;

while number != 0 {
    println!("{number}!");
    number -= 1;
}
```
A 'for' loop can execute code for each item in a collection.
```
let a = [10, 20, 30, 40, 50];

for element in a {
        println!("the value is: {element}");
}
```
We can also use for to loop over a range.
```
for number in (1..4) {
        println!("{number}!");
}
```

### Understanding Ownership
Ownership is Rust’s most unique feature and has deep implications for the rest of the language. It enables Rust to make memory safety guarantees without needing a garbage collector.

Ownership is a set of rules that govern how a Rust program manages memory. All programs have to manage the way they use a computer’s memory while running. Some languages have garbage collection that regularly looks for no-longer-used memory as the program runs, in other languages, the programmer must explicitly allocate and free the memory. Rust uses a third approach, memory is managed through a system of ownership with a set of rules that the compiler checks. If any of the rules are violated, the program won’t compile.

Many programming languages don’t require you to think about the stack and the heap very often. But in a systems programming language like Rust, whether a value is on the stack or the heap affects how the language behaves and why you have to make certain decisions.<br>
Both the stack and the heap are parts of memory available to your code to use at runtime, but they are structured in different ways. The stack stores values in the order it gets them and removes the values in the opposite order. This is referred to as last in, first out. All data stored on the stack must have a known, fixed size. Data with an unknown size at compile time or a size that might change must be stored on the heap instead. The heap is less organized: when you put data on the heap, you request a certain amount of space. The memory allocator finds an empty spot in the heap that is big enough, marks it as being in use, and returns a pointer, which is the address of that location. This process is called allocating on the heap. Because the pointer to the heap is a known, fixed size, you can store the pointer on the stack, but when you want the actual data, you must follow the pointer. Pushing to the stack is faster than allocating on the heap because the allocator never has to search for a place to store new data, that location is always at the top of the stack. Accessing data in the heap is slower than accessing data on the stack because you have to follow a pointer to get there.<br>
When your code calls a function, the values passed into the function (including, potentially, pointers to data on the heap) and the function’s local variables get pushed onto the stack. When the function is over, those values get popped off the stack. However, values stored on the heap need to be removed manually when not in use anymore.<br>
The main purpose of ownership is to manage heap data.

In Rust, each value has an owner, there can only be one owner at a time, when the owner goes out of scope the value will be dropped. Here is an example of a variable's scope.
```
{                          // s is not valid here, it’s not yet declared
        let s = "hello";   // s is valid from this point forward

        // do stuff with s
}                          // this scope is now over, and s is no longer valid
```
The types covered previously are of a known size, can be stored on the stack and popped off the stack when their scope is over. The 'String' data type is stored on the heap to allow storage of an amount of text that is unknown at compile time. You can create a 'String' from a string literal using the from function, like so `let s = String::from("hello");`. The double colon :: operator allows us to namespace this particular 'from' function under the 'String' type. This kind of string can be mutated:
```
let mut s = String::from("hello");
s.push_str(", world!");
```
In languages with a garbage collector (GC), the GC keeps track of and cleans up memory that isn’t being used anymore. In most languages without a GC, it’s our responsibility to identify when memory is no longer being used and to call code to explicitly free it, just as we did to request it. Doing this correctly has historically been a difficult programming problem. If we forget, we’ll waste memory. If we do it too early, we’ll have an invalid variable. If we do it twice, that’s a bug too. Rust takes a different path: the memory is automatically returned once the variable that owns it goes out of scope.

In the following code a variable containing an integer is copied into another variable. Thus both variables will hold the value 5 but in different memory spaces which we call a deep copy. This is possible because integers use the stack which can create copies fast.
```
let x = 5;
let y = x;
```
However, because 'String' uses the heap it won't create a deep copy instead a shallow copy which consists of the second variable pointing to the same heap memory space. This could create a double-free problem if both variables are freed while they point to the same memory location. To resolve this problem Rust makes the first 'String' variable invalid, thus we can talk about 'moving' instead of really shallow copying.
```
let s1 = String::from("hello");
let s2 = s1;

println!("{s1}, world!"); // This will create a compilation error because s1 has been made invalid.
```
If we do want to deeply copy the heap data of the 'String', not just the stack data, we can use a common method called `clone`.
```
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {s1}, s2 = {s2}"); // This works just fine.
```
Passing a variable to a function will move or copy, just as assignment does.
```
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // x would move into the function,
                                    // but i32 is Copy, so it's okay to still
                                    // use x afterward

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{some_string}");
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{some_integer}");
} // Here, some_integer goes out of scope. Nothing special happens.
```
If we tried to use 's' after the call to 'takes_ownership', Rust would throw a compile-time error, this because its value got 'moved' to the function.<br>
Returning values from a function can also transfer ownership. Rust does let us return multiple values using a tuple.

A reference is like a pointer in that it’s an address we can follow to access the data stored at that address, that data is owned by some other variable.<br>
Here is an example where we use references to avoid the need to move ownership.
```
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1); # We use & to indicate reference.

    println!("The length of '{s1}' is {len}."); // Because s1 didn't get moved to the calculate_length function we can still use it.
}

fn calculate_length(s: &String) -> usize { // We use & to indicate reference.
    s.len()
}
```
We call the action of creating a reference borrowing. Like variables, references too are immutable by default. However, references can also use the 'mut' keyword to become mutable.
```
fn main() {
    let mut s = String::from("hello");

    change(&mut s); // &mut is used to indicate a mutable reference
}

fn change(some_string: &mut String) { // &mut is used to indicate a mutable reference
    some_string.push_str(", world");
}
```
Mutable references have one big restriction, if you have a mutable reference to a value, you can have no other references to that value. As always, we can use curly brackets to create a new scope, allowing for multiple mutable references, just not simultaneous ones.<br>
References pointing to deallocated variables will create compilation errors.

Slices let you reference a contiguous sequence of elements in a collection rather than the whole collection. A collection is a dynamic data sequence on the heap such as a String or Vector. A slice is a kind of reference, so it does not have ownership.<br>
A String Slice is a reference to a part of a String, and it looks like `let hello = &s[0..5];`. To indicate up to last element `&s[3..]`. Arrays are spliced in a similar way.

### Using Structs to structure related data
A struct, or structure, is a custom data type that lets you package together and name multiple related values that make up a meaningful group. If you’re familiar with an object-oriented language, a struct is like an object’s data attributes.<br>
To define a struct, we enter the keyword struct and name the entire struct.
```
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}
```
To use a struct after we’ve defined it, we create an instance of that struct by specifying concrete values for each of the fields.
```
fn main() {
    let mut user1 = User { // The 'mut' keyword indicates the values inside the structure are mutable.
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };
}
```
To get a specific value from a struct, we use dot notation. For example, to access this user’s email address, we use `user1.email`.<br>
Tuple structs are named tuples, its attributes are not named. They are defined and instanciated like this.
```
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```
Unit-like structs are structs without any fields, they are useful when you need to implement a trait on some type but don’t have any data that you want to store in the type itself. Traits will be discussed later. They are defined like this `struct AlwaysEqual;`.<br>
Methods are similar to functions, but unlike functions, methods are defined within the context of a struct (or an enum or a trait which will be discussed later), and their first parameter is always 'self', which represents the instance of the struct the method is being called on.<br>
```
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle { // This implementation block is used to define methods of Rectangle struct. 
    fn area(&self) -> u32 { // The '&self' is actually short for 'self: &Self'. We don’t want to take ownership, and we just want to read the data in the struct, not write to it. If we wanted to change the instance that we’ve called the method on as part of what the method does, we’d use '&mut self' as the first parameter.
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area() // We call the struct method.
    );
}
```
All functions within 'impl' block can be called associated functions because they are associated with a certain struct/type. Associated functions that have 'self' as first parameter are methods. Associated functions that aren’t methods are often used for constructors that will return a new instance of the struct.
```
impl Rectangle {
    fn square(size: u32) -> Self { // 'Self' keywords in the return type and in the body of the function are aliases for the type that appears after the 'impl' keyword, which in this case is 'Rectangle'.
        Self {
            width: size,
            height: size,
        }
    }
}
```
To call this associated function, we use the '::' syntax with the struct name `let sq = Rectangle::square(3);`. The '::' syntax is used for both associated functions and namespaces created by modules. We’ll discuss modules later.<br>
Each struct is allowed to have multiple 'impl' blocks.

### Enums and pattern matching
Enums allow you to define a type by enumerating its possible variants. Enums give you a way of saying a value is one of a possible set of values.<br>
Any IP address can be either a version four or a version six address, but not both at the same time. That property of IP addresses makes the enum data structure appropriate because an enum value can only be one of its variants. Such as enum would be defined and instanciated like this.
```
enum IpAddrKind {
    V4,
    V6,
}

let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```
We can put data directly into each enum variant.
```
enum IpAddr {
        V4(String),
        V6(String),
}

let home = IpAddr::V4(String::from("127.0.0.1"));
let loopback = IpAddr::V6(String::from("::1"));
```
Just as we’re able to define methods on structs using 'impl', we’re also able to define methods on enums.<br>
Rust doesn’t have the 'null' feature that many other languages have. 'null' is a value that means there is no value there. In languages with 'null', variables can always be in one of two states: 'null' or 'not-null'. The problem with 'null' values is that if you try to use a 'null' value as a 'not-null' value, you’ll get an error of some kind. Rust does not have 'nulls', but it does have an enum that can encode the concept of a value being present or absent. This enum is `Option<T>`, and it is defined as follows.
```
enum Option<T> {
    None,
    Some(T),
}
```
The Option<T> enum is so useful that it’s even included in the prelude, you don’t need to bring it into scope explicitly. `<T>` is a generic type that can take any type, we will cover it later.
```
let some_number = Some(5);
let some_char = Some('e');
let absent_number: Option<i32> = None;
```
When we have a 'Some' value, we know that a value is present and the value is held within the 'Some'. When we have a 'None' value, in some sense it means the same thing as 'null'. For 'absent_number', Rust requires us to annotate the overall 'Option' type as the compiler can’t infer the type that the corresponding 'Some' variant will hold by looking only at a 'None' value.

Rust has an extremely powerful control flow construct called match that allows you to compare a value against a series of patterns and then execute code based on which pattern matches.
```
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin { // The match construct verifies what variant the enum is.
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```
If you want to run multiple lines of code in a match arm, you must use curly brackets, and the comma following the arm is then optional.
```
fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => {
            println!("Lucky penny!");
            1
        }
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```
'_' is a special pattern that matches any value and does not bind to that value. '()' indicates no code to run.
```
let dice_roll = 9;
match dice_roll {
    3 => add_fancy_hat(),
    7 => remove_fancy_hat(),
    _ => (),
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
```

The 'if let' syntax lets you combine 'if' and 'let' into a less verbose way to handle values that match one pattern while ignoring the rest. It is shorter than using match by only verifying one pattern.
```
let config_max = Some(3u8);
if let Some(max) = config_max {
    println!("The maximum is configured to be {max}");
}
```
The syntax 'if let' takes a pattern and an expression separated by an equal sign. It works the same way as a match. In this case, the pattern is 'Some(max)', and the 'max' binds to the value inside the 'Some'. We can then use 'max' in the body of the 'if let' block. The code in the 'if let' block isn’t run if the value doesn’t match the pattern.<br>
'else' can also be used after the 'if let'.
```
let mut count = 0;
if let Coin::Quarter(state) = coin {
    println!("State quarter from {state:?}!");
} else {
    count += 1;
}
```

### Managing growing projects with Packages, Crates, and Modules
As you write large programs, organizing your code will become increasingly important. By grouping related functionality and separating code with distinct features, you’ll clarify where to find code that implements a particular feature and where to go to change how a feature works.

A crate is the smallest amount of code that the Rust compiler considers at a time. Crates can contain modules, and the modules may be defined in other files that get compiled with the crate.<br>
A crate can come in one of two forms: a binary crate or a library crate. Binary crates are programs you can compile to an executable, such as command-line programs, they must have a 'main' function. Library crates don't have a 'main' function and don't compile to an executable, instead they define functionality shareable with multiple projects.<br>
A package is a bundle of one or more crates that provides a set of functionality. A package contains a Cargo.toml file that describes how to build those crates. A package can contain as many binary crates as you like, but at most only one library crate.

Modules let us organize code within a crate for readability and easy reuse. Modules also allow us to control the privacy of items because code within a module is private by default. We can choose to make modules and the items within them public, which exposes them to allow external code to use and depend on them.<br>
We define a module with the 'mod' keyword followed by the name of the module. The body of the module then goes inside curly brackets. Inside modules, we can place other modules.
```
mod front_of_house {
    mod hosting {
        fn add_to_waitlist() {}

        fn seat_at_table() {}
    }

    mod serving {
        fn take_order() {}

        fn serve_order() {}

        fn take_payment() {}
    }
}
```

To show Rust where to find an item in a module tree, we use a path in the same way we use a path when navigating a filesystem. A path can take two forms. An absolute path is the full path starting from a crate root, it begins with the 'crate' name.
A relative path starts from the current module and uses 'self', 'super', or an identifier in the current module. Both absolute and relative paths are followed by one or more identifiers separated by double colons (::). Choosing whether to use a relative or absolute path is a decision you’ll make based on your project, and it depends on whether you’re more likely to move item definition code separately from or together with the code that uses the item. Our preference in general is to specify absolute paths because it’s more likely we’ll want to move code definitions and item calls independently of each other.<br>
```
// Absolute path
crate::front_of_house::hosting::add_to_waitlist();

// Relative path
front_of_house::hosting::add_to_waitlist()
```
We can construct relative paths that begin in the parent module, rather than the current module or the crate root, by using 'super' at the start of the path. This is like starting a filesystem path with the '..' syntax.<br>
The 'pub' keyword on a module only lets code in its ancestor modules refer to it, not access its inner code. To make the items within the module public we need to use 'pub' on those items. If we use pub before a struct definition, we make the struct public, but the struct’s fields will still be private. We can make each field public or not on a case-by-case basis. In contrast, if we make an enum public, all of its variants are then public. We only need the 'pub' before the enum keyword.
```
mod back_of_house {
    pub struct Breakfast {
        pub toast: String,
        seasonal_fruit: String,
    }

    impl Breakfast {
        pub fn summer(toast: &str) -> Breakfast {
            Breakfast {
                toast: String::from(toast),
                seasonal_fruit: String::from("peaches"),
            }
        }
    }

    pub enum Appetizer {
        Soup,
        Salad,
    }
}
```

We can create a shortcut to a path with the 'use' keyword once, and then use the shorter name everywhere else in the scope.
```
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting; // 'hosting' now becomes a valid name.

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist(); // 'hosting' can be called directly instead of 'front_of_house::hosting'.
}
```
'as' can be used to create an alias, basically renaming.
```
use std::fmt::Result;
use std::io::Result as IoResult; // We chose the new name IoResult, which won’t conflict with the 'Result' from 'std::fmt' that we’ve also brought into scope.
```
'use' can be preceded by 'pub' when wanting to make its statement public when being imported as a module for external code to use, this is called re-exporting.<br>
To use an external package we can define it in our Cargo.toml. For example the 'rand' package can be indicated with its version like this `rand = "0.8.5"`. Then to include this package in scope `use rand;`. Many packages exist and can be found on 'crates.io'. On the other hand, 'std' refers to the standard library that comes with the Rust language and thus doesn't need to be indicated in 'Cargo.toml'. But we do need to include it in scope `use std::collections::HashMap;`.<br>
When using multiple items defined in the same crate/module, we can do that in one line `use std::{cmp::Ordering, io};`.
```
// Written in two lines.
use std::io;
use std::io::Write;

// Can be written in one line instead where we use the keyword 'self'.
use std::io::{self, Write};
```
If we want to bring all public items defined in a path into scope, we can specify that path followed by the '*' glob operator: `use std::collections::*;`.

When modules get large, you might want to move their definitions to a separate file to make the code easier to navigate.<br>
One file that contains 'front_of_house' module and a submodule named 'hosting' can look like this.
```
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}
```
We can split this in multiple files by creating 'src/front_of_house.rs', where the module name becomes file name. Its content would be `pub mod hosting;`. And creating 'src/front_of_house/hosting.rs', where parent module becomes directory name and submodule file name. Its content would be `pub fn add_to_waitlist() {}`. If we instead put 'hosting.rs' in the 'src' directory, the compiler would expect the 'hosting.rs' code to be in a hosting module declared in the crate root, and not declared as a child of the 'front_of_house' module.<br>
The 'mod' keyword declares modules, and Rust looks in a file with the same name as the module for the code that goes into that module. If the file name is the module name, inside the file you don't need to define the module anymore, only the items it contains. This allows moving each module’s code to a separate file while the module tree remains the same. 

Rust lets you split a package into multiple crates and a crate into modules so you can refer to items defined in one module from another module. You can do this by specifying absolute or relative paths. These paths can be brought into scope with a 'use' statement so you can use a shorter path for multiple uses of the item in that scope. Module code is private by default, but you can make definitions public by adding the 'pub' keyword.

### Common Collections
Rust’s standard library includes a number of very useful data structures called collections. Each kind of collection has different capabilities and costs, and choosing an appropriate one for your current situation is a skill you’ll develop over time.<br>
In this chapter, we’ll discuss three collections that are used very often in Rust programs. A 'vector' allows you to store a variable number of values next to each other. A 'string' is a collection of characters. A 'hash map' allows you to associate a value with a specific key. It’s a particular implementation of the more general data structure called a 'map'.

Vectors (`Vec<T>`) can store a dynamic amount of values next to each in memory. Vectors can only store values of the same type.<br>
We create a new vector like this `let mut v: Vec<i32> = Vec::new();`. Because we aren’t inserting any values into this vector, Rust doesn’t know what kind of elements we intend to store, this is why we specified type 'i32'. Rust conveniently provides the 'vec!' macro, which will create a new vector that holds the values you give it, like this `let v = vec![1, 2, 3];`.<br>
We can use the 'push' method to add elements to a mutable vector like this `v.push(5);`. The 'pop' method removes and returns the last element.<br>
Here is an example showing how to access elements.
```
let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2]; // We can access a value in a vector using the indexing syntax which gives a reference.
println!("The third element is {third}");

let third: Option<&i32> = v.get(2); // We can access a value in a vector using the 'get' method which gives an 'Option<&T>'.
match third {
    Some(third) => println!("The third element is {third}"),
    None => println!("There is no third element."), // When the 'get' method is passed an index that is outside the vector, it returns 'None' without crashing.
}
```
We can iterate over immutable or mutable vectors.
```
let v = vec![100, 32, 57];
for i in &v {
    println!("{i}");
}

let mut v = vec![100, 32, 57];
for i in &mut v {
    *i += 50; // We transform each value in the mutable vector.
}
```
To store multiple types in one vector we can use an Enum.
```
enum SpreadsheetCell {
    Int(i32),
    Float(f64),
    Text(String),
}

let row = vec![
    SpreadsheetCell::Int(3),
    SpreadsheetCell::Text(String::from("blue")),
    SpreadsheetCell::Float(10.12),
];
```

Rust has only one string type in the core language, which is the string slice 'str' that is usually seen in its borrowed form '&str'. The String type, which is provided by Rust’s standard library rather than coded into the core language, is a growable, mutable, owned string type. Although this section is largely about String, both types are used heavily in Rust’s standard library.<br>
We create a string like this `let mut s = String::new();` and we can instanciate it with data like this `let s = "initial contents".to_string();` or `let s = String::from("initial contents");`.<br>
A String can grow in size and its contents can change. In addition, you can conveniently use the '+' operator or the 'format!' macro to concatenate 'String' values. We can grow a 'String' by using the 'push_str' method to append a string slice.
```
let s1 = String::from("Hello, ");
let s2 = String::from("world!");
let s3 = s1 + &s2;

//For combining strings in more complicated ways, we can instead use the 'format!' macro.
let s1 = String::from("tic");
let s2 = String::from("tac");
let s3 = String::from("toe");
let s = format!("{s1}-{s2}-{s3}");
// The code generated by the 'format!' macro uses references so that this call doesn’t take ownership of any of its parameters.

let mut s = String::from("foo");
s.push_str("bar");
```
Rust strings don’t support indexing, because it’s not clear what the return type of the string-indexing operation should be: a byte value, a character, a grapheme cluster, or a string slice. Rather than indexing using '[]' with a single number, you can use '[]' with a range to create a string slice containing particular bytes. Regular characters are one byte long but Russian characters are for example two bytes long.
```
let hello = "Здравствуйте";

let s = &hello[0..4]; // This refers to 'Зд' because Russian chars are two bytes long.
```
The best way to operate on pieces of strings is to be explicit about whether you want characters or bytes.
```
for c in "Зд".chars() {
    println!("{c}");
}
```
The standard library offers a lot of functionality built off the 'String' and '&str' types.

The type `HashMap<K, V>` stores a mapping of keys of type 'K' to values of type 'V' using a hashing function, which determines how it places these keys and values into memory. Many programming languages support this kind of data structure, but they often use a different name, such as hash, map, object, hash table, dictionary, or associative array, just to name a few. Hash maps are useful when you want to look up data not by using an index, as you can with vectors, but by using a key that can be of any type.<br>
One way to create an empty hash map is to use 'new' and to add elements with 'insert'. All of the keys must have the same type, and all of the values must have the same type.
```
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);
```
We can get a value out of the hash map by providing its key to the get method. The 'get' method returns an 'Option<&V>', if there’s no value for that key in the hash map, 'get' will return 'None'. 
```
let team_name = String::from("Blue");
let score = scores.get(&team_name).copied().unwrap_or(0);
```
'copied()' can be used to get an 'Option<V>' instead of 'Option<&V>'. And 'unwrap_or' to set score to zero if scores doesn’t have an entry for the key.<br>
We can iterate over each key–value pair in a hash map using a 'for' loop.
```
for (key, value) in &scores {
    println!("{key}: {value}");
}
```
If we insert a key and a value into a hash map and then insert that same key with a different value, the value associated with that key will be replaced/overwritten.<br>
By default, 'HashMap' uses a hashing function called 'SipHash' that can provide resistance to denial-of-service (DoS) attacks involving hash tables. This is not the fastest hashing algorithm available, but the trade-off for better security is worth it. If you find that the default hash function is too slow for your purposes, you can switch to another function by specifying a different hasher.

### Error Handling
Rust makes distinction between recoverable errors, such as file not found, and unrecoverable erros, such as trying to access a location beyond the end of an array.
Most languages don't make this distinction and handle all errors the same with 'exceptions'. But Rust instead uses `Result<T,E>` for recoverable errors and the `panic!` macro to stop program execution when unrecoverable errors are encountered.

The `panic!` macro can be explicitly called or will be automatically called after an illegal action such as trying to access an array past the end. By default these panics will print a failure message, clean and quit the program. You can also customize these panics in 'Cargo.toml' to abort instantly instead of clean in certain instances.

In C, attempting to read beyond the end of a data structure is undefined behavior. You might get whatever is at the location in memory that would correspond to that element in the data structure, even though the memory doesn’t belong to that structure. This is called a buffer overread and can lead to security vulnerabilities if an attacker is able to manipulate the index in such a way as to read data they shouldn’t be allowed to that is stored after the data structure.<br>
To protect your program from this sort of vulnerability, if you try to read an element at an index that doesn’t exist, Rust will stop execution and refuse to continue.

Most errors aren’t serious enough to require the program to stop entirely. Sometimes when a function fails it’s for a reason that you can easily interpret and respond to.<br>
The 'Result' enum is defined as having two variants, 'Ok' and 'Err', as follows:
```
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```
Let’s call a function that returns a 'Result' value because the function could fail.
```
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    let greeting_file = match greeting_file_result {
        Ok(file) => file,
        Err(error) => match error.kind() {
            ErrorKind::NotFound => match File::create("hello.txt") {
                Ok(fc) => fc,
                Err(e) => panic!("Problem creating the file: {e:?}"),
            },
            other_error => {
                panic!("Problem opening the file: {other_error:?}");
            }
        },
    };
}
```
Using 'match' works well enough, but it can be a bit verbose and doesn’t always communicate intent well. The 'Result' type has many helper methods defined on it to do various, more specific tasks. The 'unwrap' method is a shortcut method implemented just like the match expression. If the 'Result' value is the 'Ok' variant, 'unwrap' will return the value inside the 'Ok'. If the 'Result' is the 'Err' variant, 'unwrap' will call the 'panic!' macro for us.
```
use std::fs::File;

fn main() {
    let greeting_file = File::open("hello.txt").unwrap();
}
```
Instead of 'unwrap' you can use 'expect' which lets you choose the 'panic!' error message.
```
let greeting_file = File::open("hello.txt")
        .expect("hello.txt should be included in this project");
```

Instead of handling an error within a function itself, you can let the function return the error, allowing the code that called the function to handle the error instead, we call this propagating the error.<br>
The '?' operator can be used as a shortcut for propagating errors.
```
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
    let mut username = String::new();

    //The '?' placed after a 'Result' value is defined to work in almost the same way as the match expressions we defined to handle the 'Result' values.
    //If the value of the Result is an 'Ok', the value inside the 'Ok' will get returned from this expression, and the program will continue.
    //If the value is an 'Err', the 'Err' will be returned from the whole function as if we had used the 'return' keyword so the error value gets propagated to the calling code.
    File::open("hello.txt")?.read_to_string(&mut username)?; // Here we chain method calls after the '?' for shorter code.
    Ok(username)
}
```
Instead we can use `fs::read_to_string("hello.txt")` as one function to open a file and put its contents into a string while handling errors automatically.<br>
Note that you can use the '?' operator on a 'Result' in a function that returns 'Result', and you can also use the '?' operator on an 'Option' in a function that returns 'Option'.<br>
When a main function returns a 'Result<(), E>', the executable will exit with a value of '0' if main returns 'Ok(())' and will exit with a nonzero value if main returns an 'Err' value. Executables written in C return integers when they exit, programs that exit successfully return the integer '0', and programs that error return some integer other than '0'. Rust also returns integers from executables to be compatible with this convention.

Only use 'panic!' when the error is unrecoverable, else use 'Result' to have the option to recover.<br>
It can also be beneficial to use 'panic!' when code could end in a bad state where continuing could be insecure or harmful. 

### Generic Types, Traits, and Lifetimes
Generics are placeholders who can represent any type. They usually are denoted as `T`. We declare a generic function like this `fn largest<T>(list: &[T]) -> &T {`. We can also define structs to use a generic type parameter/placeholder in one or more fields.
```
struct Point<T> {
    x: T,
    y: T,
}

fn main() {
    let integer = Point { x: 5, y: 10 };
    let float = Point { x: 1.0, y: 4.0 };
}
```
If we want to use different placeholders we can too.
```
struct Point<T, U> { // Next to T we use the placeholder U.
    x: T,
    y: U,
}

fn main() {
    let both_integer = Point { x: 5, y: 10 };
    let both_float = Point { x: 1.0, y: 4.0 };
    let integer_and_float = Point { x: 5, y: 4.0 }; // One is integer and other float.
}
```
We can define enums to hold generic data types in their variants.
```
enum Option<T> {
    Some(T),
    None,
}
```
We can implement methods on structs and enums and use generic types in their definitions too.
```
impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}
```

A trait defines the functionality a particular type has and can share with other types. A type’s behavior consists of the methods we can call on that type. Different types share the same behavior if we can call the same methods on all of those types.<br>
A trait is a grouping of method signatures (the combination of a method's name and its parameter list) that types can implement. Each type implementing the trait must provide its own custom behavior for the body of the method signature. The compiler will enforce that any type implementing a trait has the methods defined in the trait.
```
pub trait Summary { // The keyword pub makes any module, function, or data structure accessible from inside of external modules.
    fn summarize(&self) -> String; // Method signature associated with the trait.
}

pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle { // Here we implement the trait for NewsArticle type.
    fn summarize(&self) -> String { // We define its own function body.
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for Tweet { // Here we implement the trait for Tweet type.
    fn summarize(&self) -> String { // We define its own function body.
        format!("{}: {}", self.username, self.content) 
    }
}
```
Sometimes it’s useful to have default behavior for some or all of the methods in a trait instead of requiring implementations for all methods on every type. Then, as we implement the trait on a particular type, we can keep or override each method’s default behavior. Inside the trait we would declare the method's function body too, and inside the type implementation we don't need to add anything when wanting to keep the default behavior, but can rewrite function if wanting to override it.
```
pub trait Summary {
    fn summarize_author(&self) -> String;

    fn summarize(&self) -> String {
        format!("(Read more from {}...)", self.summarize_author())
    }
}

impl Summary for Tweet {
    fn summarize_author(&self) -> String {
        format!("@{}", self.username)
    }

    // We don't override 'summarize(&self)' thus keep its default behavior.
}
```
Traits can also be used to indicate acceptable parameter types.
```
pub fn notify(item: &impl Summary) { // Instead of a concrete type for the 'item' parameter, we specify the 'impl' keyword and the trait name. This parameter accepts any type that implements the specified trait.
    println!("Breaking news! {}", item.summarize()); // In the body of notify, we can call any methods on 'item' that come from the 'Summary' trait, such as 'summarize'.
}
```
The 'impl Trait' syntax is actually syntax sugar for a longer form known as a trait bound, that looks like this.
```
pub fn notify<T: Summary>(item: &T) {
    println!("Breaking news! {}", item.summarize());
}
```
We can also specify more than one trait bound.
```
pub fn notify(item: &(impl Summary + Display)) { // Both Summary and Display traits are indicated.
```
We can also use the 'impl Trait' syntax in the return position to return a value of some type that implements a trait, as shown here.
```
fn returns_summarizable() -> impl Summary {
    Tweet {
        username: String::from("horse_ebooks"),
        content: String::from(
            "of course, as you probably already know, people",
        ),
        reply: false,
        retweet: false,
    }
}
```
We can also implement a trait for any type that implements another trait. This is called blanket implementations. 
```
impl<T: Display> ToString for T { // The 'ToString' trait is implemented on any type that implements the 'Display' trait.
}
```

Lifetimes ensure that references are valid as long as we need them to be. Every reference has a lifetime. Most of the time this lifetime is implicit and inferred, but sometimes when ambiguous, annotation is necessary.<br>
Lifetime annotations don’t change how long any of the references live. Rather, they describe the relationships of the lifetimes of multiple references to each other. Lifetime annotations have a slightly unusual syntax: the names of lifetime parameters must start with an apostrophe (') and are usually all lowercase and very short. Most people use the name 'a for the first lifetime annotation.
```
&i32        // a reference
&'a i32     // a reference with an explicit lifetime
&'a mut i32 // a mutable reference with an explicit lifetime
```
To use lifetime annotations in function signatures, we need to declare the generic lifetime parameters inside angle brackets between the function name and the parameter list, just as we did with generic type parameters. We want the signature to express the following constraint to the compiler: the returned reference will be valid as long as both the parameters are valid. This is the relationship between lifetimes of the parameters and the return value. We’ll name the lifetime 'a and then add it to each reference.
```
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```
In practice, the function signature means that the lifetime of the reference returned by the 'longest' function is the same as the lifetimes of the values referred to by the function arguments. Remember, when we specify the lifetime parameters in this function signature, we’re not changing the lifetimes of any values passed in or returned. Rather, we’re specifying that the compiler should reject any values that don’t adhere to these constraints. The lifetime annotations become part of the contract of the function, much like the types in the signature.<br>
The following code calling the previously defined function with lifetimes will create an error. 
```
fn main() {
    let string1 = String::from("long string is long");
    let result;
    {
        let string2 = String::from("xyz");
        result = longest(string1.as_str(), string2.as_str());
    }
    println!("The longest string is {result}");
}
```
The error shows that for 'result' to be valid for the 'println!' statement, string2 would need to be valid until the end of the outer scope. Rust knows this because we annotated the lifetimes of the 'longest' function parameters and return values using the same lifetime parameter 'a.<br>
Lifetimes can also be used in methods.
```
impl<'a> ImportantExcerpt<'a> {
    fn level(&self) -> i32 {
        3
    }
}
```
'static is a special lifetime which denotes the affected reference lives for the entire duration of the program. Most of the time, an error message suggesting the use of 'static occurs from attempting to create a dangling reference or a mismatch of the available lifetimes. In such cases, the solution is to fix those problems, not to specify the 'static lifetime.<br>
Here is an example of how to specify generic types, traits, and lifetimes, all in one function.
```
use std::fmt::Display;

fn longest_with_an_announcement<'a, T>(
    x: &'a str,
    y: &'a str,
    ann: T,
) -> &'a str
where
    T: Display, // The generic type T can be filled by any type that implements the Display trait.
{
    println!("Announcement! {ann}");
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

### Writing automated tests
Rust includes support for writing automated software tests because its compiler is not able to verify if functions do what they were intended to do. Thus automated tests are used to verify functions return what they should. Those tests can be run each time we make changes to our code.

At its simplest, a test in Rust is a function that’s annotated with the test attribute. Attributes are metadata about pieces of Rust code. To change a function into a test function, add `#[test]` on the line before `fn`.<br>
When you run your tests with the `cargo test` command, Rust builds a test runner binary that runs the annotated functions and reports on whether each test function passes or fails. Whenever we make a new library project with Cargo, a test module with a test function in it is automatically generated for us.<br>
Here is an example test function that uses the `assert_eq!` macro to assert the test result is correct.
```
#[test]
fn it_works() {
    let result = add(2, 2);
    assert_eq!(result, 4); // We give the 'assert!' macro arguments that evaluate to a Boolean. If the value is 'true', nothing happens and the test passes. If the value is 'false', the 'assert!' macro calls 'panic!' to cause the test to fail.
}
```
The 'assert!' macro can also only take one argument, then that one argument should return true or false. Inversely, the `assert_ne!` macro passes if the argument returns false or two values are different.<br>
We can also use custom error messages.
```
#[test]
    fn greeting_contains_name() {
        let result = greeting("Carol");
        assert!(
            result.contains("Carol"),
            // If an error occurs "Greeting did ..." will be used as error message.
            "Greeting did not contain name, value was `{}`", // '{}' is a placeholder for 'result'.
            result
        );
    }
```
The function attribute `#[should_panic]` indicates the test passes if the code inside the function panics. We can be even more precise and indicate with what error message the function should panic by indicating a substring of that error message, for example `#[should_panic(expected = "less than or equal to 100")]`.

Just as `cargo run` compiles your code and then runs the resulting binary, `cargo test` compiles your code in test mode and runs the resulting test binary.<br>
When you run multiple tests, by default they run in parallel using threads, meaning they finish running faster. When running in parallel the different tests cannot share the same state, if they do you should indicate the use of only one thread `cargo test -- --test-threads=1`.<br>
Running all the tests can sometimes take a long time, sometimes when only working on specific code part you may only want to pass certain tests. You can choose which tests to run by passing `cargo test` the name of the test's function you want to run as an argument. We can also specify part of a test name, and any test whose name matches that value will be run. Within code you can also use the attribute `#[ignore]` on test functions you don't want to execute. If you want to run all tests whether they’re ignored or not, you can run `cargo test -- --include-ignored`.

The Rust community thinks about tests in terms of two main categories: unit tests and integration tests.<br>
The purpose of unit tests is to test each unit of code in isolation from the rest of the code to quickly pinpoint where code is and isn’t working as expected. The convention is to create a module named 'tests' in each file of the 'src' directory to contain the test functions and to annotate the module with `#[cfg(test)] `. This annotation tells Rust to compile and run the test code only when you run `cargo test`. This saves compile time when you only want to build the library and saves space in the resulting compiled artifact because the tests are not included.<br>
In Rust, integration tests are entirely external to your library. They use your library in the same way any other code would, which means they can only call functions that are part of your library’s public API. Their purpose is to test whether many parts of your library work together correctly. Units of code that work correctly on their own could have problems when integrated, so test coverage of the integrated code is important as well. We create the integration tests in a 'tests' directory next to the 'src' directory, cargo knows to look for integration test files in this directory. Each file in the tests directory is a separate crate, the test functions it contains also need the `#[test]` annotation. To run all the tests in a particular integration test file, use the `--test` argument of `cargo test` followed by the name of the file.

### Functional Language Features: Iterators and Closures
Rust’s design has taken inspiration from many existing languages and techniques, and one significant influence is functional programming. Some features of Rust are similar to features found in many functional languages. Those features we will cover are closures and iterators who have the advantage of speed. Pattern matching and enums we already covered and are also influenced by the functional style.

Rust’s closures are anonymous functions you can save in a variable or pass as arguments to other functions.
```
let add_one_v2 = |x: u32| -> u32 { x + 1 }; // Verbose closure definition.
let add_one_v3 = |x|             { x + 1 }; // Type annotations are optional in closures as the compiler can infer the types.
let add_one_v4 = |x|               x + 1  ; // Because function body only has one expression the brackets are optional.
```

An iterator allows iterating over a sequence of elements until the end of the sequence.
```
let v1 = vec![1, 2, 3];

let v1_iter = v1.iter(); // Create an iterator from the vector sequence.

for val in v1_iter { // Iterate over next element after next loop automatically.
    println!("Got: {val}");
}
```
Iterators contain the 'next' method, which returns one item of the iterator at a time wrapped in 'Some' of 'Option' enum, or when iteration is over it returns 'None'. Each call to 'next' eats up an item from the iterator, so that on its next call the following item is returned.<br>
The values returned from an iterator are immutable references. If we want to iterate over mutable references we can use the method `.iter_mut()` instead of `.iter()`.<br>
Iterator adaptors are methods defined on the Iterator trait that don’t consume the iterator. Instead, they produce different iterators by changing some aspect of the original iterator. For example the 'map' method takes a function that changes each element of an iterator.
```
let v1: Vec<i32> = vec![1, 2, 3];

let v2: Vec<_> = v1.iter().map(|x| x + 1).collect(); // 'collect' is necessary to collect the resulting values into a collection data type.
```

Iterators, although a high-level abstraction, get compiled down to roughly the same code as if you’d written the lower-level code yourself. Iterators are one of Rust’s zero-cost abstractions, by which we mean using the abstraction imposes no additional runtime overhead.<br>
In general, C++ implementations obey the zero-overhead principle: What you don’t use, you don’t pay for. And further: What you do use, you couldn’t hand code any better. Rust tries to be fast like C and C++.<br>
The implementations of closures and iterators are such that runtime performance is not affected. This is part of Rust’s goal to strive to provide zero-cost abstractions.

### More About Cargo and Crates.io
So far we’ve used only the most basic features of Cargo to build, run, and test our code, but it can do a lot more.

In Rust, 'release profiles' are predefined and customizable profiles with different configurations that allow a programmer to have more control over various options for compiling code.<br>
Cargo has two main profiles: the 'dev' profile Cargo uses when you run cargo build and the 'release' profile Cargo uses when you run cargo build --release. The 'dev' profile is defined with good defaults for development, and the 'release' profile has good defaults for release builds.<br>
Cargo has default settings for each of the profiles that apply when you haven’t explicitly added any `[profile.*]` sections in the project’s 'Cargo.toml' file. You can override a default setting by adding a different value for it in 'Cargo.toml'. For example, if we want to use optimization level 1 in the development profile, we can add these two lines to our project’s Cargo.toml file.
```
[profile.dev]
opt-level = 1 // The opt-level setting controls the number of optimizations Rust will apply to your code, with a range of 0 to 3. Applying more optimizations extends compiling time.
```
For the full list of configuration options and defaults for each profile, see [Cargo’s documentation](https://doc.rust-lang.org/cargo/reference/profiles.html).

We’ve used packages from [crates.io](https://crates.io/) as dependencies of our project, but you can also share your code with other people by publishing your own packages.<br>
Accurately documenting your packages will help other users know how and when to use them, so it’s worth investing the time to write documentation. Comments are usually done with `//` but documentation comments use `///` and supports markdown notation. Documentation comments are usually written before the function it explains. Running `cargo doc --open` generates an HTML representation from the documentation comments and opens it in a web browser. In those documentation comments it is recommended to have a section for examples, panics (scenarios where the function could panic), errors (errors that return 'Result'), safety (when the function can be unsafe). Running `cargo test` will run the code examples in the documentation as tests too. To document an entire crate/module instead of a single function we can at top of file write comments using `//!`.<br>
When creating a package and having modules within modules, it may be better to re-export the deeper modules within the top module, to make those deeper modules more visible in the documentation and shorter to include. In the following example `pub use` is used for that.
```
//! # Art
//!
//! A library for modeling artistic concepts.

pub use self::kinds::PrimaryColor; // Allows direct use of PrimaryColor.
pub use self::kinds::SecondaryColor;
pub use self::utils::mix;

pub mod kinds {
    // --snip--
}

pub mod utils {
    // --snip--
}
```
Before you can publish any crates, you need to create an account on 'crates.io' and get an API token. Once you’re logged in, visit your account settings at 'https://crates.io/me/' and retrieve your API key. Then run the `cargo login` command and paste your API key when prompted.<br>
If you want to publish a crate, you need to add some metadata in the `[package]` section of the crate's 'Cargo.toml' file.
```
[package]
name = "guessing_game" // The crate will need a name that is unique on 'crates.io'.
version = "0.1.0"
edition = "2021"
description = "A fun game where you guess what number the computer has chosen."
license = "MIT" // For the license field, you need to give a license identifier value.
```
Now you can run `cargo publish`. Be careful, because a publish is permanent. The version can never be overwritten, and the code cannot be deleted. However, it is possible to prevent any future projects from adding the crate as a new dependency, we call this yanking a crate version, this is useful when a crate version is broken.<br>
When you’ve made changes to your crate and are ready to release a new version, you change the version value specified in your 'Cargo.toml' file and republish.

As your project develops, you might find that the library crate continues to get bigger and you want to split your package further into multiple library crates. Cargo offers a feature called workspaces that can help manage multiple related packages that are developed in tandem.<br>
A workspace is a set of packages that share the same 'Cargo.lock' and output directory. If each crate had its own target directory, each crate would have to recompile each of the other crates in the workspace to place the artifacts in its own target directory. By sharing one target directory, the crates can avoid unnecessary rebuilding.<br>
To create a workspace, first create a directory with a 'Cargo.toml' file that contains a `[workspace]` section instead of a `[package]` section. Then use `cargo new` to create the underlying packages and `cargo build` to build the workspace.
```
[workspace]

members = [
    "adder", // Specify the path to underlying packages.
    "add_one",
]
```
Cargo doesn’t assume that crates in a workspace will depend on each other, so we need to be explicit about the dependency relationships.
```
[dependencies]
add_one = { path = "../add_one" } // Now the other crates can use 'add_one'.
rand = "0.8.5" // This is a dependency to an external package.
```
Notice that a workspace has only one 'Cargo.lock' file at the top level, rather than having a 'Cargo.lock' in each crate’s directory. This ensures that all crates are using the same version of all dependencies, making them compatible. 

The `cargo install` command allows you to install and use binary crates locally. Note that you can only install packages that have binary targets. A binary target is the runnable program that is created if the crate has a 'src/main.rs' file or another file specified as a binary, as opposed to a library target that isn’t runnable on its own but is suitable for including within other programs. All those installed binaries are stored in the root's 'bin' folder. For example rust's implementation of the 'grep' command is called 'ripgrep' and can be installed via cargo like this `cargo install ripgrep`. After you can use the installed command by calling `cargo ripgrep`.

### Smart pointers
A pointer is a general concept for a variable that contains an address in memory. This address refers to, or points at, some other data.<br>
The most common kind of pointer in Rust is a reference. They are indicated by the '&' symbol and borrow the value they point to. They don’t have any special capabilities other than referring to data, and have no overhead.<br>
Smart pointers, on the other hand, are data structures that act like a pointer but also have additional metadata and capabilities. Smart pointers originated in C++ and exist in other languages as well. Rust has a variety of smart pointers defined in the standard library that provide functionality beyond that provided by references.<br>
While references only borrow data, smart pointers usually own the data they point to.<br>
The previously seen 'String' and 'Vec<T>' can count as smart pointers because they own some memory and allow you to manipulate it.

The 'Box<T>' smart pointer stores data on the heap rather than the stack, what remains on the stack is the pointer to the heap data.<br>
A value of recursive type can have another value of the same type as part of itself. Recursive types pose an issue because at compile time Rust needs to know how much space a type takes up. However, the nesting of values of recursive types could theoretically continue infinitely, so Rust can’t know how much space the value needs. Because boxes have a known size, we can enable recursive types by inserting a box in the recursive type definition. As an example of a recursive type, let’s explore the 'cons list'. This data type comes from the lisp programming language and is like a linked list. It is made up of nested pairs like this `(1, (2, (3, Nil)))`. The 'cons list' isn’t a commonly used data structure in Rust. Most of the time when you have a list of items in Rust, 'Vec<T>' is a better choice to use.<br>
The 'Box<T>' type is a smart pointer because it implements the 'Deref' trait, which allows 'Box<T>' values to be treated like references. When a 'Box<T>' value goes out of scope, the heap data that the box is pointing to is cleaned up as well because of the 'Drop' trait implementation.

Implementing the 'Deref' trait allows you to customize the behavior of the dereference operator '*'. This operator is used to access the value the reference points to instead of the reference itself.

Implementing the 'Drop' trait lets you customize what happens when a value is about to go out of scope. With smart pointers 'Drop' is often used to deallocate the memory they point to. Besides smart pointers, 'Drop' is also used to free memory from other resources such as file handles, sockets, locks.<br>
Even if drop is usually called automatically when going out of scope, it is also possible to call it manually. You may want to call it manually for example when wanting to release/free a lock for other code in same scope to acquire the lock. However, to avoid a double free you cannot call the 'Drop' method itself manually, instead you should call the `std::mem::drop` function that takes the value we want to free early.

'Rc<T>' is an abbreviation for reference counting and it enables multiple owners on a single value. It keeps track of the number of references to a value to determine whether or not the value is still in use. If there are zero references to a value, the value can be cleaned up without any references becoming invalid.<br>
Note that 'Rc<T>' is only for use in single-threaded scenarios. In multi-threaded programs, reference counting is done differently.<br>
To create the first owner use `Rc::new(variable)` and for the next owners use `Rc::clone(&variableToClone)`. When using 'Rc:clone' we don't create a deep copy but instead simply increment the reference count which is fast.<br>
Calling the `Rc::strong_count` function displays the reference count.<br>
Via immutable references, 'Rc<T>' allows you to share data between multiple parts of your program for reading only.

'Interior mutability' is a design pattern in Rust that allows you to mutate data even when there are immutable references to that data. Normally, this action is disallowed by the borrowing rules. To mutate data, the pattern uses 'unsafe code' inside a data structure to bend Rust’s usual rules that govern mutation and borrowing. 'Unsafe code' indicates to the compiler that we’re checking the rules manually instead of relying on the compiler to check them for us. Let’s explore this concept by looking at the 'RefCell<T>' type that follows the 'interior mutability' pattern.<br>
'RefCell<T>' can either hold one mutable reference or multiple immutable references. With references and 'Box<T>' the borrowing rules are enforced at compile time, but with 'RefCell<T>' those are enforced at runtime. This means that instead of compilation errors, when breaking the rules with 'RefCell<T>', your program will panic and exit while running.<br>
Similar to 'Rc<T>', 'RefCell<T>' is only for use in single-threaded scenarios.<br>
There are situations in which it would be useful for a value to mutate itself in its methods but appear immutable to other code. Code outside the value’s methods would not be able to mutate the value. Using 'RefCell<T>' is one way to get the ability to have interior mutability.<br>
When creating immutable and mutable references, we use the '&' and '&mut' syntax, respectively. With 'RefCell<T>', we use the 'borrow' and 'borrow_mut' methods. The borrow method returns the smart pointer type 'Ref<T>', and 'borrow_mut' returns the smart pointer type 'RefMut<T>'. Both types implement 'Deref', so we can treat them like regular references. If we try to violate these rules, rather than getting a compiler error as we would with references, the implementation of 'RefCell<T>' will panic at runtime.
```
impl Messenger for MockMessenger {
        fn send(&self, message: &str) {
            // The creation of two mutable borrows within same scope will create a runtime error.
            let mut one_borrow = self.sent_messages.borrow_mut(); 
            let mut two_borrow = self.sent_messages.borrow_mut();

            one_borrow.push(String::from(message));
            two_borrow.push(String::from(message));
        }
}
```
The 'RefCell<T>' keeps track of how many 'Ref<T>' and 'RefMut<T>' smart pointers are currently active. Every time we call 'borrow', the 'RefCell<T>' increases its count of how many immutable borrows are active. When a 'Ref<T>' value goes out of scope, the count of immutable borrows goes down by one. Just like the compile-time borrowing rules, 'RefCell<T>' lets us have many immutable borrows or one mutable borrow at any point in time.<br>
A common way to use 'RefCell<T>' is in combination with 'Rc<T>'. Recall that 'Rc<T>' lets you have multiple owners of some data, but it only gives immutable access to that data. If you have an 'Rc<T>' that holds a 'RefCell<T>', you can get a value that can have multiple owners and that you can mutate.
```
use crate::List::{Cons, Nil};
use std::cell::RefCell;
use std::rc::Rc;

fn main() {
    let value = Rc::new(RefCell::new(5));
    //We need to clone 'value' so both 'a' and 'value' have ownership of the inner 5 value. 
    let a = Rc::new(Cons(Rc::clone(&value), Rc::new(Nil)));
    //We wrap the list 'a' in an 'Rc<T>' so when we create lists 'b' and 'c', they can both refer to 'a'.
    let b = Cons(Rc::new(RefCell::new(3)), Rc::clone(&a));
    let c = Cons(Rc::new(RefCell::new(4)), Rc::clone(&a));
    //The 'borrow_mut' method returns a 'RefMut<T>' smart pointer, and we use the dereference operator on it and change the inner value.
    *value.borrow_mut() += 10;
    //When we print 'a', 'b', and 'c', we can see that they all have the modified value of 15 rather than 5.
    println!("a after = {a:?}");
    println!("b after = {b:?}");
    println!("c after = {c:?}");
}
```
'RefCell<T>' adds usage flexibility but while compromising program speed.

To recapitulate.<br>
'Rc<T>' enables multiple owners of the same data, 'Box<T>' and 'RefCell<T>' have single owners.<br>
'Box<T>' allows immutable or mutable borrows checked at compile time, 'Rc<T>' allows only immutable borrows checked at compile time, 'RefCell<T>' allows immutable or mutable borrows checked at runtime.<br>
Because 'RefCell<T>' allows mutable borrows checked at runtime, you can mutate the value inside the 'RefCell<T>' even when the 'RefCell<T>' is immutable.<br>
The 'Box<T>' type has a known size and points to data allocated on the heap. The 'Rc<T>' type keeps track of the number of references to data on the heap so that data can have multiple owners. The 'RefCell<T>' type with its interior mutability gives us a type that we can use when we need an immutable type but need to change an inner value of that type, it also enforces the borrowing rules at runtime instead of at compile time.

A memory leak refers to memory that is accidentally never cleaned up. Rust’s memory safety guarantees make it difficult, but not impossible, to accidentally create a memory leak.<br>
We can see that Rust allows memory leaks by using 'Rc<T>' and 'RefCell<T>'. It’s possible to create references where items refer to each other in a cycle. This creates memory leaks because the reference count of each item in the cycle will never reach 0, and the values will never be dropped. We call this a reference cycle.<br>
Strong references are how you can share ownership of an 'Rc<T>' instance. Weak references don’t express an ownership relationship, and their count doesn’t affect when an 'Rc<T>' instance is cleaned up. They won’t cause a reference cycle because any cycle involving some weak references will be broken once the strong reference count of values involved is 0. When you call 'Rc::downgrade', you get a smart pointer of type 'Weak<T>'. Instead of increasing the 'strong_count' in the 'Rc<T>' instance by 1, calling 'Rc::downgrade' increases the 'weak_count' by 1. The 'Rc<T>' type uses 'weak_count' to keep track of how many 'Weak<T>' references exist, similar to 'strong_count'. The difference is the 'weak_count' doesn’t need to be 0 for the 'Rc<T>' instance to be cleaned up. Because the value that 'Weak<T>' references might have been dropped, to do anything with the value that a 'Weak<T>' is pointing to, you must make sure the value still exists. Do this by calling the 'upgrade' method on a 'Weak<T>' instance, which will return an 'Option<Rc<T>>'. You’ll get a result of 'Some' if the 'Rc<T>' value has not been dropped yet and a result of 'None' if the 'Rc<T>' value has been dropped.

### Fearless Concurrency
Concurrent programming, where different parts of a program execute independently, and parallel programming, where different parts of a program execute at the same time, are becoming increasingly important as more computers take advantage of their multiple processors (For this chapter, please mentally substitute 'concurrent and/or parallel' whenever we use 'concurrent'). Historically, programming in these contexts has been difficult and error prone, Rust hopes to change that. By leveraging ownership and type checking, many concurrency errors are compile-time errors in Rust rather than runtime errors. Therefore, rather than making you spend lots of time trying to reproduce the exact circumstances under which a runtime concurrency bug occurs, incorrect code will refuse to compile and present an error explaining the problem. As a result, you can fix your code while you’re working on it rather than potentially after it has been shipped to production. We’ve nicknamed this aspect of Rust fearless concurrency.

In most current operating systems, an executed program’s code is run in a process, and the operating system will manage multiple processes at once. Within a program, you can also have independent parts that run simultaneously. The features that run these independent parts are called threads. For example, a web server could have multiple threads so that it could respond to more than one request at the same time.

Splitting the computation in your program into multiple threads to run multiple tasks at the same time can improve performance, but it also adds complexity.<br> 
Because threads can run simultaneously, there’s no inherent guarantee about the order in which parts of your code on different threads will run. This can lead to problems, such as:
* Race conditions, where threads are accessing data or resources in an inconsistent order.<br>
* Deadlocks, where two threads are waiting for each other, preventing both threads from continuing.<br>
* Bugs that happen only in certain situations and are hard to reproduce and fix reliably.

To create a new thread, we call the `thread::spawn` function and pass it a closure (anonymous function) containing the code we want to run in the new thread.<br>
Note that when the main thread of a Rust program completes, all spawned threads are shut down, whether or not they have finished running. We can fix the problem of the spawned thread ending prematurely by saving the return value of 'thread::spawn' in a variable. The return type of 'thread::spawn' is 'JoinHandle'. A 'JoinHandle' is an owned value that, when we call the join method on it, will wait for its thread to finish.
```
use std::thread;
use std::time::Duration;

fn main() {
    let handle = thread::spawn(|| {
        for i in 1..10 {
            println!("hi number {i} from the spawned thread!");
            thread::sleep(Duration::from_millis(1)); // The calls to 'thread::sleep' force a thread to stop its execution for a short duration, allowing a different thread to run.
        }
    });

    for i in 1..5 {
        println!("hi number {i} from the main thread!");
        thread::sleep(Duration::from_millis(1));
    }

    handle.join().unwrap(); // Calling join on the handle blocks the thread currently running until the thread represented by the handle terminates.
}
```
We’ll often use the 'move' keyword with closures passed to 'thread::spawn' because the closure will then take ownership of the values it uses from the environment, thus transferring ownership of those values from one thread to another.
```
use std::thread;

fn main() {
    let v = vec![1, 2, 3];

    let handle = thread::spawn(move || { //The 'move' keyword is used to allow subsequent use of 'v' within our spawned thread, this also guarantees we won't use 'v' anymore in the main thread.
        println!("Here's a vector: {v:?}");
    });

    handle.join().unwrap();
```

Message passing refers to threads communicating, one thread sending a message to another. A channel is a general programming concept by which data is sent from one thread to another. Rust’s standard library provides an implementation of channels. A channel has a transmitter who sends the message data and a receiver who receives the message data. A channel is said to be closed if either the transmitter or receiver is dropped.<br>
We create a new channel using the `mpsc::channel` function; mpsc stands for multiple producer, single consumer. In short, the way Rust’s standard library implements channels means a channel can have multiple sending ends that produce values but only one receiving end that consumes those values.
```
use std::sync::mpsc;
use std::thread;

fn main() {
    let (tx, rx) = mpsc::channel(); // The 'mpsc::channel' function returns a tuple, the first element of which is the sending end (the transmitter) and the second element is the receiving end (the receiver). The abbreviations 'tx' and 'rx' are traditionally used in many fields for transmitter and receiver respectively.

    thread::spawn(move || { // Using 'move' to move 'tx' into the closure so the spawned thread owns 'tx'.
        let val = String::from("hi");
        tx.send(val).unwrap(); // The 'send' method returns a 'Result<T, E>' type, so if the receiver has already been dropped and there’s nowhere to send a value, the 'send' operation will return an error. In this example, we’re calling 'unwrap' to panic in case of an error.
    });

    let received = rx.recv().unwrap(); // 'recv', short for receive, will block the main thread’s execution and wait until a value is sent down the channel. Once a value is sent, 'recv' will return it in a 'Result<T, E>'. When the transmitter closes, 'recv' will return an error to signal that no more values will be coming.
    println!("Got: {received}");
}
```
Instead of 'recv' we can use 'try_recv' which doesn't block, instead it returns immediately a 'Result<T,E>' containing 'Ok' with message if one is available, else an 'Err' value.<br>
```
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::channel();

    thread::spawn(move || {
        let vals = vec![
            String::from("hi"),
            String::from("from"),
            String::from("the"),
            String::from("thread"),
        ];

        for val in vals { // We iterate over the strings in the vector and send one every second.
            tx.send(val).unwrap();
            thread::sleep(Duration::from_secs(1));
        }
    });

    for received in rx { // We treat 'rx' as an iterator containing the received values. When the channel closes, the iteration ends.
        println!("Got: {received}");
    }
}
```
In the next example we will use multiple threads and transmitters to send messages to one receiver.
```
    let (tx, rx) = mpsc::channel();

    let tx1 = tx.clone(); // We clone the transmitter to have one for each thread.
    thread::spawn(move || {
        let vals = vec![
            String::from("hi"),
            String::from("from"),
            String::from("the"),
            String::from("thread"),
        ];

        for val in vals {
            tx1.send(val).unwrap(); // In this thread we use the cloned transmitter.
            thread::sleep(Duration::from_secs(1));
        }
    });

    thread::spawn(move || {
        let vals = vec![
            String::from("more"),
            String::from("messages"),
            String::from("for"),
            String::from("you"),
        ];

        for val in vals {
            tx.send(val).unwrap(); // In this thread we use the original transmitter.
            thread::sleep(Duration::from_secs(1));
        }
    });

    for received in rx {
        println!("Got: {received}");
    }
```

Instead of sending messages between threads, you can also share data/memory between threads. Shared memory concurrency is like multiple ownership, multiple threads can access the same memory location at the same time. This adds complexity, but mutexes for example can be used to handle this.<br>
Mutex is an abbreviation of mutual exclusion. It takes the shared data and contains one key to access that data. Only one thread at a time can have the key to access the data. Once a thread is done with the data it must free the key so another thread can use it.
```
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let counter = Arc::new(Mutex::new(0)); // We create a mutex within an 'Arc' smart pointer which is a smart pointer that is safe to share between threads.
    let mut handles = vec![];

    for _ in 0..10 {
        let counter = Arc::clone(&counter); // We clone to have a mutex for each thread.
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap(); // We acquire the value contained by the mutex via the 'lock' method.

            *num += 1; // The value contained in the mutex is mutable.
        });
        handles.push(handle);
    }

    for handle in handles {
        handle.join().unwrap();
    }

    println!("Result: {}", *counter.lock().unwrap());
}
```
'Mutex<T>' comes with the risk of creating deadlocks. These occur when an operation needs to lock two resources and two threads have each acquired one of the locks, causing them to wait for each other forever.

Your options for handling concurrency are not limited to the language or the standard library, you can write your own concurrency features or use those written by others. However, two concurrency concepts are embedded in the language, the 'std::marker' traits 'Sync' and 'Send'.<br>
The 'Send' marker trait indicates that ownership of values of the type implementing 'Send' can be transferred between threads. Almost every Rust type is 'Send', but there are some exceptions, including 'Rc<T>'.<br>
The 'Sync' marker trait indicates that it is safe for the type implementing 'Sync' to be referenced from multiple threads. In other words, any type 'T' is 'Sync' if '&T' (an immutable reference to 'T') is 'Send', meaning the reference can be sent safely to another thread. The smart pointers 'Rc<T>', 'RefCell<T>' and the family of related 'Cell<T>' types are not 'Sync'.

### Object-Oriented Programming Features of Rust
Object-oriented programming (OOP) is a way of modeling programs using the programmatic concept of objects. An object is represented in code via attributes/variables representing its characteristics and methods/functions representing its actions.

Rust is influenced by many programming paradigms, including OOP. Rust contains 'structs' and 'enums' with 'impl' blocks to provide methods on them, this is similar to the object functionality.<br>
Another aspect commonly associated with OOP is the idea of encapsulation, which refers to some attributes/methods of objects being private, thus only accessible from within the object itself. In Rust everyting is private by default but becomes public when using the 'pub' keyword.<br>
Inheritance is a mechanism whereby an object can inherit elements from another object’s definition, thus gaining the parent object’s data and behavior without you having to define them again. If a language must have inheritance to be an object-oriented language, then Rust is not one. There is no way to define a 'struct' that inherits the parent 'struct' fields and method implementations without using a macro. However, traits in Rust allow for similar functionality. Inheritance has recently fallen out of favor as a programming design solution in many programming languages because it’s often at risk of sharing more code than necessary. For these reasons, Rust takes the different approach of using trait objects instead of inheritance.

You can use trait objects to get some object-oriented features in Rust. Dynamic dispatch is the process of selecting which implementation of a polymorphic operation to call at run time. Dynamic dispatch can give your code some flexibility in exchange for a bit of runtime performance. You can use this flexibility to implement object-oriented patterns that can help your code’s maintainability. Rust also has other features, like ownership, that object-oriented languages don’t have. An object-oriented pattern won’t always be the best way to take advantage of Rust’s strengths, but is an available option.

### Patterns and Matching
Patterns are a special syntax in Rust for matching against the structure of types. Using patterns in conjunction with 'match' expressions and other constructs gives you more control over a program’s control flow.

We use patterns in the arms of 'match' expressions like this.
```
match VALUE {
    PATTERN => EXPRESSION,
    PATTERN => EXPRESSION,
    PATTERN => EXPRESSION,
}
```
One requirement for 'match' expressions is that they need to be exhaustive in the sense that all possibilities for the value in the match expression must be accounted for. One way to ensure you’ve covered every possibility is to have a catchall pattern for the last arm. The particular pattern '_' will match anything.

Mixing 'if let', 'else if', 'else if let', and 'else' has the advantage compared to 'match' that it can compare multiple values instead of one.

We can also find patterns in loops' conditions. 'let' statements and function parameters also match to a pattern/value.

Patterns that will match for any possible value are irrefutable. An example would be 'x' in the statement `let x = 5;` because 'x' matches anything and therefore cannot fail to match.<br>
Patterns that can fail to match for some possible value are refutable. An example would be 'Some(x)' in the expression `if let Some(x) = a_value` because if the value in the 'a_value' variable is 'None' rather than 'Some', the 'Some(x)' pattern will not match.<br>

You can match patterns against literals directly.
```
let x = 1;

match x {
    1 => println!("one"),
    2 => println!("two"),
    3 => println!("three"),
    _ => println!("anything"),
}
```
Named variables are irrefutable patterns that match any value.
```
let x = Some(5);

match x {
    Some(50) => println!("Got 50"),
    Some(y) => println!("Matched, y = {y}"), //Will match the named variable y.
    _ => println!("Default case, x = {x:?}"),
}
```
In 'match' expressions, you can match multiple patterns using the '|' syntax, which is the pattern 'or' operator.
```
let x = 1;

match x {
    1 | 2 => println!("one or two"),
    3 => println!("three"),
    _ => println!("anything"),
}
```
The '..=' syntax allows us to match to an inclusive range of values.
```
let x = 5;

match x {
    1..=5 => println!("one through five"), //If x is 1, 2, 3, 4, or 5, the first arm will match.
    _ => println!("something else"),
}
```
```
let x = 'c';

match x {
    'a'..='j' => println!("early ASCII letter"),
    'k'..='z' => println!("late ASCII letter"),
    _ => println!("something else"),
}
```
We can also use patterns to destructure structs, enums, and tuples to use different parts of these values.
```
fn main() {
    let p = Point { x: 0, y: 7 };

    let Point { x, y } = p;
    assert_eq!(0, x);
    assert_eq!(7, y);
}
```
You can also match nested enums and structs.
```
enum Color {
    Rgb(i32, i32, i32),
    Hsv(i32, i32, i32),
}

enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(Color),
}

fn main() {
    let msg = Message::ChangeColor(Color::Hsv(0, 160, 255));

    match msg {
        Message::ChangeColor(Color::Rgb(r, g, b)) => {
            println!("Change color to red {r}, green {g}, and blue {b}");
        }
        Message::ChangeColor(Color::Hsv(h, s, v)) => {
            println!("Change color to hue {h}, saturation {s}, value {v}")
        }
        _ => (),
    }
}
```
We can use '_' to ignore a specific value in a pattern or '..' to ignore the remaining values.<br>
```
fn main() {
    let numbers = (2, 4, 8, 16, 32);

    match numbers {
        (first, .., last) => {
            println!("Some numbers: {first}, {last}");
        }
    }
}
```
If you create a variable but don’t use it anywhere, Rust will usually issue a warning because an unused variable could be a bug. However, sometimes it’s useful to be able to create a variable you won’t use yet, such as when you’re prototyping or just starting a project. In this situation, you can tell Rust not to warn you about the unused variable by starting the name of the variable with an underscore.<br>
A match guard is an additional 'if' condition, specified after the pattern in a match arm, that must also match for that arm to be chosen.
```
let num = Some(4);

match num {
    Some(x) if x % 2 == 0 => println!("The number {x} is even"),
    Some(x) => println!("The number {x} is odd"),
    None => (),
}
```
The 'at' operator '@' lets us create a variable that holds a value at the same time as we’re testing that value for a pattern match.
```
enum Message {
    Hello { id: i32 },
}

let msg = Message::Hello { id: 5 };

match msg {
    Message::Hello {
        id: id_variable @ 3..=7, //'id_variable' will hold the value that matched the range 3-7 to use it in subsequent expression.
    } => println!("Found an id in range: {id_variable}"),
    Message::Hello { id: 10..=12 } => {
        println!("Found an id in another range")
    }
    Message::Hello { id } => println!("Found some other id: {id}"),
}
```

### Advanced Features
#### Unsafe Rust
All the code we’ve discussed so far has had Rust’s memory safety guarantees enforced at compile time. However, Rust has a second language hidden inside it that doesn’t enforce these memory safety guarantees, it’s called unsafe Rust and works just like regular Rust, but gives us extra superpowers.<br>
Although the code might be okay, if the Rust compiler doesn’t have enough information to be confident, it will reject the code. In these cases, you can use unsafe code to tell the compiler, “Trust me, I know what I’m doing.”. Be warned, however, that you use unsafe Rust at your own risk. It is best to keep unsafe blocks small.<br>
To switch to unsafe Rust, use the 'unsafe' keyword and then start a new block that holds the unsafe code. You can take five actions in unsafe Rust that you can’t in safe Rust, which we call unsafe superpowers and will discuss below.

The compiler always ensures references to be valid. Unsafe Rust has two new types called raw pointers that are similar to references. As with references, raw pointers can be immutable or mutable and are written as '*const T' and '*mut T', respectively. The asterisk isn’t the dereference operator, it’s part of the type name. In the context of raw pointers, immutable means that the pointer can’t be directly assigned to after being dereferenced. Different from references and smart pointers, raw pointers:<br>
* Are allowed to ignore the borrowing rules by having both immutable and mutable pointers or multiple mutable pointers to the same location<br>
* Aren’t guaranteed to point to valid memory<br>
* Are allowed to be null<br>
* Don’t implement any automatic cleanup

How to create and use an immutable and a mutable raw pointer from references.
```
let mut num = 5;

let r1 = &num as *const i32; // We’ve created raw pointers by using 'as' to cast an immutable and a mutable reference into their corresponding raw pointer types. 
let r2 = &mut num as *mut i32;

unsafe { // We can create raw pointers in safe code, but we can’t dereference raw pointers and read the data being pointed to in safe code.
    println!("r1 is: {}", *r1);
    println!("r2 is: {}", *r2);
}
```
Raw pointers are useful when interfacing with C code or when building up safe abstractions that the borrow checker doesn't understand.

Unsafe functions and methods look exactly like regular functions and methods, but they have an extra 'unsafe' before the rest of the definition `unsafe fn dangerous() {}`. Bodies of unsafe functions are effectively unsafe blocks. 

Sometimes, your Rust code might need to interact with code written in another language. For this, Rust has the keyword 'extern' that facilitates the creation and use of a Foreign Function Interface (FFI). An FFI is a way for a programming language to define functions and enable a different (foreign) programming language to call those functions. Functions declared within 'extern' blocks are always unsafe to call from Rust code. The reason is that other languages don’t enforce Rust’s rules and guarantees.
```
extern "C" {
    fn abs(input: i32) -> i32; //Integration with the 'abs' function from the 'C' standard library.
}

fn main() {
    unsafe {
        println!("Absolute value of -3 according to C: {}", abs(-3));
    }
}
```
Within the extern 'C' block, we list the names and signatures of external functions from another language we want to call. The 'C' part defines which application binary interface (ABI) the external function uses, the ABI defines how to call the function at the assembly level. The 'C' ABI is the most common and follows the 'C' programming language’s ABI.<br>
We can also use 'extern' to create an interface that allows other languages to call Rust functions. Instead of creating a whole 'extern' block, we add the 'extern' keyword and specify the ABI to use just before the 'fn' keyword for the relevant function. We also need to add a '#[no_mangle]' annotation to tell the Rust compiler not to mangle the name of this function. Mangling is when a compiler changes the name we’ve given a function to a different name that contains more information for other parts of the compilation process to consume but is less human readable. Every programming language compiler mangles names slightly differently, so for a Rust function to be nameable by other languages, we must disable the Rust compiler’s name mangling.
```
//In the following example, we make the 'call_from_c' function accessible from 'C' code, after it’s compiled to a shared library and linked from 'C'.
#[no_mangle]
pub extern "C" fn call_from_c() {
    println!("Just called a Rust function from C!");
}
```

Rust supports global variables, those are called static variables. Static variables are constants and by convention are written in SCREAMING_SNAKE_CASE. However, when using unsafe rust they can be mutated. With mutable data that is globally accessible, it’s difficult to ensure there are no data races, which is why Rust considers mutable static variables to be unsafe. Where possible, it’s preferable to use the concurrency techniques and thread-safe smart pointers.
```
static mut COUNTER: u32 = 0;

fn add_to_count(inc: u32) {
    unsafe {
        COUNTER += inc;
    }
}

fn main() {
    add_to_count(3);

    unsafe {
        println!("COUNTER: {COUNTER}");
    }
}
```

We can use 'unsafe' to implement an unsafe trait. A trait is unsafe when at least one of its methods has some invariant that the compiler can’t verify. We declare that a trait is unsafe by adding the unsafe keyword before trait and marking the implementation of the trait as unsafe too.
```
unsafe trait Foo {
    // methods go here
}

unsafe impl Foo for i32 {
    // method implementations go here
}
```

Unions are primarily used to interface with unions in C code. Accessing union fields is unsafe because Rust can’t guarantee the type of the data currently being stored in the union instance.

Using unsafe to take one of the five actions (superpowers) just discussed isn’t wrong or even frowned upon. When you have a reason to use unsafe code, you can do so, and having the explicit 'unsafe' annotation makes it easier to track down the source of problems when they occur.

#### Advanced Traits
Associated types connect a type placeholder with a trait such that the trait method definitions can use these placeholder types in their signatures.<br>
One example of a trait with an associated type is the 'Iterator' trait that the standard library provides. The associated type is named 'Item'.
```
pub trait Iterator {
    type Item;
    //The type 'Item' is a placeholder, and the 'next' method’s definition shows that it will return values of type 'Option<Self::Item>'.
    fn next(&mut self) -> Option<Self::Item>;
}
```
Implementors of the 'Iterator' trait will specify the concrete type for 'Item', and the 'next' method will return an 'Option' containing a value of that concrete type.
```
impl Iterator for Counter {
    type Item = u32;

    fn next(&mut self) -> Option<Self::Item> {
        // --snip--
```
The difference with generics, is that with generics you can define a different type on each function call while with associated types we only define a type once in the 'impl' block.

Sometimes, you might write a trait definition that depends on another trait, for a type to implement the first trait, you want to require that type to also implement the second trait. You would do this so that your trait definition can make use of the associated items of the second trait. The trait your trait definition is relying on is called a supertrait of your trait.

#### Advanced Types
Rust provides the ability to declare a type alias to give an existing type another name. For this we use the 'type' keyword. For example, we can create the alias 'Kilometers' to 'i32' like so `type Kilometers = i32;` or `type Thunk = Box<dyn Fn() + Send + 'static>;`.

Rust has a special type named '!' that’s known in type theory lingo as the empty type because it has no values. We prefer to call it the never type because it stands in the place of the return type when a function will never return.
```
fn bar() -> ! {
    // --snip--
}
```

Dynamically sized types (DSTs) also called unsized types, let us write code using values whose size we can know only at runtime.<br>
'str' is a DTS because we do not know its size until runtime.<br>
To work with DSTs, Rust provides the 'Sized' trait to determine whether or not a type’s size is known at compile time. This trait is automatically implemented for everything whose size is known at compile time.

#### Advanced Functions and Closures
We’ve talked about how to pass closures to functions, but you can also pass regular functions to functions. Passing functions with function pointers will allow you to use functions as arguments to other functions.
```
fn add_one(x: i32) -> i32 {
    x + 1
}

fn do_twice(f: fn(i32) -> i32, arg: i32) -> i32 { //The function 'do_twice' takes two parameters: a function pointer to any function that takes an 'i32' parameter and returns an 'i32', and one 'i32' value.
    f(arg) + f(arg) //The 'do_twice' function calls the function 'f' twice, passing it the 'arg' value, then adds the two function call results together.
}

fn main() {
    let answer = do_twice(add_one, 5);

    println!("The answer is: {answer}");
}
```

#### Macros
We’ve used macros like println! throughout this book, but we haven’t fully explored what a macro is and how it works. The term macro refers to a family of features in Rust, consisting of declarative macros and three kinds of procedural macros. We will talk about each.

Fundamentally, macros are a way of writing code that writes other code, which is known as metaprogramming. Macros expand to produce more code than the code you’ve written manually.<br>
Metaprogramming is useful for reducing the amount of code you have to write and maintain, which is also one of the roles of functions. However, macros have some additional powers that functions don’t. A function signature must declare the number and type of parameters the function has. Macros, on the other hand, can take a variable number of parameters, for example we can call 'println!("hello")' with one argument or 'println!("hello {}", name)' with two arguments. The downside to implementing a macro instead of a function is that macro definitions are more complex than function definitions because you’re writing Rust code that writes Rust code.

The most widely used form of macros in Rust is the declarative macro. At their core, declarative macros allow you to write something similar to a Rust match expression. Macros also compare a value to patterns that are associated with particular code, in this situation, the value is the literal Rust source code passed to the macro, the patterns are compared with the structure of that source code, and the code associated with each pattern, when matched, replaces the code passed to the macro. This all happens during compilation.
```
#[macro_export] //Without this annotation, the macro can’t be brought into scope.
macro_rules! vec { //We start the macro definition with 'macro_rules!' and its name.
    ( $( $x:expr ),* ) => { //The structure in the 'vec!' body is similar to the structure of a match expression. Here we have one arm with the pattern '( $( $x:expr ),* )', followed by '=>' and the block of code associated with this pattern. If the pattern matches, the associated block of code will be emitted. Given that this is the only pattern in this macro, there is only one valid way to match.
        {
            let mut temp_vec = Vec::new();
            $(
                temp_vec.push($x); //'temp_vec.push()' within '$()*' is generated for each part that matches '$()' in the pattern zero or more times depending on how many times the pattern matches.
            )*
            temp_vec
        }
    };
}
```
When we call this macro with `vec![1, 2, 3];`, the `$x` pattern matches three times with the three expressions `1`, `2`, and `3`. The `$x` is replaced with each expression matched. When we call this macro with `vec![1, 2, 3]`, the code generated that replaces this macro call will be the following.
```
{
    let mut temp_vec = Vec::new();
    temp_vec.push(1);
    temp_vec.push(2);
    temp_vec.push(3);
    temp_vec
}
```

The second form of macros is the procedural macro, which acts more like a function (and is a type of procedure). Procedural macros accept some code as an input, operate on that code, and produce some code as an output rather than matching against patterns and replacing the code with other code as declarative macros do.

### Appendix

#### Appendix A: Keywords
[Link](https://doc.rust-lang.org/book/appendix-01-keywords.html)

#### Appendix B: Operators and Symbols
[Link](https://doc.rust-lang.org/book/appendix-02-operators.html)

#### Appendix C: Derivable Traits
[Link](https://doc.rust-lang.org/book/appendix-03-derivable-traits.html)

#### Appendix D: Useful Development Tools
The 'rustfmt' tool reformats your code according to the community code style. Many collaborative projects use rustfmt to prevent arguments about which style to use when writing Rust. To install 'rustfmt', enter the following: `rustup component add rustfmt`.

The 'rustfix' tool is included with Rust installations and can automatically fix compiler warnings that have a clear way to correct the problem that’s likely what you want. Error fixes suggested by the compiler can be applied using the command `cargo fix`.

The 'Clippy' tool is a collection of lints to analyze your code so you can catch common mistakes and improve your Rust code.
```
rustup component add clippy //Install
cargo clippy //Run
```
An example error it could for example find would be the use of `let x = 3.1415;` instead of Rust's constant `PI`.

Your IDE can gain abilities such as autocompletion, jump to definition, and inline errors, while writing rust, by using 'rust-analyzer' plugin for your IDE.

#### Appendix E: Editions
[Link](https://doc.rust-lang.org/book/appendix-05-editions.html)

#### Appendix G: How Rust is Made and “Nightly Rust”
Rust’s development model follows a Request For Comments (RFC) process. If you’d like an improvement in Rust, you can write up a proposal, called an RFC. Anyone can write RFCs to improve Rust, and the proposals are reviewed and discussed by the Rust team, which is comprised of many topic subteams. If the feature is accepted, an issue is opened on the Rust repository, and someone can implement it.

[See more](https://doc.rust-lang.org/book/appendix-07-nightly-rust.html)

## Resources
[The Rust Programming Language](https://doc.rust-lang.org/book/title-page.html)
