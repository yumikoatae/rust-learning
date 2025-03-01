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
<br>

## A unit function and return value
```rust
// a unit function that doesn't return anything
fn print_sum(numbers: &[i32]) {
    let sum = numbers.iter().sum(); // Calculate the sum of elements in slice
    if sum % 2 == 0 {               // Check if sum is even
        println!("The sum is even.");
    } else {
        println!("The sum is odd.");
    }
}

fn main() {
    let numbers = [1, 2, 3];      // Define a slice of integers
    print_sum(&numbers);          // Call the unit function with the slice as an argument
}
```

## Using panic
```rust
fn process_numbers(slice: &[i32]) {
    for (index, number) in slice.iter().enumerate() {
        if *number < 0 {
            panic!("Negative number found at index {}", index); // Stop execution and show error message
        }
    }
}

fn main() {
    let numbers = [1, 2, 3, -5];   // Include a negative number to trigger the panic
    process_numbers(&numbers);     // Call function with slice of integers as an argument
}
```
