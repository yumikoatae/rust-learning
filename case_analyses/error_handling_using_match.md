# **Case Study: Error Handling in Rust Using `match`**

### Original Code
```rust
use std::fs::File;
use std::io::{BufRead, BufReader};

fn main() {
    let file = File::open("non_existent_file.txt");
    let file = match file {
        Ok(file) => file,
        Err(error) => {
            match error.kind() {
                std::io::ErrorKind::NotFound => {
                    panic!("File not found: {}", error)
                }
                _ => {
                    panic!("Error opening file: {}", error)
                }
            }
        }
    };
    
    let reader = BufReader::new(file);
    for line in reader.lines() {
        match line {
            Ok(line) => println!("{}", line),
            Err(error) => {
                panic!("Error reading line: {}", error)
            }
        }
    }
}
```

### Analysis of the Original Code
The provided Rust program attempts to open a file named `non_existent_file.txt` and read its contents line by line. It employs Rust's error handling mechanisms to manage potential failures. The `match` construct is used to handle errors that may occur when opening the file and reading its contents.

#### Key Features:
1. **Opening the File:**
   - The program uses `File::open("non_existent_file.txt")`, which returns a `Result<File, std::io::Error>`.
   - The `match` construct evaluates this result:
     - If successful (`Ok(file)`), it assigns the file to the variable.
     - If an error occurs (`Err(error)`), it checks the error type.
     - If the error is `NotFound`, it panics with a specific message.
     - For any other error, it panics with a generic message.

2. **Reading the File:**
   - A `BufReader` is used to read lines from the file.
   - Each line is checked using `match`:
     - If successful, the line is printed.
     - If an error occurs, the program panics with an error message.

### Reflection Questions
#### How does the `match` construct help in error handling? What advantages does it offer over other error handling mechanisms?
The `match` construct provides structured and explicit error handling by forcing the developer to handle all possible cases of a `Result` or `Option` type. It ensures that errors are not ignored and provides a clear way to deal with different error scenarios. Compared to traditional error-handling methods such as exceptions in other languages, `match`:
- **Makes error handling explicit**: The compiler enforces handling all possible cases, reducing the chances of unhandled errors.
- **Encourages detailed error responses**: Different error types can be handled uniquely, leading to more robust code.
- **Avoids unwarranted panic**: Instead of crashing unexpectedly, errors can be managed gracefully.

#### In the provided code, what would happen if the file "non_existent_file.txt" existed? How would the program output change?
If the file existed and was readable, the program would:
1. Successfully open the file.
2. Read its contents line by line.
3. Print each line to the console.

There would be no panics, and the program would execute normally.

### Challenge Questions
#### Handling a Permission Error
Modify the program to specifically handle permission errors when opening the file:

```rust
use std::fs::File;
use std::io::{self, BufRead, BufReader};

fn main() {
    let file = File::open("non_existent_file.txt");
    let file = match file {
        Ok(file) => file,
        Err(error) => {
            match error.kind() {
                std::io::ErrorKind::NotFound => {
                    panic!("File not found: {}", error);
                }
                std::io::ErrorKind::PermissionDenied => {
                    panic!("Permission denied: {}", error);
                }
                _ => {
                    panic!("Error opening file: {}", error);
                }
            }
        }
    };
    
    let reader = BufReader::new(file);
    for line in reader.lines() {
        match line {
            Ok(line) => println!("{}", line),
            Err(error) => panic!("Error reading line: {}", error),
        }
    }
}
```

This modification adds a specific error case for `PermissionDenied`, making the error handling more comprehensive.

#### Implementing a File Writing Function
We can extend the program by adding a function to write to a file and handle potential errors:

```rust
use std::fs::OpenOptions;
use std::io::{self, Write};

fn write_to_file(filename: &str, content: &str) {
    let file = OpenOptions::new().write(true).create(true).open(filename);
    match file {
        Ok(mut file) => {
            match file.write_all(content.as_bytes()) {
                Ok(_) => println!("Successfully wrote to file."),
                Err(error) => println!("Error writing to file: {}", error),
            }
        }
        Err(error) => {
            match error.kind() {
                std::io::ErrorKind::PermissionDenied => {
                    println!("Permission denied: {}", error);
                }
                _ => println!("Error opening file: {}", error),
            }
        }
    }
}

fn main() {
    write_to_file("output.txt", "Hello, Rust!");
}
```

### Conclusion
This case study explores error handling in Rust using the `match` construct. By handling specific errors such as file not found and permission denied, the program becomes more robust and user-friendly. Additionally, extending the program to write to a file demonstrates how error handling applies to different operations, reinforcing the importance of structured error management in Rust.
