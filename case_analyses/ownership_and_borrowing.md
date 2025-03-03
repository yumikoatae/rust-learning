# Case Study on Ownership and Borrowing in Rust

## **1. Analysis of the Original Code**

### **Original Code**
```rust
fn own_vec(mut vector: Vec<i32>) {
    vector.push(10);
    println!("{:?}", vector);
}

fn own_integer(x: i32) {
    x + 1;
}

fn own_string(s: String) {
    println!("{}", s);
}

fn main() {
    let mut my_vec = vec![1, 2, 3, 4, 5];
    let my_int = 10;
    let my_string = String::from("Hello, world!");

    own_integer(my_int);
    println!("{}", my_int);

    own_string(my_string);
    // println!("{:?}", my_string); // This will not compile!

    own_vec(my_vec);
    // println!("{:?}", my_vec); // This will not compile!
}
```

### **Code Issues and Observations**

1. **Ownership Transfer:**
   - `own_string(my_string);` moves ownership of `my_string`, making it inaccessible after the function call.
   - `own_vec(my_vec);` moves ownership of `my_vec`, causing a compilation error when trying to access it later.

2. **Copy vs Move Semantics:**
   - `i32` implements `Copy`, so `my_int` remains accessible after passing it to `own_integer(x: i32)`.
   - `String` and `Vec<i32>` do not implement `Copy`, causing ownership transfer and invalidation in `main`.

---

## **2. Reflection Questions**

### **What is the difference between owning a variable and borrowing a variable in Rust? Why is borrowing important for writing safe and efficient code?**

In Rust, ownership determines which part of the code is responsible for a variable's memory allocation and deallocation. When a variable is passed to a function that takes ownership, the original owner loses access to it, and the function becomes the new owner. Borrowing, on the other hand, allows a function to access a variable without transferring ownership. This is done using references (`&` for immutable borrowing and `&mut` for mutable borrowing).

Borrowing is essential for writing safe and efficient code because:
- It prevents unnecessary memory allocations and deallocations.
- It ensures that only one mutable reference exists at a time, preventing data races.
- It allows multiple immutable references to coexist safely.

### **What happens to `my_int`, `my_string`, and `my_vec` when passed to their respective functions?**

- **`my_int`**: Since `i32` implements the `Copy` trait, when `my_int` is passed to `own_integer(x: i32)`, Rust creates a copy of `my_int`. This allows the original `my_int` to still be accessible in `main` after the function call.
- **`my_string`**: `String` does not implement `Copy`, so when it is passed to `own_string(s: String)`, its ownership moves to the function. This makes `my_string` inaccessible in `main` after the function call, preventing further usage.
- **`my_vec`**: `Vec<i32>` also does not implement `Copy`, so when it is passed to `own_vec(mut vector: Vec<i32>)`, ownership moves to the function. As a result, `my_vec` is no longer accessible in `main` after the function call.

---

## **3. Challenge Questions**

### **1. Modify the code to create a function named `borrow_vec` that borrows the `my_vec` variable instead of taking ownership. Inside the function, print the vector without modifying it. Call this function from the `main` function.**

```rust
fn borrow_vec(vector: &Vec<i32>) {
    println!("{:?}", vector);
}

fn main() {
    let my_vec = vec![1, 2, 3, 4, 5];
    borrow_vec(&my_vec);
    println!("{:?}", my_vec); // my_vec is still accessible
}
```

### **Explanation:**
- The `borrow_vec` function takes `vector` as an immutable reference (`&Vec<i32>`), meaning it can read `vector` but cannot modify it.
- The `&my_vec` in `main` ensures that ownership is not transferred, allowing `my_vec` to still be used after the function call.

---

### **2. Extend the code by creating a function named `borrow_string` that borrows the `my_string` variable and appends some text to it without taking ownership. Print the modified string inside the function and then print it again in the `main` function to observe the changes.**

```rust
fn borrow_string(s: &mut String) {
    s.push_str(" How are you?");
    println!("Inside function: {}", s);
}

fn main() {
    let mut my_string = String::from("Hello, world!");
    borrow_string(&mut my_string);
    println!("After function call: {}", my_string);
}
```

### **Explanation:**
- The `borrow_string` function takes a mutable reference (`&mut String`), allowing it to modify the original `my_string`.
- The `&mut my_string` in `main` ensures that ownership is not transferred, only borrowed temporarily.
- The modification persists after the function call because it was done through a mutable reference.

---

## **4. Conclusion**

Understanding ownership and borrowing is crucial for writing efficient and safe Rust programs. By distinguishing between ownership transfers and borrowing mechanisms, we can control memory usage effectively while maintaining data integrity. 

This case study demonstrates how to use references to avoid ownership issues and optimize function calls in Rust.

