# Rust `for` Loop Examples

In this example, we demonstrate several ways to use the `for` loop in Rust, including:

- Iterating over a simple range.
- Using the `rev()` method to reverse the iteration order.
- Working with inclusive and exclusive ranges.
- Iterating over a vector.
- Using the `continue` and `break` statements to control loop flow.

### Basic `for` Loop (0..5)

```rust
fn main() {
    for i in 0..5 {
        println!("i = {}", i);
    }
}
```

This `for` loop iterates over a range from `0` to `4` (excluding `5`) and prints the value of `i` in each iteration. The range `0..5` is exclusive of the upper bound (`5`), meaning it will only go through the values `0, 1, 2, 3, 4`.

### Reversed Iteration Using `rev()`

```rust
fn main() {
    for i in (0..5).rev() {
        println!("i = {}", i);
    }
}
```

Here, the `.rev()` method is used to reverse the iteration order. The range `0..5` is reversed to iterate from `4` to `0`. This can be useful when you need to process a sequence in reverse order.

### Inclusive Range (1..=10)

```rust
fn main() {
    for i in 1..=10 {
        println!("i = {}", i);
    }
}
```

The range `1..=10` is inclusive, meaning it includes both `1` and `10`. The loop will iterate through the values `1, 2, 3, ..., 10`, printing each value of `i`.

### Exclusive Range (1..10)

```rust
fn main() {
    for i in 1..10 {
        println!("i = {}", i);
    }
}
```

The range `1..10` is exclusive of the upper bound (`10`), meaning the loop will iterate over the values `1, 2, 3, ..., 9`, but not `10`. The upper limit is excluded from the iteration.

### Iterating Over a Vector

```rust
fn main() {
    let vetor = vec![10, 20, 30, 40, 50];
    for &item in &vetor {
        println!("item = {}", item);
    }
}
```

In this example, a vector `vetor` is created, and we iterate over its elements using a `for` loop. Notice the use of `&vetor` to borrow the vector by reference, and `&item` to dereference each element for printing. This is a common pattern when working with collections in Rust.

### Using `continue` and `break` in Loops

In Rust, you can control the flow of a loop using the `continue` and `break` statements:

#### `continue` Statement

The `continue` statement allows you to skip the current iteration of the loop and proceed to the next one.

```rust
fn main() {
    for i in 0..5 {
        if i == 2 {
            continue; // Skips when i is 2
        }
        println!("i = {}", i);
    }
}
```

In this example, when `i` is equal to `2`, the `continue` statement is triggered. This causes the loop to skip the print statement and move to the next iteration, effectively skipping `i = 2`.

#### `break` Statement

The `break` statement allows you to exit the loop entirely, regardless of whether the loop has finished iterating or not.

```rust
fn main() {
    for i in 0..5 {
        if i == 3 {
            break; // Exits the loop when i is 3
        }
        println!("i = {}", i);
    }
}
```

Here, when `i` is equal to `3`, the `break` statement is triggered, causing the loop to terminate immediately. The output will be `i = 0`, `i = 1`, and `i = 2`, and then the loop exits when `i` reaches `3`.

### Summary

- **Basic `for` Loop**: Iterates over a range of numbers.
- **Reversed Iteration**: Uses `.rev()` to reverse the iteration order.
- **Inclusive Range**: The `1..=10` syntax includes the upper bound (`10`).
- **Exclusive Range**: The `1..10` syntax excludes the upper bound (`10`).
- **Vector Iteration**: Iterates over the elements of a vector.
- **`continue` Statement**: Skips the current iteration and continues with the next one.
- **`break` Statement**: Exits the loop prematurely.
