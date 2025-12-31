# JAVASCRIPT LANGUAGE FORMAL SPECIFICATION


## 12 PRIMARY JAVASCRIPT KEYWORDS

### 1. **VARIABLE** - Data Storage & Declaration
```javascript
// Declarations
const PI = 3.14159;              // Immutable
let counter = 0;                 // Block-scoped, mutable
var legacy = 'avoid';            // Function-scoped (legacy)

// Variable naming
const firstName = 'John';        // camelCase preferred
const CONSTANT_VALUE = 100;      // UPPER_CASE for constants
const _private = 'internal';     // Leading underscore convention

// Rules: Always use const/let, never var. Prefer const, use let when reassignment needed
```

### 2. **DATATYPE** - Primitive & Complex Types
```javascript
// Primitives
const string = 'text';
const number = 42;
const boolean = true;
const nullValue = null;
const undefinedValue = undefined;
const symbol = Symbol('unique');
const bigint = 100n;

// Objects
const object = { name: 'John', age: 30 };
const array = [1, 2, 3];
const set = new Set([1, 2, 3]);
const map = new Map([['key', 'value']]);

// Functions
const fn = (x) => x * 2;
const asyncFn = async (x) => await process(x);

// Type checking: Use typeof, instanceof, Array.isArray()
typeof 42 === 'number';
Array.isArray([]);
obj instanceof Object;
```

### 3. **FUNCTION** - Function Declaration & Invocation
```javascript
// Declaration
function add(a, b) { return a + b; }

// Arrow function
const multiply = (a, b) => a * b;

// Async function
async function fetchData(url) {
  const response = await fetch(url);
  return response.json();
}

// Parameters
function greet(name = 'Guest', ...rest) { }

// Closures
function counter() {
  let count = 0;
  return () => ++count;
}

// Rules: Use arrow functions for callbacks, regular functions for methods
```

### 4. **CONTROL** - Flow Control Structures
```javascript
// If/Else
if (condition) {
  // true case
} else if (other) {
  // other case
} else {
  // default case
}

// Switch
switch (value) {
  case 1: /* action */ break;
  case 2: /* action */ break;
  default: /* action */
}

// Ternary
const result = condition ? 'yes' : 'no';

// Logical operators
condition1 && action1();
condition2 || action2();

// Rules: Prefer ternary for simple conditions, avoid nested ternaries
```

### 5. **LOOP** - Iteration Structures
```javascript
// For loop
for (let i = 0; i < 10; i++) { }

// While loop
while (condition) { }

// For...of (arrays, strings)
for (const item of array) { }

// For...in (object keys)
for (const key in object) { }

// Array methods (preferred)
array.forEach(item => { });
array.map(item => item * 2);
array.filter(item => item > 0);
array.reduce((acc, item) => acc + item, 0);

// Rules: Prefer array methods over loops, avoid for...in
```

### 6. **OBJECT** - Object Creation & Manipulation
```javascript
// Object literal
const person = {
  name: 'John',
  age: 30,
  greet() { return `Hello, ${this.name}`; }
};

// Destructuring
const { name, age } = person;
const [first, second] = array;

// Spread operator
const copy = { ...original };
const merged = { ...obj1, ...obj2 };

// Classes
class Animal {
  constructor(name) { this.name = name; }
  speak() { console.log(`${this.name} speaks`); }
}

// Rules: Use object methods for data, classes for complex types
```

### 7. **ASYNC** - Asynchronous Programming
```javascript
// Promises
fetch(url)
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// Async/await
async function getData() {
  try {
    const response = await fetch(url);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error(error);
  }
}

// Promise.all
Promise.all([promise1, promise2, promise3])
  .then(results => { });

// Rules: Prefer async/await over .then(), always handle errors
```

### 8. **MANIPULATION** - DOM & Data Manipulation
```javascript
// DOM selection
const element = document.getElementById('id');
const elements = document.querySelectorAll('.class');

// DOM modification
element.textContent = 'text';
element.innerHTML = '<span>html</span>';
element.classList.add('active');
element.style.color = 'red';

// Event handling
element.addEventListener('click', (event) => {
  console.log(event.target);
});

// Data transformation
const doubled = array.map(x => x * 2);
const filtered = array.filter(x => x > 0);
const summed = array.reduce((a, b) => a + b, 0);

// Rules: Use dataset for custom attributes, avoid inline styles
```

### 9. **ERROR** - Error Handling & Validation
```javascript
// Try/catch
try {
  riskyOperation();
} catch (error) {
  console.error('Error:', error.message);
} finally {
  cleanup();
}

// Throwing errors
if (!value) {
  throw new Error('Value required');
}

// Custom errors
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = 'ValidationError';
  }
}

// Validation
if (typeof value !== 'string') {
  throw new TypeError('Must be string');
}

// Rules: Use specific error types, always provide context
```

### 10. **MODULE** - Modules & Imports
```javascript
// Named exports
export const util = () => { };
export class MyClass { }

// Default export
export default MyComponent;

// Imports
import MyComponent from './component.js';
import { util, MyClass } from './utils.js';
import * as utils from './utils.js';

// Dynamic imports
const module = await import('./dynamic.js');

// Rules: Use named exports for utilities, default for components
```

### 11. **PATTERN** - Common Patterns & Best Practices
```javascript
// Singleton
const singleton = {
  instance: null,
  getInstance() {
    if (!this.instance) {
      this.instance = new Class();
    }
    return this.instance;
  }
};

// Factory
function createUser(name, role) {
  return { name, role, created: Date.now() };
}

// Observer
class Subject {
  constructor() { this.observers = []; }
  subscribe(observer) { this.observers.push(observer); }
  notify(data) { this.observers.forEach(o => o(data)); }
}

// Debounce
const debounce = (fn, wait) => {
  let timeout;
  return (...args) => {
    clearTimeout(timeout);
    timeout = setTimeout(() => fn(...args), wait);
  };
};

// Rules: Use patterns to solve common problems, not over-engineer
```

### 12. **TESTING** - Testing & Quality Assurance
```javascript
// Jest testing
describe('Calculator', () => {
  test('adds numbers correctly', () => {
    expect(add(2, 3)).toBe(5);
  });
  
  test('handles edge cases', () => {
    expect(add(0, 0)).toBe(0);
  });
});

// Assertions
expect(value).toBe(expected);
expect(value).toEqual(expected);
expect(array).toContain(item);
expect(fn).toThrow();
expect(value).toBeTruthy();

// Mocking
jest.mock('./module.js');
const mockFn = jest.fn();

// Rules: Test behavior, not implementation. Aim for 80%+ coverage
```

## 6-STEP JAVASCRIPT GENERATION WORKFLOW

### STEP-1: UNDERSTAND INTENT
- What functionality needed?
- What libraries/frameworks?
- Async requirements?
- Browser/Node compatibility?
- Performance targets?

### STEP-2: ARCHITECTURE PLANNING
```
Cache memory:
- Framework choice
- Async pattern (promises/async-await)
- Module system (ESM/CommonJS)
- Testing approach
- Error handling strategy
```

### STEP-3: RETRIEVE LANGUAGE RULES
```
Rules:
- Const/let, never var
- Arrow functions for callbacks
- Async/await preferred
- DRY principle
- Semantic naming
- Error handling required
- Type safety (JSDoc or TypeScript)
```

### STEP-4: REQUIREMENTS CHECKLIST
```
☐ Type definitions (JSDoc/TypeScript)
☐ Error handling in place
☐ Async patterns consistent
☐ DOM queries optimized
☐ Event listeners cleaned
☐ Comments added
☐ Tests written (80%+ coverage)
☐ Performance optimized
```

### STEP-5: GENERATION ROADMAP
```
PHASE 1: STRUCTURE
├─ Module definitions
├─ Type definitions
└─ Error classes

PHASE 2: CORE LOGIC
├─ Main functions
├─ Utilities
└─ Data transformations

PHASE 3: ASYNC HANDLING
├─ API calls
├─ Promise chains
└─ Error handling

PHASE 4: UI INTEGRATION
├─ DOM manipulation
├─ Event listeners
└─ State management

PHASE 5: TESTING
├─ Unit tests
├─ Integration tests
└─ Edge cases

PHASE 6: OPTIMIZATION
├─ Minification
├─ Tree-shaking
├─ Code splitting
└─ Performance
```

### STEP-6: EXECUTE GENERATION
```javascript
// Production-ready structure
'use strict';

// Constants
const API_URL = 'https://api.example.com';
const TIMEOUT = 5000;

// Utilities
const debounce = (fn, wait) => {
  let timeout;
  return (...args) => {
    clearTimeout(timeout);
    timeout = setTimeout(() => fn(...args), wait);
  };
};

// Main class
class DataManager {
  constructor(apiUrl = API_URL) {
    this.apiUrl = apiUrl;
    this.cache = new Map();
  }
  
  async fetchData(endpoint) {
    if (this.cache.has(endpoint)) {
      return this.cache.get(endpoint);
    }
    
    try {
      const response = await fetch(`${this.apiUrl}${endpoint}`);
      if (!response.ok) throw new Error(`HTTP ${response.status}`);
      
      const data = await response.json();
      this.cache.set(endpoint, data);
      return data;
    } catch (error) {
      console.error('Fetch error:', error);
      throw error;
    }
  }
}

// Export
export default DataManager;
```

## BEST PRACTICES

1. **Always use const by default** - let when reassignment needed
2. **Prefer async/await** over promises for readability
3. **Handle errors explicitly** - try/catch or .catch()
4. **Use descriptive names** - variable and function names
5. **Keep functions small** - single responsibility
6. **Avoid global scope** - use modules and classes
7. **Test thoroughly** - unit and integration tests
8. **Optimize performance** - minimize DOM queries
9. **Type safety** - JSDoc or TypeScript
10. **Document code** - comments for complex logic

---


