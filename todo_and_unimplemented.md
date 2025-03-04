# Understanding the `todo!` and `unimplemented!` Macros in Rust

In Rust, both `todo!` and `unimplemented!` are macros used to indicate that certain parts of the code are placeholders and have not yet been implemented. However, there is a subtle difference in their intended use, and understanding these differences is important to choose the right one for your needs.

## The `todo!` Macro

The `todo!` macro is used to mark a place in the code where functionality is yet to be implemented, and the developer intends to complete it later. When invoked, it triggers a panic at runtime, which halts the execution of the program. The `todo!` macro is typically used during the early stages of development, when certain parts of the program are only planned or outlined but not yet written.

### Example:

```rust
fn some_function() {
    // This function is a placeholder for future code
    todo!();
}
```

If `some_function()` is called, the program will panic, and you'll see an error message indicating that the code isn't implemented.

## The `unimplemented!` Macro

The `unimplemented!` macro is also used as a placeholder for code that hasn't been implemented yet. It works similarly to `todo!` by causing the program to panic when invoked. However, the key difference between `todo!` and `unimplemented!` is that `unimplemented!` is generally used in situations where the function or method is expected to be implemented eventually but is not a priority at the moment.

The `unimplemented!` macro is often used in scenarios where the function signature exists, but the actual implementation is missing, and the developer knows it will be implemented in the future.

### Example:

```rust
fn process_data() {
    // Placeholder for data processing logic
    unimplemented!();
}
```

Like `todo!`, calling `process_data()` would cause the program to panic.

## Key Differences Between `todo!` and `unimplemented!`

### 1. **Semantics**

- **`todo!`**: Indicates that the code is a "to-do" item and needs to be implemented later. It is often used in the context of development planning.
- **`unimplemented!`**: Signifies that the code is not implemented yet but is expected to be in the future. It has a more neutral tone compared to `todo!`, which can convey more of a reminder to finish specific tasks.

### 2. **Usage**

- **`todo!`**: Typically used for areas of code that you know are necessary, and you want to specifically mark them for future implementation as part of a larger feature or functionality.
- **`unimplemented!`**: More general in nature, often used when you know the function or method needs to be there but haven’t gotten to it yet or don’t have an exact plan for it.

### 3. **Error Messages**

Both macros will panic, but `todo!` can optionally take a string message that explains the task to be done:

```rust
todo!("Implement the logic for price calculation");
```

`unimplemented!()` does not accept a message and will simply panic with a generic message: _"not yet implemented"_.

### 4. **Philosophical Difference**

- `todo!` feels more like a "work in progress" indicator, something to remind you of the tasks you need to tackle soon.
- `unimplemented!` feels more like an acknowledgment that certain functionality is missing, but not necessarily something that requires immediate attention.

## Example Comparison

```rust
// Using todo!
fn some_feature() {
    // This part of the code still needs to be done
    todo!("Implement user authentication logic");
}

// Using unimplemented!
fn another_feature() {
    // Placeholder for another feature
    unimplemented!();
}
```

In this example, both functions are not implemented, but the `todo!` explicitly suggests that there is a task to finish soon, while `unimplemented!` leaves it more open-ended.

## Conclusion

Both `todo!` and `unimplemented!` serve as useful tools to mark unfinished sections of your code in Rust. The main difference lies in the intention behind their use:

- Use `todo!` when you want to explicitly remind yourself or others of a specific task that still needs to be done.
- Use `unimplemented!` when you're acknowledging that a part of the code is missing, but there's no immediate urgency to complete it.

Both macros trigger panics at runtime if the code is executed, so they should be used during development and replaced with actual implementations before shipping production code.
