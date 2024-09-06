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

## Resources
[The Rust Programming Language](https://doc.rust-lang.org/book/title-page.html)
