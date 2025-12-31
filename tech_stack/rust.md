# RUST FORMAL SPECIFICATION v1.73.0

## 12 PRIMARY RUST KEYWORDS

### 1. **VARIABLE** - Variable Declaration
```rust
// Immutable binding
let x = 5;

// Mutable variable
let mut x = 5;
x = 6;

// Type annotation
let y: i32 = 10;

// Constants
const MAX_USERS: u32 = 100;

// Static
static STATIC_STR: &str = "hello";
```

### 2. **FUNCTION** - Function Definition
```rust
// Basic function
fn add(a: i32, b: i32) -> i32 {
    a + b  // Return value
}

// No return value
fn print_hello() {
    println!("Hello!");
}

// Generic function
fn largest<T: std::cmp::PartialOrd + std::marker::Copy>(list: &[T]) -> T {
    let mut largest = list[0];
    for &item in list {
        if item > largest {
            largest = item;
        }
    }
    largest
}
```

### 3. **OWNERSHIP** - Ownership System
```rust
// Ownership transfer
fn takes_ownership(s: String) {
    println!("{}", s);
} // s is dropped here

let s1 = String::from("hello");
takes_ownership(s1);
// s1 is no longer valid here

// Borrowing
fn borrows_reference(s: &String) {
    println!("{}", s);
} // s is not dropped

let s2 = String::from("world");
borrows_reference(&s2);
// s2 is still valid

// Mutable borrowing
fn borrows_mutable(s: &mut String) {
    s.push_str(" world");
}

let mut s3 = String::from("hello");
borrows_mutable(&mut s3);
```

### 4. **STRUCT** - Struct Definition
```rust
// Struct definition
struct User {
    id: u32,
    name: String,
    email: String,
}

// Struct implementation
impl User {
    fn new(id: u32, name: String, email: String) -> User {
        User { id, name, email }
    }
    
    fn describe(&self) -> String {
        format!("User: {}", self.name)
    }
}

// Usage
let user = User::new(1, String::from("John"), String::from("john@example.com"));
println!("{}", user.describe());
```

### 5. **ENUM** - Enumeration
```rust
enum Status {
    Active,
    Inactive,
    Pending,
}

enum Result<T> {
    Ok(T),
    Err(String),
}

match status {
    Status::Active => println!("Active"),
    Status::Inactive => println!("Inactive"),
    Status::Pending => println!("Pending"),
}
```

### 6. **TRAIT** - Trait Definition
```rust
trait Drawable {
    fn draw(&self);
    fn area(&self) -> f64;
}

struct Circle {
    radius: f64,
}

impl Drawable for Circle {
    fn draw(&self) {
        println!("Drawing circle");
    }
    
    fn area(&self) -> f64 {
        std::f64::consts::PI * self.radius * self.radius
    }
}
```

### 7. **PATTERN** - Pattern Matching
```rust
match value {
    0 => println!("Zero"),
    1..=10 => println!("One to ten"),
    _ => println!("Other"),
}

// Destructuring
let (x, y) = (5, 10);

// Destructuring struct
let User { id, name, .. } = user;

// Option pattern
if let Some(value) = optional {
    println!("Value: {}", value);
}
```

### 8. **ERROR** - Error Handling
```rust
use std::io;

fn read_file(path: &str) -> Result<String, io::Error> {
    std::fs::read_to_string(path)
}

// Using ?  operator
fn process_file() -> Result<(), Box<dyn std::error::Error>> {
    let content = std::fs::read_to_string("file.txt")?;
    println!("{}", content);
    Ok(())
}

// Match error
match read_file("path") {
    Ok(content) => println!("{}", content),
    Err(e) => eprintln!("Error: {}", e),
}
```

### 9. **LIFETIME** - Lifetime Annotations
```rust
// Function with lifetime
fn longest<'a>(s1: &'a str, s2: &'a str) -> &'a str {
    if s1.len() > s2.len() { s1 } else { s2 }
}

// Struct with lifetime
struct User<'a> {
    name: &'a str,
}

// Lifetime elision
fn first_word(s: &str) -> &str {
    let bytes = s.as_bytes();
    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }
    &s[..]
}
```

### 10. **ASYNC** - Async/Await
```rust
use tokio::task;

async fn fetch_data(url: &str) -> Result<String, Box<dyn std::error::Error>> {
    let response = reqwest::get(url).await?;
    let body = response.text().await?;
    Ok(body)
}

#[tokio::main]
async fn main() {
    match fetch_data("https://example.com").await {
        Ok(data) => println!("{}", data),
        Err(e) => eprintln!("Error: {}", e),
    }
}

// Join multiple tasks
let (result1, result2) = tokio::join!(
    fetch_data("url1"),
    fetch_data("url2")
);
```

### 11. **MACRO** - Macros
```rust
// println! macro
println!("Hello, {}!", "world");

// Custom macro
macro_rules! test {
    ($x:expr) => {
        println!("Value: {}", $x);
    };
}

test!(42);

// Derive macro
#[derive(Debug, Clone)]
struct User {
    name: String,
}
```

### 12. **TESTING** - Testing
```rust
#[cfg(test)]
mod tests {
    use super::*;
    
    #[test]
    fn test_add() {
        assert_eq!(add(2, 3), 5);
    }
    
    #[test]
    fn test_ownership() {
        let s = String::from("hello");
        assert_eq!(s.len(), 5);
    }
    
    #[test]
    #[should_panic]
    fn test_panic() {
        panic!("Expected panic");
    }
}

// Run tests: cargo test
```

## BEST PRACTICES
1. Understand ownership rules
2. Use borrows instead of moves
3. Prefer immutability
4. Use Result for fallible operations
5. Leverage pattern matching
6. Use traits for abstraction
7. Write tests alongside code
8. Manage memory safely
9. Use iterators effectively
10. Document with doc comments
