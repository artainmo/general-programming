# OCaml

## Table of contents
- [Free tutorials](#Free-tutorials)
- [Resources](#Resources)

## Free tutorials
### Introduction
OCaml is a functional programming language. Functional meaning it is written using functions over objects/classes. Although object oriented features exist in OCaml they are considered bad practice and rarely used in this language. 

An ocaml interactive shell can be launched with the command `ocaml`. Its commands should end with `;;` while this is not the case in a compiled OCaml program.

OCaml programs should be written inside '.ml' source files. Two compilers exist, 'ocamlc' compiles to byte-code and 'ocamlopt' to machine code. The machine code executes faster but takes more time to compile.<br>
`ocamlc -g -c file.ml` will produce 'file.cmo' while 'ocamlopt' would procude 'file.cmx'. `-g` is used for debug info to be included in output file. Afterwards the output files will have to be linked like this `ocamlc -g -o executableName file1.cmo file2.cmo` to form an executable that can be executed `./executableName`.

Comments are written in between `(*` and `*)`.

### Data types and conditions
In ocaml the following variable types exist: unit, int, char, float, bool, string. Type inference allows automatic type deduction without the need to explicitly specify the type.

The 'unit' type refers to `()` which represent what 'void' represents in C.

Integers can use `+`, `-`, `*`, `/`, `mod` (modulo, remainder of division)... Floats use the same arithemtic operators but with a '.' like `+.`, `-.`, `*.`, `/.`... Conversion between float and int is also possible with `int_of_float x` and `float_of_int x`.

Like in c, chars describe characters that use single brackets in their syntax `'v'`. Escape characters start with a backslash, for example `\\`, `\'`, `\n`...

Unlike strings in C, character strings are not arrays of characters, and they do not use the null-character ’\000’ for termination. The syntax for strings uses the double-quote symbol " as a delimiter.<br>
The operator `^` performs string concatenation.<br>
Strings also support random access. The expression `s.[i]` returns the i’th from string 's' and the expression `s.[i] <- c` replaces the i’th in string 's' by character 'c'.<br>
The String module (see Section 8.3) also defines many functions to manipulate strings, including the 'String.length' function, which returns the length of a string and the 'String.sub' function, which returns a substring.

Bools are a binary data type holding the value 'true' or 'false'.<br>
Logical operators compare two values and return a bool. Such operators are for example ==, !=, <, <=, >, >= but also = and <> which means 'equal to' and 'not equal to' instead of 'identical' to.<br> 
The `||` (or)  and `&&` (and) operators can also be used in conditions.<br>
Conditions are written like this:
```
if 1 < 2 then
	3 + 7
else
	4

It is important to know that each expression in OCaml has one type. Each expression returns a value which also has a type, sometimes it is the trivial unit type `()`.
```

While other languages usually use a switch statement, OCaml has the 'match' statement. It looks for example like this:
```
match i with
	0 -> "zero"
	1 -> "one"
	2 -> "three"
```
The body of a OCaml function can also only consist of such a match statement where the sole function parameter is matched against patterns, such a function uses the keyword 'function' instead of 'fun'.<br>
Patterns can be defined in more complex ways, if a pattern should consist of multiple values those can be separated using `value1 | value2 | value3`, if you want the whole alphabet you can use the pattern `'A'..'Z'`. A pattern that matches everything is indicated with `_`, usually then an error is raised like this `_ -> raise (Invalid_argument "personal message")`.<br>

### Variables, Functions, Looping 
Variables are defined using the 'let' keyword like this `let variableName = expression`. 

Functions are defined using the 'fun' keyword like this `fun parameterName1, parameterName2 -> expression`. Be default functions are anonymous in OCaml. To name them make them equal a variable `let functionName = fun paramName -> expression`. The 'expression' result or last line of function body will be returned. Functions can be called like this `functionName param1` and parantheses are used for arguments that are an expression `functionName (2 * 3)`. They keywords 'begin' 'end' can replace parantheses.<br>
Alternatively named functions can be defined like this `let functionName param1 param2 = expression`.

Recursive functions are defined with 'rec' keyword like this `let rec functionName param = expression` with 'expression' calling at some point its function.<br>
Recursion is the primary means for specifying looping and iteration, making it one of the most important concepts in functional programming. However OCaml also offers the possibility of using 'for' and 'while' loops. OCaml provides both 'for' and 'while' loops, but there is no 'break' statement as found in languages like C and Java. Instead, exceptions can be used to abort a loop prematurely.

Contrary to other languages we can name variables and functions with arithmetic operators. This allows us for example to name a function `let ( ** ) x i = power i x` and use this function like this `10 ** 5` which equals 100000.

Function parameters can also be labeled which allows the arguments of the function call to be in a non-specific order. To indicate labeled parameters and arguments a tidle `~` is used.<br>
Function parameters can also be optional. This is indicated using '?' like this `let functionName ?(param1=1) param2 = param1 - param2`.<br>
You can also explicitly indicate what function parameter or return type should be like this ` let functionName (i : int) : bool = expression;` where int is the parameter type and bool the return type.

### Tuples, Lists and Unions
A tuple is a collection of values of arbitrary types.<br>
The syntax for a tuple is a sequence of expressions separated by commas. For example `let tuple = 1, "Hello World"`, which can be deconstructed like this `let x, y = tuple` with x taking the first tuple value and y the second.<br>
Tuples can be useful to let functions return multiple values.

Lists are also used extensively in OCaml programs. A list is a sequence of immutable values of the same type.<br>
There are two constructors, one like this `[element1; element2;]` and another like this `element1 :: element2 :: []`.<br>
Lists can also contain tuples or other lists as long as all its elements have the same type.

A disjoint union, or union for short, represents the union of several different types, where each of the parts is given an
unique, explicit name.<br>
OCaml allows the definition of exact and open union types. The following syntax is used for an exact union type:
```
type unionTypeName = 
	identifier of type1
	identifier of type2
```
An open union type is able to add more cases to the type during subsequent definitions. The syntax is similar to the previous exact union type, but the identifier names are predefined with a back-quote (').

### Reference cells
By default variables are constants in OCaml. To make variables mutable in OCaml we need to define 'reference cells'. Reference cells can be seen as a box that contains a value that is mutable, meaning the value it contains can change by being reassigned a new one.<br>
Reference cells are created using the 'ref' keyword like this `let variableName = ref value`. To access the value inside a reference cell we need to use the '!' symbol like this `!variableName`.

### Records, Arrays, and String
A record is like a tuple where the elements of the tuple are named. Arrays and strings are fixed-length sequences of data supporting random access to the elements. All three types support mutation of elements, by assignment.

A record is a labeled collection of values of arbitrary types. Here is how we define a record:
```
type db_entry = { 
	name : string;
	height : float;
	phone : string;
	mutable salary : float (*The mutable keyword is used to indicate the associated field can be updated*)
};
```
And here is how we define a record value of that type:
```
let jason = {
	name = "Jason";
	height = 6.25;
	phone = "626-555-1212"
	salary = 50.0
}
```
With its values being accessible like that `jason.height` for example. The 'salary' field is mutable and can be updated like this `jason.salary <- 150.0`.


Arrays are fixed-size vectors of values whereby all the values must have the same type, can be accessed and modified. They are created with the following syntax `let arrayName = [| element1; element2; element3 |]`. The values it contains are accessed like this `arrayName.(3)` whereby we access value at index 3. And values are updated like this `arrayName.(3) <- newValue`.<br>
The Array module also contains functions for arrays such as `Array.length arrayName`.

Strings are like arrays of characters. A string can be defined like this `let stringName = "Jason"`. Its elements accessed like this `stringName.[3]` whereby we access the character at index 3. And characters are updated like this `stringName.[3] <- 's'`.<br>
The String module also contains functions for strings such as `String.length stringName`.

### Exceptions
Exceptions are used to signal errors. They are triggered automatically or they can be defined explicitly by the programmer.<br>
They can be defined like this:
```
exception Fail of string (*Means we define an exception named 'Fail' with one argument of type 'string'*)
raise (Fail "error message") (*Here we trigger the exception*)
```
When an exception is raised it is passed to the currently active exception handler. Exception handlers can be defined like match patterns but using the 'try' keyword instead of the 'match' keyword.

Examples of automatically triggered exceptions that you could manually raise too are for example 'Not_found' when searching, 'Invalied_argument' when a function received a wrong argument...

In some cases it is useful to define a 'finally' cause when 'trying' an exception. The purpose of a 'finally' clause is to execute some code (usually to clean up) after an expression is evaluated, no matter if the exception was raised or not.

### Input and Output


## Resources
[Introduction to Objective Caml](http://courses.cms.caltech.edu/cs134/cs134b/book.pdf)<br>
