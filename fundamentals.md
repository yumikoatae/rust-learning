# Essential Rust Keywords and Concepts

Rust is a systems programming language with several essential components and keywords that help structure and optimize code execution. Let's explore some of these: `use`, `main`, `pub`, `fn`, variable assignment, immutability, basic control flow, and shadowing.

## Variable Assignment and Immutability

In Rust, variables are immutable by default. This means that once a variable is assigned a value, it cannot be modified. To make a variable mutable, you need to use the `mut` keyword.

### Immutable Variables (Default)
By default, variables in Rust are immutable. If you try to modify their values after assignment, the compiler will generate an error.

```rust
fn main() {
    let x = 5;  // Immutable variable
    println!("x = {}", x);
    // x = 10;  // Error! Cannot reassign an immutable variable
}
```
Here, `x` is immutable, and reassigning it would result in an error. This feature helps prevent unintended changes to variable values, promoting safer code.

### Mutable Variables
To allow a variable's value to change after assignment, declare it as mutable using the `mut` keyword.

```rust
fn main() {
    let mut y = 10;  // Mutable variable
    println!("y = {}", y);
    
    y = 20;  // Allowed because `y` is mutable
    println!("y after modification = {}", y);
}
```
Here, `y` is mutable, so we can modify its value during program execution.

## `use`

The `use` keyword is used to import modules, libraries, or items from other modules, making them accessible in the current scope. Without `use`, you would need to reference the full path to access a function or structure.

```rust
mod util {
    pub fn greeting() {
        println!("Hello, Rust!");
    }
}

use util::greeting;

fn main() {
    greeting();  // Calling the function directly
}
```
Here, `use` brings `greeting` from the `util` module into the `main` scope, allowing us to call it without prefixing it with `util::`.

## `main`

The `main` function is the entry point of any Rust program. When the program runs, `main` is executed. It is mandatory in executable Rust programs.

```rust
fn main() {
    println!("This is the program entry point.");
}
```
A `main` function can also return a `Result` to handle errors:

```rust
fn main() -> Result<(), String> {
    println!("Program start");

    let success = false;
    
    if !success {
        return Err("Something went wrong!".to_string());
    }
    
    Ok(())
}
```

## `pub`

The `pub` keyword makes functions, structures, or modules accessible outside their defining module. By default, everything in Rust is private.

```rust
mod my_module {
    pub fn public_function() {
        println!("This function is public!");
    }

    fn private_function() {
        println!("This function is private.");
    }
}

fn main() {
    my_module::public_function(); // Allowed
    // my_module::private_function(); // Error! Cannot call a private function
}
```
Here, `public_function` is public and can be accessed outside `my_module`, whereas `private_function` is private.

## `fn`

Functions in Rust are defined using the `fn` keyword. Functions can take parameters and return values.

```rust
fn greeting() {
    println!("Hello, World!");
}

fn main() {
    greeting();
}
```
### Functions with Parameters

```rust
fn greeting(name: &str) {
    println!("Hello, {}!", name);
}

fn main() {
    greeting("Maria");
}
```
### Functions Returning Values

```rust
fn add(a: i32, b: i32) -> i32 {
    a + b
}

fn main() {
    let result = add(5, 10);
    println!("Sum is: {}", result);
}
```
Functions can also return complex types, such as tuples:

```rust
fn division(a: i32, b: i32) -> (i32, i32) {
    let quotient = a / b;
    let remainder = a % b;
    (quotient, remainder)
}

fn main() {
    let (quotient, remainder) = division(10, 3);
    println!("Quotient: {}, Remainder: {}", quotient, remainder);
}
```
Rust also supports anonymous functions (closures):

```rust
fn main() {
    let sum = |a, b| a + b;
    println!("Sum result: {}", sum(3, 4));
}
```

## Basic Control Flow

### Conditional Statements (`if`, `else`)

```rust
fn main() {
    let x = 10;
    
    if x > 5 {
        println!("x is greater than 5");
    } else {
        println!("x is less than or equal to 5");
    }
}
```

### Loops (`loop`, `while`, `for`)

#### `loop` (Infinite Loop with Exit Condition)

```rust
fn main() {
    let mut counter = 0;
    
    loop {
        counter += 1;
        println!("Counter: {}", counter);
        
        if counter == 5 {
            break;
        }
    }
}
```

#### `while` Loop

```rust
fn main() {
    let mut counter = 0;
    
    while counter < 5 {
        println!("Counter: {}", counter);
        counter += 1;
    }
}
```

#### `for` Loop

```rust
fn main() {
    for i in 0..5 {
        println!("i = {}", i);
    }
}
```

## Shadowing

Shadowing allows re-declaring a variable with the same name, "overriding" the previous one. The original variable is no longer accessible after shadowing.

```rust
fn main() {
    let x = 5;
    println!("x = {}", x);
    
    let x = x + 1; // Shadowing creates a new variable
    println!("New x = {}", x);
}
```

Shadowing also allows type changes:

```rust
fn main() {
    let x = 5;
    println!("x = {}", x);
    
    let x = "Now I'm a string!";
    println!("x now = {}", x);
}
```

Shadowing offers flexibility by reusing variable names without requiring explicit mutability.

---

These fundamental Rust keywords and concepts form the building blocks for writing safe and efficient programs.

