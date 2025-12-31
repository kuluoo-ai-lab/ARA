# SWIFT FORMAL SPECIFICATION v5.9.0

## 12 PRIMARY SWIFT KEYWORDS

### 1. **VARIABLE** - Variable Declaration
```swift
// Constants
let name = "John"
let age: Int = 30

// Variables
var counter = 0
var message: String = "Hello"

// Optionals
var optionalName: String? = nil
if let unwrapped = optionalName {
  print(unwrapped)
}

// Guard statement
guard let name = optionalName else {
  return
}
```

### 2. **FUNCTION** - Function Definition
```swift
// Basic function
func add(_ a: Int, _ b: Int) -> Int {
  return a + b
}

// Function with labels
func greet(name: String, age: Int) -> String {
  return "Hello, \(name). You are \(age) years old."
}

// Default parameters
func printMessage(_ message: String = "Hello") {
  print(message)
}

// Variadic parameters
func sum(_ numbers: Int...) -> Int {
  return numbers.reduce(0, +)
}
```

### 3. **STRUCT** - Struct Definition
```swift
struct User {
  var id: Int
  var name: String
  var email: String
  
  init(id: Int, name: String, email: String) {
    self.id = id
    self.name = name
    self.email = email
  }
  
  func getDisplayName() -> String {
    return name
  }
  
  mutating func updateEmail(_ newEmail: String) {
    self.email = newEmail
  }
}

let user = User(id: 1, name: "John", email: "john@example.com")
```

### 4. **CLASS** - Class Definition
```swift
class User {
  var id: Int
  var name: String
  
  init(id: Int, name: String) {
    self.id = id
    self.name = name
  }
  
  func getDescription() -> String {
    return "User: \(name)"
  }
  
  deinit {
    print("User deallocated")
  }
}

class AdminUser: User {
  var adminLevel: Int = 1
  
  override func getDescription() -> String {
    return super.getDescription() + " (Admin)"
  }
}
```

### 5. **PROTOCOL** - Protocol Definition
```swift
protocol Identifiable {
  var id: Int { get }
  func describe() -> String
}

struct User: Identifiable {
  let id: Int
  let name: String
  
  func describe() -> String {
    return "User: \(name)"
  }
}
```

### 6. **ENUM** - Enumeration
```swift
enum Status: String {
  case active
  case inactive
  case pending
}

enum Result<T> {
  case success(T)
  case failure(Error)
}

let result: Result<Int> = .success(42)
if case .success(let value) = result {
  print("Value: \(value)")
}
```

### 7. **CLOSURE** - Closure
```swift
// Simple closure
let add: (Int, Int) -> Int = { a, b in
  return a + b
}

// Trailing closure
array.map { item in
  return item * 2
}

// Escaping closure
func fetchData(completion: @escaping (String) -> Void) {
  DispatchQueue.global().async {
    completion("Data fetched")
  }
}
```

### 8. **EXTENSION** - Extension
```swift
extension String {
  func capitalize() -> String {
    return self.prefix(1).uppercased() + self.dropFirst()
  }
}

let message = "hello".capitalize() // "Hello"

extension User {
  func isAdmin() -> Bool {
    return self.role == "admin"
  }
}
```

### 9. **ERROR** - Error Handling
```swift
enum APIError: Error {
  case invalidURL
  case requestFailed(String)
  case decodingFailed
}

func fetchUser(id: Int) throws -> User {
  guard let url = URL(string: "https://api.example.com/users/\(id)") else {
    throw APIError.invalidURL
  }
  
  do {
    let data = try Data(contentsOf: url)
    let user = try JSONDecoder().decode(User.self, from: data)
    return user
  } catch {
    throw APIError.decodingFailed
  }
}

do {
  let user = try fetchUser(id: 1)
  print(user)
} catch APIError.invalidURL {
  print("Invalid URL")
} catch {
  print("Error: \(error)")
}
```

### 10. **ASYNC** - Async/Await
```swift
actor UserRepository {
  private var users: [User] = []
  
  func fetchUsers() async throws -> [User] {
    let url = URL(string: "https://api.example.com/users")!
    let (data, _) = try await URLSession.shared.data(from: url)
    return try JSONDecoder().decode([User].self, from: data)
  }
  
  nonisolated func getUserCount() -> Int {
    return 0
  }
}

// Usage
let repo = UserRepository()
let users = try await repo.fetchUsers()
```

### 11. **MEMORY** - Memory Management
```swift
class User {
  var name: String
  weak var delegate: UserDelegate?
  unowned let coordinator: Coordinator
  
  init(name: String, coordinator: Coordinator) {
    self.name = name
    self.coordinator = coordinator
  }
}

// Capture list in closures
let closure = { [weak self] in
  self?.updateUI()
}
```

### 12. **TESTING** - Unit Testing
```swift
import XCTest

class UserTests: XCTestCase {
  var user: User!
  
  override func setUp() {
    super.setUp()
    user = User(id: 1, name: "John")
  }
  
  override func tearDown() {
    user = nil
    super.tearDown()
  }
  
  func testUserCreation() {
    XCTAssertEqual(user.name, "John")
    XCTAssertEqual(user.id, 1)
  }
  
  func testAsyncOperation() async {
    let result = await fetchUser(id: 1)
    XCTAssertNotNil(result)
  }
}
```

## BEST PRACTICES
1. Use optionals wisely
2. Prefer structs over classes
3. Use protocols for abstraction
4. Handle errors explicitly
5. Use async/await for concurrency
6. Manage memory carefully (weak/unowned)
7. Use value types when possible
8. Test thoroughly
9. Follow naming conventions
10. Document public APIs

