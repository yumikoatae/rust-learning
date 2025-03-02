# Sum Function in Rust

## Original Code

Let's begin with the original Rust code:

```rust
fn sum(numbers: &[i32]) -> i32 {
    let mut result = 0;
    for number in numbers {
        result += number;
    }
    result
}

fn main() {
    // Rust does not support variadic arguments
    let numbers = [1, 2, 3, 4, 5];
    let result = sum(&numbers);
    println!("The sum is {}", result);
}
```

## Code Explanation

### 1. `sum` Function

```rust
fn sum(numbers: &[i32]) -> i32 {
    let mut result = 0;
    for number in numbers {
        result += number;
    }
    result
}
```

- **Function Definition:**
  - The `sum` function takes a reference to a slice of integers (`&[i32]`) as input. A slice allows handling a portion of an array or vector.
  - The function returns an `i32`, representing the sum of all elements in the slice.

- **Variable Initialization:**
  - A mutable variable `result` is initialized to `0`, which accumulates the sum.

- **Loop Iteration:**
  - A `for` loop iterates through each number in `numbers`, adding it to `result`.

- **Returning the Result:**
  - After processing all elements, the function returns `result`.

### 2. `main` Function

```rust
fn main() {
    let numbers = [1, 2, 3, 4, 5];
    let result = sum(&numbers);
    println!("The sum is {}", result);
}
```

- **Array Declaration:**
  - The array `numbers` is defined with values `[1, 2, 3, 4, 5]`.

- **Calling `sum`:**
  - The function `sum` is called with a reference to `numbers` (`&numbers`).
  - Using a reference prevents copying the entire array, improving efficiency.

- **Printing the Result:**
  - The computed sum is displayed using `println!`.

#### Expected Output

```plaintext
The sum is 15
```

## Code Reflection

### Why Use Function Arguments?

- **Purpose of Arguments:**
  - Function arguments allow reusability and flexibility by working with different inputs rather than hardcoded values.

- **Code Modularity & Reusability:**
  - Functions improve modularity, enabling reuse across different parts of the program.
  - Any updates to function logic require changes in one place rather than multiple locations.

### What Happens If an Empty Array is Passed?

- If an empty array (`[]`) is passed to `sum`, the `for` loop does not execute.
- `result` remains `0`, which is then returned.

#### Expected Output for an Empty Array

```plaintext
The sum is 0
```

## Challenge 1: Accepting User Input

Now, let's modify the program to accept user input for numbers.

### Modified Code

```rust
use std::io::{self, Write};

fn sum(numbers: &[i32]) -> i32 {
    let mut result = 0;
    for number in numbers {
        result += number;
    }
    result
}

fn main() {
    print!("Enter the number of elements: ");
    io::stdout().flush().unwrap();

    let mut num_elements = String::new();
    io::stdin().read_line(&mut num_elements).unwrap();
    let num_elements: usize = num_elements.trim().parse().unwrap();

    let mut numbers = Vec::new();

    for i in 0..num_elements {
        print!("Enter number {}: ", i + 1);
        io::stdout().flush().unwrap();

        let mut input = String::new();
        io::stdin().read_line(&mut input).unwrap();
        let num: i32 = input.trim().parse().unwrap();
        numbers.push(num);
    }

    let result = sum(&numbers);
    println!("The sum is {}", result);
}
```

### Explanation

- **User Input for Array Size:**
  - The user specifies how many numbers they want to sum.

- **Loop for Collecting Numbers:**
  - A loop prompts the user to input numbers, storing them in a `Vec<i32>`.

- **Computing & Displaying the Sum:**
  - The `sum` function is called, and the result is displayed.

#### Expected Output Example

```plaintext
Enter the number of elements: 3
Enter number 1: 5
Enter number 2: 10
Enter number 3: 15
The sum is 30
```

## Challenge 2: Calculating the Average

Now, let's modify the program to compute the average instead of the sum.

### Modified Code for Average Calculation

```rust
use std::io::{self, Write};

fn average(numbers: &[i32]) -> f32 {
    let sum: i32 = numbers.iter().sum();
    sum as f32 / numbers.len() as f32
}

fn main() {
    print!("Enter the number of elements: ");
    io::stdout().flush().unwrap();

    let mut num_elements = String::new();
    io::stdin().read_line(&mut num_elements).unwrap();
    let num_elements: usize = num_elements.trim().parse().unwrap();

    let mut numbers = Vec::new();

    for i in 0..num_elements {
        print!("Enter number {}: ", i + 1);
        io::stdout().flush().unwrap();

        let mut input = String::new();
        io::stdin().read_line(&mut input).unwrap();
        let num: i32 = input.trim().parse().unwrap();
        numbers.push(num);
    }

    let result = average(&numbers);
    println!("The average is {:.2}", result);
}
```

### Explanation

- **`average` Function:**
  - Uses `.iter().sum()` to sum the numbers.
  - Divides the sum by the length of `numbers` to compute the average.
  - Returns `f32` to allow decimal precision.

- **Displaying the Average:**
  - Uses `{:.2}` for formatting output to two decimal places.

#### Expected Output Example

```plaintext
Enter the number of elements: 3
Enter number 1: 5
Enter number 2: 10
Enter number 3: 15
The average is 10.00
```

## Conclusion

This exercise demonstrated how to:

- Use functions for modular and reusable code.
- Pass arguments to functions to improve flexibility.
- Handle user input dynamically.
- Compute both sums and averages efficiently.

These concepts are fundamental for writing clean, efficient, and maintainable Rust programs.

