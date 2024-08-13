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

## Resources
[The Rust Programming Language](https://doc.rust-lang.org/book/title-page.html)
