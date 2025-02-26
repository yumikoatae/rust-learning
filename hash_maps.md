## Working with Hash Maps


### Introduction
A common collection type in Rust is the **hash map**. The `HashMap<K, V>` type stores data by associating each key `K` with its corresponding value `V`. Unlike vectors, where data is accessed via an integer index, a hash map allows access via a unique key.

Hash maps are widely used in programming languages to implement objects, hash tables, and dictionaries.

Similar to vectors, hash maps are dynamically resizable. Their data is stored in the heap, and Rust enforces runtime safety checks when accessing hash map items.

### Defining a Hash Map
The following example demonstrates how to define a hash map for tracking book reviews. The keys represent book titles, while the values contain reader reviews.

```rust
use std::collections::HashMap;

let mut reviews: HashMap<String, String> = HashMap::new();

reviews.insert(String::from("Ancient Roman History"), String::from("Very accurate."));
reviews.insert(String::from("Cooking with Rhubarb"), String::from("Sweet recipes."));
reviews.insert(String::from("Programming in Rust"), String::from("Great examples."));
```

Let's analyze the key aspects of this code:

- The `use` statement imports `HashMap` from Rust’s standard library.
- The `HashMap::new()` method initializes an empty hash map.
- The `mut` keyword makes the `reviews` variable mutable, allowing modifications.
- Both keys and values are stored as `String` types.

### Adding Key-Value Pairs
Elements can be added to a hash map using the `.insert(<key>, <value>)` method:

```rust
reviews.insert(String::from("Ancient Roman History"), String::from("Very accurate."));
```

### Retrieving a Value by Key
Once data is inserted, we can retrieve a value using the `.get(<key>)` method:

```rust
// Retrieve a specific review
let book: &str = "Programming in Rust";
println!("\nReview for '{}': {:?}", book, reviews.get(book));
```

#### Expected Output:
```rust
Review for 'Programming in Rust': Some("Great examples.")
```

**Note:** The output includes `Some("Great examples.")` rather than just `"Great examples."` because `.get()` returns an `Option<&Value>`, meaning Rust wraps the value inside a `Some()` variant.

### Removing a Key-Value Pair
Entries can be deleted using the `.remove(<key>)` method. If we attempt to access a removed key, `.get()` will return `None`.

```rust
// Remove a book review
let obsolete: &str = "Ancient Roman History";
println!("\n'{}' removed.", obsolete);
reviews.remove(obsolete);

// Verify removal
println!("\nReview for '{}': {:?}", obsolete, reviews.get(obsolete));
```

#### Expected Output:
```rust
'Ancient Roman History' removed.
Review for 'Ancient Roman History': None
