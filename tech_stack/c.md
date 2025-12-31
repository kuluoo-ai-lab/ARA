# C LANGUAGE FORMAL SPECIFICATION v17.0.0

## 12 PRIMARY C KEYWORDS

### 1. **VARIABLE** - Variable Declaration
```c
// Basic types
int age = 30;
float height = 5.9f;
char initial = 'J';
double pi = 3.14159;
short count = 100;
long bigNumber = 1000000L;

// Pointers
int *ptr = &age;
int **doublePtr = &ptr;

// Arrays
int scores[10];
int matrix[3][3];

// Const
const int MAX = 100;
```

### 2. **FUNCTION** - Function Definition
```c
// Function declaration
int add(int a, int b);

// Function definition
int add(int a, int b) {
    return a + b;
}

// Void function
void printHello() {
    printf("Hello!\n");
}

// Pointer function
int* createArray(int size) {
    int *arr = (int*)malloc(size * sizeof(int));
    return arr;
}

// Function pointer
int (*funcPtr)(int, int) = &add;
```

### 3. **STRUCT** - Structure Definition
```c
// Struct definition
struct User {
    int id;
    char name[100];
    char email[100];
};

// Typedef
typedef struct {
    int id;
    char name[100];
} User;

// Struct initialization
User user = {1, "John", "john@example.com"};

// Struct pointer
User *userPtr = malloc(sizeof(User));
userPtr->id = 1;
free(userPtr);
```

### 4. **POINTER** - Pointer Operations
```c
// Pointer declaration
int x = 10;
int *ptr = &x;  // Get address

// Dereference
int value = *ptr;  // Get value

// Array as pointer
int arr[5] = {1, 2, 3, 4, 5};
int *arrPtr = arr;  // arr is pointer to first element
int firstElement = *arrPtr;
int secondElement = *(arrPtr + 1);  // Or arrPtr[1]

// Null pointer
int *nullPtr = NULL;
if (ptr != NULL) {
    // Safe to use
}
```

### 5. **MEMORY** - Memory Management
```c
// Allocate memory
int *arr = (int*)malloc(10 * sizeof(int));

// Zero-initialized allocation
int *arr2 = (int*)calloc(10, sizeof(int));

// Reallocate
int *newArr = (int*)realloc(arr, 20 * sizeof(int));

// Free memory
free(arr);
arr = NULL;  // Avoid dangling pointer
```

### 6. **STRING** - String Operations
```c
#include <string.h>

// String declaration
char str[100] = "Hello";
char *strPtr = "World";

// String functions
strlen(str);          // Length
strcpy(dest, src);    // Copy
strcat(dest, src);    // Concatenate
strcmp(str1, str2);   // Compare
strchr(str, 'H');     // Find character
```

### 7. **ARRAY** - Array Operations
```c
// Array declaration
int arr[10];
int matrix[3][4];

// Initialization
int arr[] = {1, 2, 3, 4, 5};

// Access elements
arr[0] = 10;
int value = arr[1];

// Multi-dimensional
matrix[0][0] = 1;
```

### 8. **CONTROL** - Control Flow
```c
// If/else
if (x > 10) {
    printf("Greater than 10\n");
} else {
    printf("Less than or equal to 10\n");
}

// Switch
switch (status) {
    case 1:
        printf("Active\n");
        break;
    case 0:
        printf("Inactive\n");
        break;
    default:
        printf("Unknown\n");
}

// Ternary
char *result = (x > 10) ? "yes" : "no";
```

### 9. **LOOP** - Iteration
```c
// For loop
for (int i = 0; i < 10; i++) {
    printf("%d\n", i);
}

// While loop
int count = 0;
while (count < 10) {
    printf("%d\n", count);
    count++;
}

// Do-while loop
do {
    printf("Enter number: ");
    scanf("%d", &num);
} while (num != 0);
```

### 10. **INPUT** - Input/Output
```c
#include <stdio.h>

// Print
printf("Value: %d\n", value);
printf("String: %s\n", str);
printf("Float: %.2f\n", pi);

// Read
scanf("%d", &number);
scanf("%s", str);
fgets(str, sizeof(str), stdin);

// File operations
FILE *file = fopen("file.txt", "r");
if (file != NULL) {
    char line[100];
    while (fgets(line, sizeof(line), file)) {
        printf("%s", line);
    }
    fclose(file);
}
```

### 11. **ERROR** - Error Handling
```c
#include <errno.h>

int result = open("file.txt", O_RDONLY);
if (result == -1) {
    perror("Error opening file");
    exit(EXIT_FAILURE);
}

// Check return values
FILE *file = fopen("file.txt", "r");
if (file == NULL) {
    fprintf(stderr, "Error opening file: %s\n", strerror(errno));
    return -1;
}
```

### 12. **HEADER** - Header Files & Organization
```c
// header.h
#ifndef HEADER_H
#define HEADER_H

struct User {
    int id;
    char name[100];
};

int add(int a, int b);

#endif

// program.c
#include "header.h"
#include <stdio.h>

int main() {
    struct User user = {1, "John"};
    int result = add(5, 3);
    printf("User: %s, Sum: %d\n", user.name, result);
    return 0;
}
```

## BEST PRACTICES
1. Always check return values
2. Manage memory carefully
3. Use const appropriately
4. Avoid buffer overflows
5. Use meaningful names
6. Comment complex logic
7. Test thoroughly
8. Validate user input
9. Use header guards
10. Follow coding standards
