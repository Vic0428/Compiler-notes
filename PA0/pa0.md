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

4. Configure environment

   ```ocaml
    eval $(opam config env)
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

### Recursive functions

`Ocaml` distinguishes between functions that can contain `recursive` calls and not. We need to define recursive functions by using `let rec`. 

Calculate the factorial of `n`

```ocaml
let rec factorial(n : int) : int = 
  if n <= 1 then 1
  else n * (factorial (n - 1));;
```

### Testing with OUnit

We will use a library called [OUnit](http://ounit.forge.ocamlcore.org/api-ounit/index.html) to write tests. 

With `OUnit`, we will write declarations in one file, and test them in another. 

- `functions.ml` the declarations of various functions
- `test.ml`  which will contain tests

A test in `OUnit` is a name paired with a function of one argument. And the test predicates most commonly used is `assert_equal`. 

The syntax `>::` is used to combine the name and the function together into a test. 

An example of test file

```ocaml
open OUnit2

let check_fn _ =
  assert_equal (2 + 2) 4;;

let my_first_test = "my_first_test">::check_fn;;

let suite = "suite">:::[my_first_test];;

run_test_tt_main suite
```

To build and run the given skeleton, we can use the Makefile to run the test

`Makefile`

```makefile
test: test.ml
	ocamlfind ocamlc -o test -package oUnit -linkpkg -g test.ml
	./test
```

We need to use `ocamlfind` that knows how to search your system for packages installed with e.g. OPAM. 

Run the test

```shell
$ make test
$ ./test
```

Another example of a failed test

```ocaml
let check_fn2 _ =
  assert_equal (2 + 3) 4;;

let my_second_test = "my_second_test">::check_fn2;;

let suite = "suite">:::[my_second_test];;
```

But however it doesn’t tell us much about the test information, we want more info. Notice that `assert_equal` has an optional argument that specifies how to turn the values under test into a string for printing. 

```ocaml
let t_int name value expected = name>::
  (fun _ -> assert_equal expected value ~printer:string_of_int);;

let my_third_test = t_int "my_third_test" (2 + 2) 7;;
let my_fourth_test = t_int "my_fourth_test" (2 + 2) 4;;

let suite = "suite">:::[
    my_third_test;
    my_fourth_test;
];;
run_test_tt_main suite
```

## Reference

- [UCSD CSE131](https://ucsd-cse131-f19.github.io/pa0/#neonate)

- [Install Opam](https://opam.ocaml.org/doc/Install.html)

  