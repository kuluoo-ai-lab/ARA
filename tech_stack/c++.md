# C++ LANGUAGE FORMAL SPECIFICATION v23.0

## 12 PRIMARY C++ KEYWORDS

### 1. **CLASS** - Class Definition
```cpp
class User {
private:
    int id;
    std::string name;

public:
    User(int id, const std::string& name) : id(id), name(name) {}
    
    int getId() const { return id; }
    std::string getName() const { return name; }
    
    void setName(const std::string& newName) {
        name = newName;
    }
    
    virtual ~User() = default;
};

// Usage
User user(1, "John");
std::cout << user.getName() << std::endl;
```

### 2. **TEMPLATE** - Template Programming
```cpp
// Template function
template<typename T>
T add(T a, T b) {
    return a + b;
}

// Template class
template<typename T>
class Stack {
private:
    std::vector<T> items;

public:
    void push(const T& value) {
        items.push_back(value);
    }
    
    T pop() {
        T value = items.back();
        items.pop_back();
        return value;
    }
};

// Usage
Stack<int> intStack;
intStack.push(42);
int value = intStack.pop();
```

### 3. **INHERITANCE** - Object Inheritance
```cpp
// Base class
class Animal {
public:
    virtual void speak() {
        std::cout << "Some sound\n";
    }
    virtual ~Animal() = default;
};

// Derived class
class Dog : public Animal {
public:
    void speak() override {
        std::cout << "Woof\n";
    }
};

// Usage
Animal *animal = new Dog();
animal->speak();  // Prints "Woof"
delete animal;
```

### 4. **POINTER** - Smart Pointers
```cpp
// Unique pointer (exclusive ownership)
std::unique_ptr<User> user1(new User(1, "John"));
std::unique_ptr<User> user2 = std::move(user1);
// user1 is now nullptr

// Shared pointer (shared ownership)
std::shared_ptr<User> sharedUser(new User(2, "Jane"));
std::shared_ptr<User> anotherRef = sharedUser;
// Both own the object, freed when all go out of scope

// Make smart pointer
auto user = std::make_unique<User>(3, "Bob");
```

### 5. **VECTOR** - Dynamic Arrays
```cpp
std::vector<int> numbers = {1, 2, 3, 4, 5};

// Operations
numbers.push_back(6);
numbers.pop_back();
numbers.size();
numbers.empty();
numbers.clear();

// Iteration
for (int num : numbers) {
    std::cout << num << " ";
}

// Access
int first = numbers[0];
int second = numbers.at(1);  // With bounds checking
```

### 6. **MAP** - Key-Value Containers
```cpp
std::map<std::string, int> ages;
ages["John"] = 30;
ages["Jane"] = 25;

// Check if key exists
if (ages.find("John") != ages.end()) {
    std::cout << ages["John"] << std::endl;
}

// Iteration
for (const auto& [name, age] : ages) {
    std::cout << name << ": " << age << std::endl;
}

// Unordered map (faster lookup)
std::unordered_map<std::string, int> fastMap;
```

### 7. **STRING** - String Operations
```cpp
std::string str = "Hello, World!";

// Operations
str.length();
str.substr(0, 5);         // Substring
str.find("World");        // Find position
str.replace(0, 5, "Hi");  // Replace
str.append(" More");      // Append

// String conversion
int num = std::stoi("42");
double pi = std::stod("3.14");
std::string numStr = std::to_string(42);

// String stream
std::stringstream ss;
ss << "Age: " << 30;
std::string result = ss.str();
```

### 8. **EXCEPTION** - Exception Handling
```cpp
try {
    if (age < 0) {
        throw std::invalid_argument("Age cannot be negative");
    }
    
    int arr[5];
    arr.at(10);  // Throws out_of_range
} catch (const std::invalid_argument& e) {
    std::cerr << "Invalid argument: " << e.what() << std::endl;
} catch (const std::out_of_range& e) {
    std::cerr << "Out of range: " << e.what() << std::endl;
} catch (const std::exception& e) {
    std::cerr << "Error: " << e.what() << std::endl;
}
```

### 9. **ALGORITHM** - STL Algorithms
```cpp
std::vector<int> numbers = {3, 1, 4, 1, 5, 9};

// Sort
std::sort(numbers.begin(), numbers.end());

// Find
auto it = std::find(numbers.begin(), numbers.end(), 4);

// Transform
std::transform(numbers.begin(), numbers.end(), 
               numbers.begin(), 
               [](int x) { return x * 2; });

// Filter
std::vector<int> filtered;
std::copy_if(numbers.begin(), numbers.end(),
             std::back_inserter(filtered),
             [](int x) { return x > 5; });
```

### 10. **LAMBDA** - Lambda Functions
```cpp
// Simple lambda
auto add = [](int a, int b) { return a + b; };
int result = add(5, 3);

// Lambda with capture
int multiplier = 2;
auto multiply = [multiplier](int x) { return x * multiplier; };

// Lambda with auto
std::vector<int> numbers = {1, 2, 3, 4, 5};
std::for_each(numbers.begin(), numbers.end(),
              [](int num) { std::cout << num << " "; });

// Complex lambda
auto findMax = [](const std::vector<int>& vec) {
    return *std::max_element(vec.begin(), vec.end());
};
```

### 11. **STREAM** - Input/Output Streams
```cpp
#include <iostream>
#include <fstream>

// Console I/O
std::cout << "Hello" << std::endl;
std::cin >> name;
std::getline(std::cin, line);

// File I/O
std::ofstream outFile("output.txt");
outFile << "Hello, World!" << std::endl;
outFile.close();

std::ifstream inFile("input.txt");
std::string line;
while (std::getline(inFile, line)) {
    std::cout << line << std::endl;
}
inFile.close();

// String stream
std::stringstream ss("42");
int value;
ss >> value;
```

### 12. **TESTING** - Unit Testing
```cpp
#include <cassert>
#include <gtest/gtest.h>

// Simple assert
void testAdd() {
    assert(add(2, 3) == 5);
}

// Google Test
TEST(MathTest, Addition) {
    EXPECT_EQ(add(2, 3), 5);
    EXPECT_NE(add(2, 3), 6);
}

TEST(MathTest, Subtraction) {
    EXPECT_GT(subtract(5, 2), 0);
    EXPECT_LT(subtract(2, 5), 0);
}

// Run with: ./program --gtest_filter="*"
```

## BEST PRACTICES
1. Use smart pointers
2. Prefer STL containers
3. Use modern C++ features (C++17+)
4. Follow RAII principles
5. Avoid raw pointers
6. Use const correctly
7. Leverage templates
8. Handle exceptions
9. Use auto wisely
10. Test thoroughly

---
