# Advanced-C
## Chapter 1 Pointers 8Hrs
- 1.1. Introduction to Pointers.
- 1.2. Declaration, definition, initialization, dereferencing.
- 1.3. Pointer arithmetic.
- 1.4. Relationship between Arrays & Pointers- Pointer to array, Array of pointers.
- 1.5. Multiple indirection (pointer to pointer).
- 1.6. Functions and pointers- Passing pointer to function, Returning pointer from function, Function pointer.
- 1.7. Dynamic memory management- Allocation(malloc(),calloc()), Resizing(realloc()), Releasing(free()).,
- 1.8. Memory leak, dangling pointers.
- 1.9. Types of pointers.
  
## Chapter 2 Strings 6Hrs
- 2.1 String Literals, string variables, declaration, definition, initialization.
- 2.2 Syntax and use of predefined string functions
- 2.3 Array of strings.
- 2.4. Strings and Pointers
- 2.5. Command line arguments.
  
## Chapter 3 Structures And Unions 8Hrs
- 3.1. Concept of structure, definition and initialization, use of typedef.
- 3.2. Accessing structure members.
- 3.3. Nested Structures
- 3.4. Arrays of Structures
- 3.5. Structures and functions- Passing each member of structure as a separate argument, Passing structure by value / address.
- 3.6. Pointers and structures.
- 3.7. Concept of Union, declaration, definition, accessing union members.
- 3.8. Difference between structures and union.
  
## Chapter 4 File Handling 6Hrs
- 4.1. Introduction to streams.
- 4.2. Types of files.
- 4.3. Operations on text files.
- 4.4. Standard library input/output functions.
- 4.5. Random access to files.
  
## Chapter 5 Preprocessor 2Hrs
- 5.1. Role of Preprocessor
- 5.2. Format of preprocessor directive
- 5.3. File inclusion directives (#include)
- 5.4. Macro substitution directive, argumented and nested macro
- 5.5. Macros versus functions               


## Chapter 1 Pointers

### 1.1. Introduction to Pointers
- A pointer in C is a variable that stores the memory address of another variable.
- Instead of holding a direct value like an integer or character, a pointer stores the location of where the data is stored in memory.
- This provides flexibility in how data is accessed and manipulated in programs, enabling efficient memory management and function handling.

* Why use pointers?
•	Memory management: Pointers allow for dynamic memory allocation and efficient use of memory.
•	Efficient function handling: They allow functions to modify variables from the calling function.
•	Array and string manipulation: Since arrays are implemented as pointers, pointers simplify their use.
•	Dynamic data structures: Pointers are essential for creating linked lists, trees, and other data structures.
---
### 1.2. Declaration, Definition, Initialization, Dereferencing
#### Declaration:
-In C, pointers are declared using the * operator, which tells the compiler that the variable is a pointer.

```c
int *ptr;   // Declares a pointer to an integer
```

#### Definition:
- When a pointer is defined, it must be initialized with the address of a variable.
```c
int num = 5;
int *ptr = &num;   // Defines a pointer and initializes it with the address of num
```
#### Initialization:
- Initialization refers to assigning the pointer to a valid memory address.
```c
ptr = &num;   // Initializes ptr with the address of num
```
#### Dereferencing:
- Dereferencing a pointer means accessing the value stored at the memory address it points to, using the * operator.
```c
int value = *ptr;  // Dereferencing ptr to get the value of num
```
Example:
```c
#include <stdio.h>

int main() {
    int num = 10;
    int *ptr = &num;  // Pointer initialization
    printf("Value of num: %d\n", num);
    printf("Value using pointer: %d\n", *ptr);  // Dereferencing pointer
    return 0;
}
```
---
### 1.3. Pointer Arithmetic
- Pointers can be manipulated using arithmetic operations. 
- Pointer arithmetic is commonly used to traverse arrays.
•	Increment (ptr++): Moves the pointer to the next element of the type it points to.
•	Decrement (ptr--): Moves the pointer to the previous element.
•	Addition (ptr + n): Moves the pointer n elements ahead.
•	Subtraction (ptr - n): Moves the pointer n elements backward.
•	Difference (ptr1 - ptr2): Finds the number of elements between two pointers (assuming both point to elements of the same array).

#### Example:
```c
#include <stdio.h>

int main() {
    int arr[] = {10, 20, 30, 40};
    int *ptr = arr;

    printf("Value at ptr: %d\n", *ptr);  // 10
    ptr++;  // Move to the next element
    printf("Value after increment: %d\n", *ptr);  // 20

    return 0;
}
```
---
### 1.4. Relationship between Arrays & Pointers
* Pointer to Array:
- An array name in C is essentially a pointer to its first element.
- An array's address can be assigned to a pointer, and you can use the pointer to access array elements.

```c
int arr[] = {1, 2, 3, 4};
int *ptr = arr;  // Pointer to the first element of the array
```
### Array of Pointers:
- An array of pointers is an array where each element is a pointer that can point to different variables or memory locations.
```c
int a = 10, b = 20, c = 30;
int *arr[] = {&a, &b, &c};  // Array of pointers
```
Example:
```c
#include <stdio.h>

int main() {
    int arr[] = {10, 20, 30, 40};
    int *ptr = arr;
    for (int i = 0; i < 4; i++) {
        printf("%d ", *(ptr + i));  // Access array elements using pointer
    }
    return 0;
}
```
---
### 1.5. Multiple Indirection (Pointer to Pointer)
- A pointer to a pointer is a variable that stores the address of another pointer.
- This allows you to indirectly access the data stored in the original pointer.
#### Declaration:
```c
int num = 10;
int *ptr = &num;
int **ptr2 = &ptr;  // Pointer to pointer
```
#### Dereferencing a pointer to a pointer:
```c
int value = **ptr2;  // Dereference twice to get the value of num
```
#### Example:
```c
#include <stdio.h>

int main() {
    int num = 5;
    int *ptr = &num;
    int **ptr2 = &ptr;

    printf("Value of num: %d\n", num);
    printf("Value using pointer to pointer: %d\n", **ptr2);

    return 0;
}
```

#### 1.6. Functions and Pointers
- Passing Pointer to Function:
- Passing a pointer to a function allows the function to modify the original data in the caller’s memory.

```c
void modify(int *ptr) {
    *ptr = 20;
}

int main() {
    int num = 10;
    modify(&num);  // Pass the address of num
    printf("Modified value: %d\n", num);  // Output: 20
    return 0;
}
```

#### Returning Pointer from Function:
- Functions can return a pointer to a variable.
- However, it is essential that the variable remains in scope (i.e., it must not be a local variable that gets destroyed when the function returns).

```c
int* getPointerToInt() {
    int *ptr = malloc(sizeof(int));  // Dynamically allocate memory
    *ptr = 100;
    return ptr;
}
```
#### Function Pointers:
- A function pointer is a pointer that points to the address of a function. It can be used to call functions dynamically.

```c
#include <stdio.h>

void greet() {
    printf("Hello, world!\n");
}

int main() {
    void (*func_ptr)() = greet;
    func_ptr();  // Call greet function using function pointer
    return 0;
}
```


#### 1.7. Dynamic Memory Management
- Allocation (malloc(), calloc()):
•	malloc(size_t size) allocates a block of memory of the specified size (in bytes) and returns a pointer to it.
•	calloc(num, size) allocates memory for an array of num elements, each of size bytes, and initializes all elements to zero.

```c
int *arr = (int *)malloc(5 * sizeof(int));  // Allocates space for 5 integers
int *arr_zero = (int *)calloc(5, sizeof(int));  // Allocates and initializes to zero
```

- Resizing (realloc()):
•	realloc(ptr, new_size) changes the size of the memory block pointed to by ptr to new_size.

```c
arr = (int *)realloc(arr, 10 * sizeof(int));  // Resize the array to hold 10 integers
Releasing (free()):
•	free(ptr) releases a previously allocated block of memory.

free(arr);  // Frees the dynamically allocated memory
```

#### 1.8. Memory Leak, Dangling Pointers
**Memory Leak:**
- A memory leak occurs when dynamically allocated memory is not freed, leading to wasted memory over time.
```c
int *ptr = (int *)malloc(10 * sizeof(int));  // Memory allocated
// Forgetting to call free(ptr) causes a memory leak
```

**Dangling Pointers:**
- A dangling pointer occurs when a pointer still references a memory location after it has been freed.
- Accessing this pointer can lead to undefined behavior.

```c
int *ptr = (int *)malloc(10 * sizeof(int));
free(ptr);
*ptr = 10;  // Dangling pointer, undefined behavior
```

**1.9. Types of Pointers**
•	Null Pointer (NULL): A pointer that does not point to any valid memory location.
•	Void Pointer (void *): A pointer that can point to any data type. It needs to be cast to the appropriate type before dereferencing.
•	Function Pointer: A pointer to a function.
•	Wild Pointer: A pointer that is not initialized properly.
•	Constant Pointer: A pointer whose value (address) cannot be changed, but the value at that address can be modified.
•	Pointer to Constant: A pointer to a constant value (the value it points to cannot be changed, but the pointer itself can point to other variables).
