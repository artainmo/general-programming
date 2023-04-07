# OCaml

## Table of contents
- [OCaml Free tutorials](#OCaml-Free-tutorials)
  - [Introduction](#Introduction)
  - [Separation of commands](#Separation-of-commands)
  - [Data types and conditions](#Data-types-and-conditions)
  - [Variables, Functions, Looping](#variables-functions-looping)
  - [Tuples, Lists and Unions](#tuples-lists-and-unions)
  - [Reference cells](#reference-cells)
  - [Records, Arrays, and String](#records-arrays-and-string)
  - [Exceptions](#Exceptions)
  - [Input and Output](#Input-and-Output)
  - [Files, Compilation Units, and Programs](#files-compilation-units-and-programs)
  - [OCaml Modules](#OCaml-Modules)
- [Ocsigen Free tutorials](#Ocsigen-Free-tutorials)
  - [OCsigen introduction](#OCsigen-introduction)
  - [Lwt](#Lwt)
  - [TyXML](#TyXML)
  - [Eliom: Services](#eliom-services)
  - [Forms and links](#Forms-and-links)
  - [Js_of_ocaml](#Js_of_ocaml)
  - [Eliom: client-server apps](#Eliom-client-server-apps)
  - [Sessions](#Sessions)
  - [Browser events](#Browser-events)
  - [Ocsigen Toolkit](#Ocsigen-Toolkit)
  - [Ocsigen Start](#Ocsigen-Start)
  - [Server to client communication](#Server-to-client-communication)
  - [Reactive programming](#Reactive-programming)
  - [Ocsigen-Server](#Ocsigen-Server)
- [Resources](#Resources)

## OCaml Free tutorials
### Introduction
OCaml is a functional programming language. Functional meaning it is written using functions over objects/classes. Although object oriented features exist in OCaml they are considered bad practice and rarely used in this language. 

OCaml programs should be written inside '.ml' source files. Two compilers exist, 'ocamlc' compiles to byte-code and 'ocamlopt' to machine code. The machine code executes faster but takes more time to compile, because it is the final code while byte-code is an intermediate code.<br>
`ocamlc -g -c file.ml` will produce 'file.cmo' while 'ocamlopt' would procude 'file.cmx'. `-g` is used for debug info to be included in output file. Afterwards the output files will have to be linked like this `ocamlc -g -o executableName file1.cmo file2.cmo` to form an executable that can be executed `./executableName`.

Comments are written in between `(*` and `*)`.

### Separation of commands
An OCaml interactive shell can be launched with the command `ocaml`. The end of expressions should be indicated with `;;`.<br>

In OCaml programs however separating commands is more complicated because whitespace and line-returns are not able to split commands.<br>
'let' bindings or function definitions are the convention for separating expressions.<br>
In OCaml, 'let' bindings are used to bind a name to a value. A 'let' binding has the following syntax: `let <name> = <expression>` where 'name' is the name of the binding and can equal to `()` if you don't want to actually bind to a name, 'expression' is the value to which 'name' is bound.<br>
In the following example an error occurs because the function's last expression doesn't get separated with the expression that follows it.
```
let stop code =
	exit code

let x = 10 in let y = x + 1 in Printf.prinf "%d %d" x y
```
Because in OCaml whitespace and line-returns do not split commands the above code is similar to:
```
let stop code =
	exit code (let x = 10 in let y = x + 1 in Printf.prinf "%d %d" x y)
```
Which creates an error because the 'exit' function should only have one argument.<br>
However using 'let' binding we can correctly separate the commands:
```
let stop code =
	exit code

let () =
	let x = 10 in let y = x + 1 in Printf.prinf "%d %d" x y
```
`let x = 10 in let y = x + 1 in Printf.prinf "%d %d" x y` is an expression because it uses the 'in' keyword. The 'in' keyword splits commands in one expression and allows the declared variable in one command to be usable in one of the next commands. Using `let () =` we can bind this expression to 'let' which allows separation of expressions.<br>
`;;` can also separate expressions in programs like they do in the interactive shell however they are not the convention in OCaml. Here is an example of its use:
```
let stop code =
	exit code
;;

let x = 10 in let y = x + 1 in Printf.prinf "%d %d" x y
```
A single semicolon can split commands within one expression. For example:
```
let stop code =
	Printf.printf "stopping the program with code %d" code ; exit code
```
As whitespace is not relevant for the OCaml compiler it can also be written like this:
```
let stop code =
	Printf.printf "stopping the program with code %d" code; 
	exit code
```

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
For example:
```
"foo" == "foo" (*Equals to false because they are not identical meaning they don't lie on same memory space*)
"foo" = "foo" (*Equals to true as we would expect*)
```
The `||` (or)  and `&&` (and) operators can also be used in conditions.<br>
Conditions are written like this:
```
if 1 < 2 then
	3 + 7
else if 1 == 3
	9
else begin
	Printf.printf "Error";
	exit 0
end (*Because the else close contains multiple expressions it needs to be closed between 'begin' and 'end' keywords*)
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
There are two constructors, one like this `[element1; element2; element3]` and another like this `element1 :: element2 :: []`.<br>
Lists can be joined together using `list1 @ list2`, similarly a value can be appended to the end of a list like this `list @ [newValue]`. However appending at end of lists demands to copy and joining two lists which is more demanding than adding a value to the front of a list like this `newValue :: list1`.<br>
Lists can also contain tuples or other lists as long as all its elements have the same type.

A disjoint union, or union for short, represents the union of several different types, where each of the parts is given a unique, explicit name.<br>
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
	phone = "626-555-1212";
	salary = 50.0
}
```
With its values being accessible like that `jason.height` for example. The 'salary' field is mutable and can be updated like this `jason.salary <- 150.0`.


Arrays are fixed-size vectors of values whereby all the values must have the same type, can be accessed and modified. They are created with the following syntax `let arrayName = [| element1; element2; element3 |]`. The values it contains are accessed like this `arrayName.(3)` whereby we access value at index 3. And values are updated like this `arrayName.(3) <- newValue`.<br>
The Array module also contains functions for arrays such as `Array.length arrayName`.

Strings are like arrays of characters. A string can be defined like this `let stringName = "Jason"`. Its elements accessed like this `stringName.[3]` whereby we access the character at index 3.<br>
In OCaml, strings are immutable, which means that you cannot change the value of a character in a string directly. However, you can create a new string with the updated character.<br>
The String module also contains functions for strings such as `String.length stringName`.

### Exceptions
Exceptions are used to signal errors. They are triggered automatically or they can be defined explicitly by the programmer.<br>
They can be defined like this:
```
exception Fail of string (*Means we define an exception named 'Fail' with one argument of type 'string'*)
raise (Fail "error message") (*Here we trigger the exception*)
```
When an exception is raised it is passed to the currently active exception handler. Exception handlers can be defined like match patterns but using the 'try' keyword instead of the 'match' keyword.

Examples of automatically triggered exceptions that you could manually raise too are for example 'Not_found' when searching, 'Invalid_argument' when a function received a wrong argument...

In some cases it is useful to define a 'finally' cause when 'trying' an exception. The purpose of a 'finally' clause is to execute some code (usually to clean up) after an expression is evaluated, no matter if the exception was raised or not.

### Input and Output
At program startup, there are three channels open, corresponding to the standard file descriptors in Unix, who allow reading and writing in terminal, namely the 'stdin' is the standard input stream, 'stdout' is the standard
output stream, and 'stderr' is the standard output stream for error messages.

In OCaml the I/O library starts by defining two data types, namely 'in_channel' and 'out_channel' who represent the channels from which characters can be read or written respectively.

To open a file we can use the function 'open_out' for writing text data and 'open_out_bin' for writing binary data. Similarly for opening and reading files we can use the functions 'open_in' and 'open_in_bin'.<br>
The 'open_out_gen' and 'open_in_gen' functions can be used to perform more kinds of file openings such as for appending, create if not exist, empty file if it already exist, fail if file already exist...<br>
Channels are not closed automatically. The closing functions 'close_out' and 'close_in' are used for explicitly closing the channels.

There are several functions for writing values to an 'out_channel'. The 'output_char' writes a single character to the channel, and the 'output_string' writes all the characters in a string to the channel. The 'output' function can be used to write part of a string to the channel.<br>
The 'input_char' function reads a single character, and the 'input_line' function reads an entire line, discarding the line terminator. The input functions raise the exception 'End_of_file' if the end of the file is reached before the entire value could be read.

If the channel is a normal file, there are several functions that can modify the position in the file. The 'seek_out' and 'seek_in' function change the file position. The 'pos_out' and 'pos_in' function return the current position in the file. The 'out_channel_length' and 'in_channel_length' return the total number of characters in the file.

The Buffer library module provides string buffers that can, in some cases, be significantly more efficient than using the native string operations. String buffers have type 'Buffer.t'. Buffers are created with the 'Buffer.create' function. Different functions also exist to clear, add text to buffer or output the buffer.

OCaml has the function 'fprintf' found in module 'Printf' which allows formatted output. For example, the following statement prints a line containing an integer 'i' and a string 's': `Printf.fprintf stdout "Number = %d, String = %s\n" i s`. When printing in terminal instead of using `fprintf stdout "message"` one can use `printf "message"`.<br>
The Printf module also provides formatted output to a string buffer. The 'bprintf' function takes a printf-style format string, and formats output to a buffer.

The Scanf module is similar to Printf, but for input instead of output. The 'fscanf' function reads from an input channel, the 'sscanf' function reads from a string, and the 'scanf' function reads from the standard input.

### Files, Compilation Units, and Programs
Learn more about compilation in the [introduction](#Introduction).

Unlike C programs, OCaml programs do not have a 'main' function. When an OCaml program is evaluated, all the statements in the implementation files are evaluated in order.<br>
OCaml is vaguely like a scripting language in that any top-level expressions are evaluated when you start up the program. It's conventional to have a function named 'main' that invokes the main work of your program. But it's not necessary at all.<br>
Expressions are evaluated in the order that the OCaml files appeared in when they were linked into an executable.

OCaml uses files as a basic unit for providing data hiding and encapsulation. Each file can be assigned an 'interface' that declares types for that file. An interface for a file 'filename.ml' is defined in a file with same name named 'filename.mli'. An interface should declare types for each of the values that are publicly accessible in a module, as well as any needed type declarations or definitions. '.mli' files need to be compiled but don't need to be specified during linking.

At top of file you can 'open' a library, which means its implementations become directly accessible. For example by using `open Array` one can use the `create` function to create an array. Without the 'open' the same function is found like this `Array.open`. The use of 'open' is not recommended as it can easily lead to errors from different implementations with same name leading to ambiguity.

The 'ocamldebug' program can be used to debug a program compiled with 'ocamlc'. The 'ocamldebug' program is a little like the 'GNU gdb' program. It allows breakpoints to be set. When a breakpoint is reached, control is returned to the debugger so that program variables can be examined. To use 'ocamldebug', the program must be compiled with the `-g` flag. The debugger is invoked like this `ocamldebug ./programExecutable`. After the debugger has been launched it will prompt you for commands that allow you to execute and visualize the program's variable at a specific time point.

### OCaml Modules
As we saw in the previous chapter, programs can be divided into parts that can be implemented in files, and each file can be given an interface that specifies what its public types and values are.<br>
Files are not the only way to partition a program, OCaml also provides a 'module' system that allows programs to be partitioned even within a single file. There are three key parts in the module system: 'signatures', 'structures', and 'functors', where 'signatures' correspond to interfaces, 'structures' correspond to implementations, and 'functors' are functions over structures. 

Named structures are defined with the module and struct keywords using the following syntax: `module ModuleName = struct implementation end`. The module name  must begin with an uppercase letter. The implementation can include any definition that might occur in a '.ml' file.

As we saw before each '.ml' file contains implementations that can be linked to an interface defined a '.mli' file. Modules allow the same, the implementations are defined in a 'structure' and the interface is defined in a 'signature'.<br>
A signature must have the same name as the structure it is linked to and be defined like that: `module type ModuleName = sig interface end`.<br>
The values defined inside the signature will be accessible outside the module like this `ModuleName.value`.

The 'let module' expression is frequently used for creating modules for local use. It is defined like that `let module ModuleName = module_expression in body_expression`, whereby 'module_expression' refers to the content of the module and 'body_expression' refers to the Ocaml code that would have access to that module.

'include' keyword allows to include the contents of one 'structure' or 'signature' into another.<br>
Modules can also be nested.

All the module references we’ve seen up to this point have been to specific, constant modules. It’s also possible in OCaml to write modules that are parameterized by other modules. To be used, 'functors' are instantiated by supplying actual module arguments for the functor’s module parameters (similar to supplying arguments in a function call). A functor parameter must be a module, or another functor.<br>
It is defined like this `module ModuleName type (Structure: Signature) = struct implementations end` whereby inside the implementations the module given as argument can be accessed.

## Ocsigen Free tutorials
### Ocsigen introduction
Ocsigen is an OCaml framework for developing web or mobile apps. It can both be used client or server side.

Ocsigen consists of several independent open-source projects such as 'Lwt', 'TyXML', 'Js_of_ocaml', 'Eliom', 'Ocsigen Server', 'Ocsigen Toolkit', 'Ocsigen Start'. Some of which we will cover later.

### Lwt
Lwt is a concurrent programming library for OCaml allowing promises like in javascript.

This library contains the 'Lwt_unix.sleep 1.0' function to temporarily halt program execution concurrently, meaning only the function it is used in gets blocked not the rest of the program.<br>
`let p = f () in Lwt.bind p (fun x -> Lwt.return e)` allows the creation of an asynchronous function that executes concurrently and returns a promise using 'Lwt.return' to 'p'.<br>
To detach a thread one can use `Lwt.async (fun () -> f ())`.

It is also possible to handle exceptions using this library with `Lwt.fail`, 'Lwt.catch'... Also the possibility exists to create a thread that waits until it is awaken with `Lwt.wait` and `Lwt.wakeup`.

### TyXML
Verifies during compilation that your OCaml functions will never generate wrong HTML.

Tyxml defines a constructor for each HTML tag and attribute. For example:
```
html
     (head (title (txt "Hello")) [])
     (body [ h1 [txt "Hello"] ;
             p [txt "Blah"] ])
```

Eliom uses TyXML to create several kinds of nodes:<br>
Module 'Eliom_content.Html.D' will automatically insert an id in the attributes of the node, to label a precise instance of the node in the DOM. On client side, calling 'Eliom_content.Html.To_dom.of_element' on these nodes will return the actual version of the nodes that are currently in the page.<br>
In a client server Eliom app, you probably always want to use 'Eliom_content.Html.D' each time you want to bind events on an element

Module 'Eliom_content.Html.R' makes it possible to create reactive nodes, that is, nodes that will be updated automatically when the data on which they depend change. It is based on module 'React', which implements functional reactive programming for OCaml.

### Eliom: Services
Eliom is a client-side library. It generates pages via 'services'. Eliom provides a service creation and identification mechanism.

To create a service use `Eliom_service.create` and to register a handler on that service use `Eliom_registration.Html.register` like this:
```
let myservice =
  Eliom_service.create
    ~path:(Eliom_service.Path ["foo"])
    ~meth:(Eliom_service.Get (Eliom_parameter.(string "myparam" ** int "i"))) (* /foo?myparam=FortyTwo&i=42 *)
    ()
    
let () =
  Eliom_registration.Html.register ~service:myservice
    (fun (myparam, i) () ->
      Lwt.return
         Eliom_content.Html.F.(html (head (title (txt "")))
                                    (body [h1 [txt myparam]])))
```
The prior code first defines a service at URL '/foo', that will use 'GET' HTTP method, and take one parameter of type 'string', named 'myparam', and one of type 'int', named 'i'.<br>
Module `Eliom_parameter` is used to describe the type of service parameters.<br>
Second the prior code registers a handler on the service. The handler function takes the parameters specified by the service and returns an HTML page defined using 'TyXML'. However handlers can also return other types of values.

### Forms and links
Functions 'Eliom_content.Html.F.a' and 'D.a' create links to services with their parameters. For example, if 'home_service' expects no parameter and 'other_service' expects a 'string' and an optional 'int':
```
Eliom_content.Html.D.a ~service:home_service [txt "Home"] ()
Eliom_content.Html.D.a ~service:other_service [txt "Other"] ("hello", Some 4)
```

Modules 'Eliom_content.Html.F' and 'D' define the form's elements with the usual 'TyXML'.<br>
In contrast, modules 'Eliom_content.Html.F.Form' and 'D.Form' define form elements.<br>
Example:
```
let open Eliom_content.Html.D in
Form.post_form
 ~service:connection_service
   (fun (name, password) ->
     [fieldset
       [label ~a:[a_for name] [txt "Name: "];
        Form.input ~input_type:`Text ~name:name Form.int;
        br ();
        Form.input
          ~a:[a_placeholder "Password"]
          ~input_type:`Password
          ~name:password
          Form.string;
        br ();
        Form.input ~input_type:`Submit ~value:"Connect" Form.string
      ]]) ()
```

### Js_of_ocaml
Js_of_ocaml is a compiler of OCaml bytecode to JavaScript, allowing to run Ocaml programs in a web-browser.

Use modules 'Js_of_ocaml.Dom' and 'Js_of_ocaml.Dom_html' to interact with the DOM, or more specifically with HTML.<br>
Functions 'Eliom_content.Html.To_dom.of_element', 'Eliom_content.Html.To_dom.of_div', etc. help to convert TyXML/Eliom_content nodes into the DOM counterparts.

### Eliom: client-server apps
Eliom allows both client and server side to be written in OCaml, simplifying communication between the two. 

It generates two pragrams from the same set of OCaml files. One compiled to bytecode to be executed on the server and the other compiled to javascript with 'Js_of_ocaml' to be executed in browser.<br>
PPX annotations allow to split the code into these two programs:<br>
```
let%client ... = ... (* Code to be included in client app *)
let%server ... = ... (* Code to be included in server app *)
let%shared ... = ... (* Code to be included both in client and server app *)
(* Same for module%shared, open%shared, type%shared etc. *)
```
Service handlers and service registration are usually written in shared sections to enable page generation on both sides.

### Sessions
Session data is saved on server side in Eliom 'references'. The following Eliom reference will count the number of visits of a user on a page:
```
let%server count_ref =
  Eliom_reference.eref
    ~scope:Eliom_common.session
    0 (* default value for everyone *)
    
let%lwt count = Eliom_reference.get count_ref in
Eliom_reference.set count_ref (count + 1);
Lwt.return ()
```

### Browser events
Attributes like 'a_onclick' in module 'Eliom_content.Html.D' or 'F' take a client side function as parameter:
```
div ~a:[a_onclick [%client fun ev -> ... ]] [ ... ]
```

Module 'Lwt_js_events' of 'Js_of_ocaml' defines a way to bind browser events using 'Lwt' promises.<br>
For example, the following code will wait for a click on element 'd' before continuing:
```
let%lwt ev = Lwt_js_events.click (Eliom_content.Html.To_dom.of_element ~%d) in
...
```
Functions like 'Lwt_js_events.clicks' or 'Lwt_js_events.mousedowns' will call the function given as second parameter for each click or mousedown events on their first parameter.

### Ocsigen Toolkit
Ocsigen Toolkit defines several widgets that can be generated either on server or client sides.

For example module 'Ot_spinner' implements a widgets that you can use to display a spinner (or fake elements) when some parts of your page take time to appear.

### Ocsigen Start
Ocsigen-start is a library and a template of Eliom application, with many common features like user registration, login box, notification system, etc.

### Server to client communication
Modules 'Eliom_notif' and 'Os_notif' define the simplest interface to enable server to client communication

### Reactive programming
Eliom allows to insert reactive nodes in pages, that is, nodes which are automatically updated when the values on which they depend change.

Function 'React.S.create' creates a signal and a function to change its value:
```
let%client mysignal, set_mysignal = React.S.create 0
```

Insert a (client side) reactive node in a page using function 'Eliom_content.Html.R.node':
```
let%client f () =
  let open Eliom_content.Html in
  F.div [ R.node s_p ]
```

Module 'Eliom_content.Html.R' also defines all 'TyXML' nodes, which take reactive content as parameter. For example 'Eliom_content.Html.R.txt' takes a value of type 'string React.S.t' as parameter (string signal).

### Ocsigen Server
Ocsigen Server is a full featured Web server.

It has a powerful extension mechanism that makes it easy to plug your own OCaml modules for generating pages.

Ocsigen Server has a [sophisticated configuration](https://ocsigen.org/ocsigenserver/latest/manual/config) file mechanism allowing complex configurations of sites.

## Resources
[Introduction to Objective Caml](http://courses.cms.caltech.edu/cs134/cs134b/book.pdf)<br>
[stackoverflow - understand expression separation](https://stackoverflow.com/questions/75887106/prior-function-definition-makes-let-binding-fail/75887763#75887763)<br>
[All Ocsigen in one page](https://ocsigen.org/tuto/latest/manual/intro)
