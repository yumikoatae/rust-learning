# Validate References by Using Lifetimes

## Understanding the Problem

The use of references presents a challenge: the item a reference is pointing to doesn't track all of its references. This can lead to issues when an item is dropped and its resources are freed while references to it still exist, creating potential invalid memory access.

Languages like [C](w) and [C++](w) often encounter a problem called a "dangling pointer," where a pointer refers to a freed item. Rust eliminates this issue by ensuring that all references always point to valid data through the concept of **lifetimes**.

Lifetimes allow Rust to enforce memory safety without the performance overhead of [garbage collection](w).

## Example of an Invalid Reference

Consider this code snippet, which tries to use a reference whose value has gone out of scope:

```rust
fn main() {
    let x;
    {
        let y = 42;
        x = &y; // `x` is a reference to `y`, but `y` is about to be dropped.
    }
    println!("x: {}", x); // `x` refers to `y`, which is no longer valid.
}
```

This will produce a compilation error:

```text
error[E0597]: `y` does not live long enough
 --> src/main.rs:6:17
  |
6 |             x = &y;
  |                 ^^ borrowed value does not live long enough
7 |         }
  |         - `y` dropped here while still borrowed
8 |         println!("x: {}", x);
  |                           - borrow later used here
```

Rust detects that `x` has a longer scope than `y` and prevents the program from compiling.

## Lifetime Annotations

Lifetimes help Rust track references and ensure that a reference never outlives its data.

In this example, `x` has a longer lifetime (`'a`) than `y` (`'b`):

```rust
fn main() {
    let x;                // ---------+-- 'a
    {                     //          |
        let y = 42;       // -+-- 'b  |
        x = &y;           //  |       |
    }                     // -+       |
    println!("x: {}", x); //          |
}
```

Since `'b` ends before `'a`, Rust prevents the program from compiling.

## Annotating Lifetimes in Functions

In Rust, lifetimes can be explicitly annotated to help the compiler determine valid references. Consider this function that returns the longest of two strings:

```rust
fn longest_word<'a>(x: &'a String, y: &'a String) -> &'a String {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

The lifetime `'a` ensures that the returned reference is valid as long as both `x` and `y` are.

### Common Lifetime Issues

Let's examine this example:

```rust
fn main() {
    let magic1 = String::from("abracadabra!");
    let result;
    {
        let magic2 = String::from("shazam!");
        result = longest_word(&magic1, &magic2);
    }
    println!("The longest magic word is {}", result);
}
```

This results in an error:

```text
error[E0597]: `magic2` does not live long enough
 --> src/main.rs:6:40
  |
6 |         result = longest_word(&magic1, &magic2);
  |                                        ^^^^^^^ borrowed value does not live long enough
```

Since `magic2` is dropped after the inner scope, `result` becomes invalid.

## Annotating Lifetimes in Structs

When using references in [structs](w), lifetimes must be explicitly declared:

```rust
#[derive(Debug)]
struct Highlight<'document>(&'document str);

fn main() {
    let text = String::from("The quick brown fox jumps over the lazy dog.");
    let fox = Highlight(&text[4..19]);
    let dog = Highlight(&text[35..43]);
    println!("{:?}", fox);
    println!("{:?}", dog);
}
```

If we move `text` out of scope, Rust prevents its use:

```rust
fn erase(_: String) { }

fn main() {
    let text = String::from("The quick brown fox jumps over the lazy dog.");
    let fox = Highlight(&text[4..19]);
    let dog = Highlight(&text[35..43]);

    erase(text); // `text` is moved here.

    println!("{:?}", fox); // ERROR: `fox` contains a reference to `text`
    println!("{:?}", dog); // ERROR: `dog` contains a reference to `text`
}
```

By enforcing lifetimes, Rust guarantees safe memory access and prevents dangling references.
