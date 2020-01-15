# Discussion 0: Programming in OCaml

## Details of `Max`

Compare the `Max` function signature in `C++/JAVA` or `Ocaml`

```ocaml
int max(int m, int n);	// C++/JAVA

let max (m : int) (n : int) : int = (* OCaml *)
```

## Define Datatypes for Expressions

In `JAVA` we need to define a common interface `Expr`, and we can define other classes that implement `IntNode` and `ExprNode`. 

```java
interface Expr {....}
class IntNode implements Expr{...}
class ExprNode implements Expr{...}
```

In `OCaml`, we can define expression datatype as `expr` 

```ocaml
type expr =
  | IntNode of int
  | ExprNode of string * expr * expr
```

It defines the type `expr` and two constructors or variants, which are `IntNode` and `ExprNode` . Since there are no names, motivating using `match` to access the pieces. 

```ocaml
let e1 = ExprNode("+", IntNode(1), IntNode(2))
```

```ocaml
let rec eval (e : expr) : int =
  match e with
    | IntNode(value) -> value
    | ExprNode("+", lhs, rhs) -> (eval lhs) + (eval rhs)
    | ExprNode("-", lhs, rhs) -> (eval lhs) - (eval rhs)
    | ExprNode(_, lhs, rhs) -> failwith "Unknown operator"
```

## Difference Between `=` and `==`

`=` is *structural equality*, which is more like `.equals()` in `Java`

`==` is *pointer* or *reference equality*, when `match` matches on a particular value, it uses `=`.  