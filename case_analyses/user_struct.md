# Case Study: `User` Struct

## Base Code
```rust
struct User {
    username: String,
    email: String,
    uri: String,
    active: bool,
}

impl User {
    fn new(username: String, email: String, uri: String) -> Self {
        Self {
            username,
            email,
            uri,
            active: true,
        }
    }
    
    fn deactivate(&mut self) {
        self.active = false;
    }
}

fn main() {
    let mut new_user = User::new(
        String::from("alfredodeza"),
        String::from("alfredodeza@example.com"),
        String::from("https://alfredodeza.com"),
    );
    
    println!("Hello, {}!", new_user.username);
    println!("Account {} status is: {}", new_user.username, new_user.active);
    new_user.deactivate();
    println!("Account {} status is: {}", new_user.username, new_user.active);
}
```

## Code Analysis
The provided code defines a `User` struct in Rust and implements methods to create and manipulate instances of this struct. Here is a summary of the main components:

### `User` Struct
The `User` struct contains the following fields:
- `username`: User's name (String)
- `email`: Email address (String)
- `uri`: URL associated with the user (String)
- `active`: Account status (bool)

### Implementation
- `new`: Associated function that creates a new instance of `User`.
- `deactivate`: Regular method that deactivates the user's account.

### Execution
The `main` function creates a user, prints information about them, deactivates the account, and prints the updated status.

## Reflection Questions

### What is an associated function in Rust, and how does it differ from regular methods?
An **associated function** is defined within the implementation of a struct but does not take `self` as the first parameter. This means it can be called without needing an instance of the struct. Regular **methods**, on the other hand, take `self`, allowing them to modify or access the instance's fields.

#### When would you choose to use an associated function instead of a regular method?
- To create new instances of a struct (`new`)
- For operations that do not require an instance

### Why is the associated function `new` used to create a `User` instance? What advantages does it offer?
The `new` function standardizes struct creation and improves code readability. It allows initializing default values and avoids the need to manually define all fields when instantiating `User`.

---

## Challenge Questions

### Modification: Create the associated function `from_email`
This function extracts the username from the email and creates a new `User`.

```rust
impl User {
    fn from_email(email: String) -> Self {
        let username = email.split('@').next().unwrap_or("").to_string();
        Self {
            username,
            email,
            uri: String::from(""),
            active: true,
        }
    }
}

fn main() {
    let new_user = User::from_email(String::from("john@example.com"));
    println!("{:?}", new_user);
}
```

### Modification: Create the method `update_uri`
This function updates the `uri` field of the `User` struct.

```rust
impl User {
    fn update_uri(&mut self, new_uri: String) {
        self.uri = new_uri;
    }
}

fn main() {
    let mut user = User::new(
        String::from("alfredodeza"),
        String::from("alfredodeza@example.com"),
        String::from("https://alfredodeza.com"),
    );
    
    user.update_uri(String::from("https://newsite.com"));
    println!("Updated URI: {}", user.uri);
}
```
