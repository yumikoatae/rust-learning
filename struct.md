# Structs in Rust

In Rust, structs are a way to define custom data types that can group multiple values into a single unit. Each value in a struct is called a field, and the fields can have different types. Structs allow you to create more complex and structured data, and they are fundamental when working with Rust.

## Defining a Struct

To define a struct, you use the `struct` keyword, followed by the name of the struct and its fields.

```rust
struct Point {
    x: i32,
    y: i32,
}
```

In this example, `Point` is a struct with two fields: `x` and `y`, both of type `i32`.

## Creating an Instance of a Struct

Once you've defined a struct, you can create instances of that struct using the struct's name and providing values for each field.

```rust
let point1 = Point {
    x: 10,
    y: 20,
};
```

This creates an instance `point1` of the struct `Point`, where `x` is `10` and `y` is `20`.

## Accessing Struct Fields

You can access the fields of a struct using dot notation:

```rust
println!("x: {}, y: {}", point1.x, point1.y);
```

This will print:

```yaml
x: 10, y: 20
```

## Updating Fields of a Struct

If the struct instance is mutable, you can update its fields:

```rust
let mut point1 = Point {
    x: 10,
    y: 20,
};
point1.x = 30;
println!("Updated point: x = {}, y = {}", point1.x, point1.y);
```

This will update the `x` field to `30` and print:

```yaml
Updated point: x = 30, y = 20
```

## Tuple Structs

In addition to the regular structs (named field structs), Rust also allows tuple structs, which are like tuples but with a custom name. These structs don’t require field names; instead, you access the values by position.

```rust
struct Color(i32, i32, i32);

let black = Color(0, 0, 0);
println!("Black color: ({}, {}, {})", black.0, black.1, black.2);
```

Here, `Color` is a tuple struct, and we access the fields using positional indexing (`black.0`, `black.1`, etc.).

## Unit-Like Structs

Rust also supports unit-like structs, which are structs that don’t have any fields. They are mainly used for types that do not store data but still want to have a name and potentially implement methods.

```rust
struct Unit;

let unit = Unit;  // No fields
```

These structs can be useful when implementing traits or using enums.

## Methods on Structs

You can define methods on structs, which are functions that are associated with the struct. To define a method, you need to implement the `impl` block for the struct.

```rust
impl Point {
    fn new(x: i32, y: i32) -> Point {
        Point { x, y }
    }

    fn distance_from_origin(&self) -> f64 {
        ((self.x.pow(2) + self.y.pow(2)) as f64).sqrt()
    }
}

let p = Point::new(3, 4);
println!("Distance from origin: {}", p.distance_from_origin());
```

In this example:
- We define a method `new` that constructs a `Point` with the given `x` and `y` values.
- We also define a method `distance_from_origin`, which calculates the distance from the origin `(0, 0)`.

## Using Structs with `&self` and `self`

- `&self` is used when you want to borrow the struct immutably (no modification).
- `self` is used when the method takes ownership of the struct, which is common when working with `self` inside a constructor or when you want to move the struct out of the function.

```rust
impl Point {
    fn move_point(self, x_offset: i32, y_offset: i32) -> Point {
        Point {
            x: self.x + x_offset,
            y: self.y + y_offset,
        }
    }
}

let p = Point { x: 5, y: 10 };
let p_moved = p.move_point(10, 15); // Ownership of `p` is moved
println!("Moved Point: x = {}, y = {}", p_moved.x, p_moved.y);
```

## Structs with Default Values (`Default` Trait)

You can implement the `Default` trait for your struct, which allows you to create a default value for it. This is useful when you want to create an instance with default values for the fields.

```rust
#[derive(Default)]
struct Point {
    x: i32,
    y: i32,
}

let p: Point = Default::default();  // Creates `Point { x: 0, y: 0 }`
```

Alternatively, you can implement `Default` manually:

```rust
impl Default for Point {
    fn default() -> Self {
        Point { x: 0, y: 0 }
    }
}
```

## Structs in Enums

You can also use structs in enums to store different types of data in each variant. This is commonly used when creating more complex data types like state machines or heterogeneous data containers.

```rust
enum Shape {
    Circle(f64),           // Holds the radius
    Rectangle(f64, f64),   // Holds the width and height
}

let circle = Shape::Circle(5.0);
let rect = Shape::Rectangle(4.0, 6.0);
```

In this example, `Shape` is an enum with two variants, each holding different data.

## Structs in Memory

Structs in Rust are stored in memory contiguously. This means that all the fields of a struct are placed next to each other in memory. However, depending on the types, Rust may insert padding between fields to align them to optimal memory boundaries.

You can use the `#[repr(C)]` attribute to control the memory layout and prevent the compiler from adding padding.

```rust
#[repr(C)]
struct Point {
    x: i32,
    y: i32,
}
```

This ensures that the fields are laid out in the same way they would be in C, with no padding.

## Conclusion

Structs in Rust are a powerful feature for creating custom data types and organizing your code. They provide a way to encapsulate related data, and you can define methods to operate on that data. Structs are also used extensively with enums to represent complex data structures and are essential for building robust Rust applications.

