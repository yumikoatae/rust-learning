# Use Enum Variants for Compound Data


Enums are types that can be any one of several variants. What Rust calls enums are more commonly known as **algebraic data types**. The important detail is that each enum variant can have data to go along with it.

We use the `enum` keyword to create an **enum type**, which can have any combination of the enum variants. Like structs, enum variants can have **named fields**, but they can also have fields **without names**, or **no fields at all**. Like struct types, enum types are also capitalized.

---

## Define an Enum

In the following example, we define an enum to classify a **web event**. Each variant in the enum is independent and stores different amounts and types of values.

### Rust Code:
```rust
enum WebEvent {
    // An enum variant can be like a unit struct without fields or data types
    WELoad,
    // An enum variant can be like a tuple struct with data types but no named fields
    WEKeys(String, char),
    // An enum variant can be like a classic struct with named fields and their data types
    WEClick { x: i64, y: i64 }
}
```

### Explanation:
- `WELoad` has **no associated data**.
- `WEKeys` has two fields with data types **String** and **char**.
- `WEClick` contains an **anonymous struct** with named fields `x` and `y`, both of type `i64`.

Each variant is part of the `WebEvent` enum type. However, **each variant isn't its own type**. Any function that uses `WebEvent` **must accept all variants**.

---

## Define an Enum with Structs

A way to work around enum variant requirements is to **define a separate struct** for each variant in the enum.

### Rust Code:
```rust
// Define a tuple struct
struct KeyPress(String, char);

// Define a classic struct
struct MouseClick { x: i64, y: i64 }

// Redefine the enum variants to use the data from the new structs
// Update the page Load variant to have the boolean type
enum WebEvent { WELoad(bool), WEClick(MouseClick), WEKeys(KeyPress) }
```

### Benefits:
- **Each variant can be used independently.**
- **Code organization is improved.**
- **More flexibility when dealing with enums.**

---

## Instantiate an Enum

To create instances of our enum variants, we use `let` and the syntax `<enum>::<variant>` with double colons `::`.

### 1. Simple Variant: `WELoad(bool)`
```rust
let we_load = WebEvent::WELoad(true);
```

### 2. Struct Variant: `WEClick(MouseClick)`
```rust
// Instantiate a MouseClick struct and bind the coordinate values
let click = MouseClick { x: 100, y: 250 };

// Set the WEClick variant to use the data in the click struct
let we_click = WebEvent::WEClick(click);
```

### 3. Tuple Variant: `WEKeys(KeyPress)`
```rust
// Instantiate a KeyPress tuple and bind the key values
let keys = KeyPress(String::from("Ctrl+"), 'N');

// Set the WEKeys variant to use the data in the keys tuple
let we_key = WebEvent::WEKeys(keys);
```

**Note:** We use `String::from("<value>")` to create a value of type `String`.

---

## Full Example

```rust
// Define a tuple struct
#[derive(Debug)]
struct KeyPress(String, char);

// Define a classic struct
#[derive(Debug)]
struct MouseClick { x: i64, y: i64 }

// Define the WebEvent enum variants to use the data from the structs
// and a boolean type for the page Load variant
#[derive(Debug)]
enum WebEvent { WELoad(bool), WEClick(MouseClick), WEKeys(KeyPress) }

fn main() {
    // Instantiate a MouseClick struct and bind the coordinate values
    let click = MouseClick { x: 100, y: 250 };
    println!("Mouse click location: {}, {}", click.x, click.y);
        
    // Instantiate a KeyPress tuple and bind the key values
    let keys = KeyPress(String::from("Ctrl+"), 'N');
    println!("\nKeys pressed: {}{}", keys.0, keys.1);
        
    // Instantiate WebEvent enum variants
    let we_load = WebEvent::WELoad(true);
    let we_click = WebEvent::WEClick(click);
    let we_key = WebEvent::WEKeys(keys);
        
    // Print the values in the WebEvent enum variants
    println!("\nWebEvent enum structure: \n\n {:#?} \n\n {:#?} \n\n {:#?}", we_load, we_click, we_key);
}
```

---

## Debug Statements

To print enum data, we use `#[derive(Debug)]`.

```rust
#[derive(Debug)]
```

This allows us to **format debug output** using `{:#?}` inside `println!`:

```rust
println!("{:#?}", we_load);
```

