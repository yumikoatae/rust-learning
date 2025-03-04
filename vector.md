# Vectors in Rust

A vector in Rust is a growable array, which means that you can dynamically add or remove elements at runtime. It is part of the standard library and is represented by the `Vec<T>` type. Vectors in Rust are commonly used when you need a collection with an unknown or variable number of elements.

## Creating a Vector

You can create a vector in Rust using several methods:

### Using the `vec!` macro

This is the most common way to create a vector. You provide a list of elements, and the macro will create the vector for you.

```rust
let v = vec![1, 2, 3, 4];
```

### Using `Vec::new()` to create an empty vector

This method creates an empty vector that you can add elements to later using the `push` method.

```rust
let mut v: Vec<i32> = Vec::new();
v.push(1);
v.push(2);
```

### Using `vec!` with repeated values

You can create a vector with repeated values using the `vec!` macro.

```rust
let v = vec![0; 5]; // Creates a vector: [0, 0, 0, 0, 0]
```

## Accessing Elements

You can access the elements of a vector using indices or methods like `get`:

### Using indices

You can access elements directly using the index, but this can panic if the index is out of bounds. Indexing starts from `0`.

```rust
let v = vec![1, 2, 3, 4];
println!("{}", v[0]); // Outputs: 1
```

### Using `get()` (Safe access)

The `get` method returns an `Option`, so it’s safe to access elements without causing a panic if the index is invalid.

```rust
let v = vec![1, 2, 3, 4];
match v.get(2) {
    Some(&value) => println!("Value: {}", value),
    None => println!("Index out of bounds"),
}
```

## Modifying Elements

If a vector is mutable, you can modify its elements:

```rust
let mut v = vec![1, 2, 3, 4];
v[0] = 10; // Modify the first element
println!("{:?}", v); // Outputs: [10, 2, 3, 4]
```

## Iterating Over a Vector

You can iterate over the elements of a vector using a `for` loop.

```rust
let v = vec![1, 2, 3, 4];
for val in &v {
    println!("{}", val);
}
```

## Adding and Removing Elements

Rust vectors are dynamically sized, meaning you can add and remove elements at runtime.

### Adding elements with `push`

The `push` method adds an element to the end of the vector.

```rust
let mut v = vec![1, 2, 3];
v.push(4); // Adds the number 4 to the end
```

### Removing elements with `pop`

The `pop` method removes the last element and returns it wrapped in an `Option`.

```rust
let mut v = vec![1, 2, 3];
let last = v.pop(); // Removes the last element (returns an Option)
```

### Removing an element at a specific position

You can remove an element from a specific position using `remove`:

```rust
let mut v = vec![1, 2, 3, 4];
let removed = v.remove(2); // Removes the element at index 2 (value: 3)
println!("Removed: {}", removed);
println!("{:?}", v); // [1, 2, 4]
```

## Capacity and Memory Allocation

A vector has a capacity that is the number of elements it can hold without reallocating. When a vector grows beyond its current capacity, it will allocate more memory.

### Checking capacity

You can check the current capacity of a vector with the `capacity()` method:

```rust
let v = vec![1, 2, 3];
println!("Capacity: {}", v.capacity()); // Returns the current capacity
```

### Reserving space in advance

You can reserve capacity in advance using the `reserve` method, which can be useful to avoid frequent reallocations when you know the number of elements in advance.

```rust
let mut v = Vec::new();
v.reserve(10); // Reserves space for at least 10 elements
```

## Slicing a Vector

You can create a slice of a vector, which is a view into a portion of the vector without owning the data:

```rust
let v = vec![1, 2, 3, 4, 5];
let slice = &v[1..4]; // Slice from index 1 to index 3
println!("{:?}", slice); // [2, 3, 4]
```

## Vector of Vectors

You can also create a vector of vectors, which is useful for representing matrices or other nested data structures:

```rust
let mut matrix: Vec<Vec<i32>> = Vec::new();
matrix.push(vec![1, 2, 3]);
matrix.push(vec![4, 5, 6]);
matrix.push(vec![7, 8, 9]);

// Accessing an element from the matrix
println!("{}", matrix[1][2]); // Outputs: 6
```

## Conclusion

Rust’s vectors are powerful and flexible. They allow you to store and manipulate data in a dynamically-sized collection. You can create, modify, and access vectors easily, and their capacity management ensures that they grow efficiently.
