## Rust Simple Example

```rust
// Demonstrating 'Rust': Basic program structure and comments
fn main() {
    // Printing greeting message
    println!("Hello, world!");
}
```

<br>

## Cargo.toml example
 A configuration file read by Cargo, listing metadata (e.g., name, version) and dependencies required by the package.
```rust
[package]
name = "example_project"
version = "0.1.0"
authors = ["Your Name <your@email.com>"]
edition = "2018"

[dependencies]
rand = "0.8.5" # Add random library dependency
```
<br>

## Shadowing
Reassigning a variable to a new value while preserving its original binding, enabling changes to its type or scope.

```rust
fn main() {
    // Original integer variable declaration
    let x = 42;
    println!("x: {}", x);
    
    // Variable reassignment (shadowing) within the same scope
    let x = "forty-two";
    println!("x: {}", x);
    
    {
        // Creating a nested scope where 'x' has a new binding
        let x = 42.5;
        println!("x: {}", x);
        
        // Leaving the inner scope - original bindings restored
    }
}
```
<br>

## Handle optional values

```rust
let maybe_number = Some(42); // or None in some cases
if let Some(num) = maybe_number {
    println!("The number is {}", num);
} else {
    println!("No number provided.");
}
```
<br>

## If / Else
```rust
let number = 7;
if number % 2 == 0 {
    println!("The number is even");
} else {
    println!("The number is odd");
}
```

<br>

## While loop
```rust
let mut x = 0;
while x < 5 {
    println!("{}", x);
    if x == 3 { continue } // skipping iteration when x is equal to 3.
    x += 1;
}
```
