# JAVA LANGUAGE FORMAL SPECIFICATION 

## 12 PRIMARY JAVA KEYWORDS

### 1. **CLASS** - Class Definition
```java
public class User {
    private int id;
    private String name;
    private String email;
    
    public User(int id, String name, String email) {
        this.id = id;
        this.name = name;
        this.email = email;
    }
    
    public int getId() { return id; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    
    @Override
    public String toString() {
        return "User{" +
            "id=" + id +
            ", name='" + name + '\'' +
            ", email='" + email + '\'' +
            '}';
    }
}
```

### 2. **INTERFACE** - Interface Definition
```java
public interface Drawable {
    void draw();
    double getArea();
}

public class Circle implements Drawable {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing circle");
    }
    
    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
}
```

### 3. **INHERITANCE** - Object Inheritance
```java
public class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public void speak() {
        System.out.println("Some sound");
    }
}

public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    @Override
    public void speak() {
        System.out.println("Woof!");
    }
}
```

### 4. **GENERICS** - Generic Types
```java
public class Container<T> {
    private T value;
    
    public void set(T value) {
        this.value = value;
    }
    
    public T get() {
        return value;
    }
}

// Usage
Container<String> stringContainer = new Container<>();
stringContainer.set("Hello");
String value = stringContainer.get();

// Wildcard
void printList(List<?> list) {
    for (Object obj : list) {
        System.out.println(obj);
    }
}
```

### 5. **COLLECTION** - Collections Framework
```java
import java.util.*;

// List
List<String> names = new ArrayList<>();
names.add("John");
names.add("Jane");
names.get(0);
names.remove(0);

// Set
Set<Integer> numbers = new HashSet<>();
numbers.add(1);
numbers.add(2);

// Map
Map<String, Integer> ages = new HashMap<>();
ages.put("John", 30);
ages.get("John");

// Iteration
for (String name : names) {
    System.out.println(name);
}

// Stream
names.stream()
    .filter(n -> n.startsWith("J"))
    .forEach(System.out::println);
```

### 6. **EXCEPTION** - Exception Handling
```java
public class FileReader {
    public String readFile(String path) throws IOException {
        FileInputStream fis = new FileInputStream(path);
        try {
            return new String(fis.readAllBytes());
        } finally {
            fis.close();
        }
    }
}

// Usage
try {
    String content = reader.readFile("file.txt");
} catch (FileNotFoundException e) {
    System.err.println("File not found: " + e.getMessage());
} catch (IOException e) {
    System.err.println("IO error: " + e.getMessage());
}

// Try-with-resources
try (FileInputStream fis = new FileInputStream("file.txt")) {
    byte[] data = fis.readAllBytes();
} catch (IOException e) {
    e.printStackTrace();
}
```

### 7. **ANNOTATION** - Annotations
```java
// Built-in annotations
@Override
public String toString() { }

@Deprecated
public void oldMethod() { }

@SuppressWarnings("unchecked")
List rawList = new ArrayList();

// Custom annotation
@interface MyAnnotation {
    String value();
    int count() default 1;
}

@MyAnnotation(value = "test")
public class AnnotatedClass { }
```

### 8. **STREAM** - Stream Processing
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Map
numbers.stream()
    .map(n -> n * 2)
    .forEach(System.out::println);

// Filter
numbers.stream()
    .filter(n -> n > 2)
    .forEach(System.out::println);

// Reduce
int sum = numbers.stream()
    .reduce(0, (a, b) -> a + b);

// Collect
List<Integer> filtered = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
```

### 9. **LAMBDA** - Lambda Expressions
```java
// Lambda
Predicate<Integer> isEven = (n) -> n % 2 == 0;
Function<Integer, Integer> double = (n) -> n * 2;
Consumer<String> print = (s) -> System.out.println(s);

// Functional interface
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

Calculator add = (a, b) -> a + b;
Calculator subtract = (a, b) -> a - b;

// Method reference
list.forEach(System.out::println);
list.stream().map(String::valueOf);
```

### 10. **OPTIONAL** - Optional Type
```java
Optional<String> name = Optional.of("John");
Optional<String> empty = Optional.empty();

// Check and get
if (name.isPresent()) {
    System.out.println(name.get());
}

// Or else
String value = name.orElse("Unknown");
String value2 = name.orElseGet(() -> "Default");

// Filter and map
name.filter(n -> n.startsWith("J"))
    .map(String::toUpperCase)
    .ifPresent(System.out::println);
```

### 11. **THREAD** - Threading
```java
// Extend Thread
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running");
    }
}

MyThread thread = new MyThread();
thread.start();

// Implement Runnable
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable running");
    }
}

Thread thread2 = new Thread(new MyRunnable());
thread2.start();

// ExecutorService
ExecutorService executor = Executors.newFixedThreadPool(2);
executor.submit(() -> System.out.println("Task"));
executor.shutdown();
```

### 12. **TESTING** - Unit Testing
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {
    private Calculator calculator = new Calculator();
    
    @Test
    public void testAddition() {
        assertEquals(5, calculator.add(2, 3));
    }
    
    @Test
    public void testSubtraction() {
        assertEquals(1, calculator.subtract(3, 2));
    }
    
    @Test
    public void testException() {
        assertThrows(ArithmeticException.class, 
            () -> calculator.divide(10, 0));
    }
}
```

## BEST PRACTICES
1. Follow JavaBeans conventions
2. Use interfaces for abstraction
3. Leverage collections framework
4. Use generics for type safety
5. Handle exceptions properly
6. Use streams for functional operations
7. Test thoroughly with JUnit
8. Follow naming conventions
9. Use immutable objects where possible
10. Document public APIs

---
