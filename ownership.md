# What is Ownership?

Rust includes an ownership system to manage memory. At compile time, the ownership system checks a set of rules to ensure that ownership features allow your program to run without slowing down.

To understand ownership, let's first take a look at Rust's scoping rules and move semantics.

## Scoping Rules

In Rust, like most other programming languages, variables are only valid within a certain scope. In Rust, scopes are often denoted by using curly brackets `{}`. Common scopes include function bodies and `if`, `else`, and `match` branches.

> **Note:**  
> In Rust, "variables" are often called "bindings." This is because "variables" in Rust aren't very variable—they don't change often since they're immutable by default. Instead, we often think of names being "bound" to data, hence the name "binding." In this module, we'll use the terms "variable" and "binding" interchangeably.

Let's say we have a `mascot` variable, which is a string, defined within a scope:

```rust
// `mascot` is not valid and cannot be used here, because it's not yet declared.
{
    let mascot = String::from("ferris");   // `mascot` is valid from this point forward.
    // do stuff with `mascot`.
}
// this scope is now over, so `mascot` is no longer valid and cannot be used.
```

If we try to use `mascot` beyond its scope, we get an error:

```rust
{
    let mascot = String::from("ferris");
}
println!("{}", mascot);
```

### Output

```bash
error[E0425]: cannot find value `mascot` in this scope
 --> src/main.rs:5:20
  |
5 |     println!("{}", mascot);
  |                    ^^^^^^ not found in this scope
```

The variable is valid from the point it's declared until the end of that scope.

## Ownership and Dropping

Rust adds a twist to the idea of scopes. Whenever an object goes out of scope, it's "dropped." Dropping a variable releases any resources tied to it. For variables like files, the file is closed. For variables with allocated memory, the memory is freed.

In Rust, bindings that have things "associated" with them that they will free when dropped are said to "own" those things.

In the previous example, the `mascot` variable owns the `String` data associated with it. The `String` itself owns the heap-allocated memory that holds the characters of that string. At the end of the scope, the `mascot` variable is "dropped," the `String` it owns is dropped, and finally, the memory that the `String` owns is freed.

```rust
{
    let mascot = String::from("ferris");
} // mascot is dropped here. The string data memory will be freed here.
```

## Move Semantics

Sometimes, however, we don't want the things associated with a variable to be dropped at the end of the scope. Instead, we want to transfer ownership of an item from one binding to another.

The simplest example of this is when declaring a new binding:

```rust
{
    let mascot = String::from("ferris");
    // transfer ownership of mascot to the variable ferris.
    let ferris = mascot;
} // ferris is dropped here. The string data memory will be freed here.
```

A key thing to understand is that once ownership is transferred, the old variable is no longer valid. If we try to use `mascot` after the `String` has been moved from `mascot` to `ferris`, the compiler won't compile our code:

```rust
{
    let mascot = String::from("ferris");
    let ferris = mascot;
    println!("{}", mascot); // Error: use after move
}
```

### Output

```bash
error[E0382]: borrow of moved value: `mascot`
 --> src/main.rs:4:20
  |
2 |     let mascot = String::from("ferris");
  |         ------ move occurs because `mascot` has type `String`, which does not implement the `Copy` trait
3 |     let ferris = mascot;
  |                  ------ value moved here
4 |     println!("{}", mascot);
  |                    ^^^^^^ value borrowed here after move
```

This result is known as a "use after move" compile error.

### Important

In Rust, only one thing can ever own a piece of data at a time.

## Ownership in Functions

Let's look at an example of a string being passed to a function as an argument. Passing something as an argument to a function moves that thing into the function.

```rust
fn process(input: String) {}

fn caller() {
    let s = String::from("Hello, world!");
    process(s); // Ownership of the string in `s` moved into `process`
    process(s); // Error! ownership already moved.
}
```

### Output

```bash
error[E0382]: use of moved value: `s`
 --> src/main.rs:6:13
  |
4 |     let s = String::from("Hello, world!");
  |         - move occurs because `s` has type `String`, which does not implement the `Copy` trait
5 |     process(s); // Transfers ownership of `s` to `process`
  |             - value moved here
6 |     process(s); // Error! ownership already transferred.
  |             ^ value used here after move
```

## Copying Instead of Moving

In the previous example, you might have noticed the mention of the `Copy` trait in the compiler error messages. A value that implements the `Copy` trait isn't moved, but instead copied.

Let's look at a value that implements the `Copy` trait: `u32`. The following code mirrors our broken code, but it compiles without issue.

```rust
fn process(input: u32) {}

fn caller() {
    let n = 1u32;
    process(n); // Ownership of the number in `n` copied into `process`
    process(n); // `n` can be used again because it wasn't moved, it was copied.
}
```

## Copying Types That Don’t Implement `Copy`

One way to work around the errors we saw in the previous example is by explicitly copying types before they're moved: known as cloning in Rust. A call to `.clone()` duplicates the memory and produces a new value. The new value is moved, meaning the old value can still be used.

```rust
fn process(s: String) {}

fn main() {
    let s = String::from("Hello, world!");
    process(s.clone()); // Passing another value, cloned from `s`.
    process(s); // `s` was never moved, so it can still be used.
}
```

This approach can be useful, but it can make your code slower, as every call to `clone` makes a full copy of the data. This method often includes memory allocations or other expensive operations. We can avoid these costs if we "borrow" values by using references.
