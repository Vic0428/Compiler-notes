# PA0 – OCaml and Compiler Warmup

## Setup

1. Install `opam`  ([OPAM](https://opam.ocaml.org/) is a package manager for OCaml)

   ```c++
   brew install gpatch opam
   ```

2. Initialize `opam` (May need clever trick in China)

   ```
   opam init
   ```

3. Install some other packages after setting up OCaml and OPAM

   ```ocaml
   opam install extlib ounit ocamlfind
   ```

## Basic Programming in OCaml

`OCaml` files are written with `.ml` extension. (Similar to `Python`, since it will evaluate the file directly when running)

An `OCaml` file consists of 

- (Optionally) a series of `open` statements for including other modules
- A series of declarations for defining datatypes, functions and constants
- A series of (though often just one) top-level expressions to evaluate

### Hello world in OCaml

`hello.ml`

```ocaml
open Printf

let message = "Hello world";;
(printf "%s\n" message)
```

- The first line includes the built-in library for printing
- The next two lines define the message and print the message

Run the file with `ocaml`

```
ocaml hello.ml
```

### Define and calling functions

Define a `max` function

```ocaml
let max (n : int) (m : int) : int = 
  if n > m then n else m;;
```

In `C++` declaration

```c++
int max(int n, int m) {
	if (n > m) {return n;}
	else {return m;}
}
```

Difference

- `OCaml` have no `return` statement
- The declaration of `OCaml` end in `;;`
- The rule of single semicolon `;` is that they are evaluated in order, and the value resulting from each expression is ignored once it is done. 

The syntax of function call

- In `C++` => `max(4, 5)`
- In `OCaml` => `(max 4 5)`

`(max 4 5)` we can think it will be substituted by `if ` expressions

```
		(max 4 5)
=>	if 4 > 5 then 4 else 5
=>	5
```



## Reference

- [UCSD CSE131](https://ucsd-cse131-f19.github.io/pa0/#neonate)

- [Install Opam](https://opam.ocaml.org/doc/Install.html)
- 