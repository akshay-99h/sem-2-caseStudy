<!--markdown-pdf markdown-file-path-->
<!--grip file-name-->

# Introduction to Programming: Case Study

#### by Akshay Prabhat Mishra

### Topic: *Concept of function pointers and arrays*


- Every variable is a memory location and every memory location has its address defined which can be accessed using ampersand (&) operator, which denotes an address in memory.

*Consider the following example, which prints the address of the variables defined*

```c
#include <stdio.h>

int main () {

   int  var1;
   char var2[10];

   printf("Address of var1 variable: %x\n", &var1  );
   printf("Address of var2 variable: %x\n", &var2  );

   return 0;
}
```

*When the above code is compiled and executed, it produces the following result*

```bash
Address of var1 variable: bff5a400
Address of var2 variable: bff5a3f6
```

The addresses are hexadecimal values which are use to locate a variable in the memory.

# What are Pointers?

- A pointer is a variable whose value is the address of another variable.

The general form of a pointer variable declaration is:

```sh
data-type *variable_name;
```

- Here, the data-type refers to the base data type which is generally a C language data-type.

Some of the valid examples of declaring a pointer are given below:

```c
int    *ip;    /* pointer to an integer */
double *dp;    /* pointer to a double */
float  *fp;    /* pointer to a float */
char   *ch     /* pointer to a character */
```

# Function Pointer in C

In C, like normal data pointers (int *, char *, etc), we can have pointers to functions. Following is a simple example that shows declaration and function call using function pointer.

```c
#include <stdio.h>

void hello(int a)
{
    printf("Value stored in a is %d\n", a);
}
  
int main()
{
    // hello_ptr is a pointer to function hello() 
    void (*hello_ptr)(int) = &hello;
  
    // Invoking hello() using hello_ptr
    (*hello_ptr)(50);
  
    return 0;
}
```

**Output:**

```bash
Value of a is 50
```

<h2>Some facts about function pointers.</h2>

- Unlike normal pointers, a function pointer points to code, not data. Typically a function pointer stores the start of executable code.

- Unlike normal pointers, we do not allocate de-allocate memory using function pointers.

- A function’s name can also be used to get functions’ address. For example, in the below program, we have removed address operator ‘&’ in assignment. We have also changed function call by removing *, the program still works.

```c
#include <stdio.h>

void hello(int a)
{
    printf("Value stored in a is %d\n", a);
}
  
int main()
{
    // hello_ptr is a pointer to function hello() 
    void (*hello_ptr)(int) = hello;
  
    // Invoking hello() using hello_ptr
    (hello_ptr)(50);
  
    return 0;
}
```

**Output:**

```bash
Value of a is 50
```

- Like normal pointers, we can have an array of function pointers.

- Function pointer can be used in place of switch case. For example, in below program, user is asked for a choice between 0 and 2 to do different tasks.

```c
#include <stdio.h>
void add(int a, int b)
{
    printf("Addition is %d\n", a+b);
}
void subtract(int a, int b)
{
    printf("Subtraction is %d\n", a-b);
}
void multiply(int a, int b)
{
    printf("Multiplication is %d\n", a*b);
}
  
int main()
{
    // fun_ptr_arr is an array of function pointers
    void (*fun_ptr_arr[])(int, int) = {add, subtract, multiply};
    unsigned int ch, a = 15, b = 10;
  
    printf("Enter Choice: 0 for add, 1 for subtract and 2 "
            "for multiply\n");
    scanf("%d", &ch);
  
    if (ch > 2) return 0;
  
    (*fun_ptr_arr[ch])(a, b);
  
    return 0;
}
```

**Output:**

```sh
Enter Choice: 0 for add, 1 for subtract and 2 for multiply
2
Multiplication is 150 
```

- Like normal data pointers, a function pointer can be passed as an argument and can also be returned from a function.
For example, consider the following C program where wrapper() receives a void fun() as parameter and calls the passed function.

```c
// A simple C program to show function pointers as parameter

#include <stdio.h>
  
// Two simple functions
void fun1()
{
    printf("Fun1\n");
}

void fun2()
{
    printf("Fun2\n");
}

// A function that receives a simple function
// as parameter and calls the function
void wrapper(void (*fun)())
{
    fun();
}
  
int main()
{
    wrapper(fun1);
    wrapper(fun2);
    return 0;
}
```

Output:

```bash
Fun1
Fun2
```

# Arrays
<br>
<span style="margin-left:150pt"><img src="https://cdn.programiz.com/sites/tutorial2program/files/c-arrays.jpg"></img></span>
<br>

- An array is a systematic arrangement of similar objects, usually in rows and columns.

- In C language, an array is a collection of similar data items stored at contiguous memory locations and elements can be accessed randomly using indices of an array.

- They can be used to store collection of primitive data types such as int, float, double, char, etc of any particular type.

The below code gives a simple idea of what arrays are:

```c
#include <stdio.h>
 
const int MAX = 3;
 
int main () {

   int  var[] = {10, 100, 200};
   int i;
 
   for (i = 0; i < MAX; i++) {
      printf("Value of var[%d] = %d\n", i, var[i] );
   }
   
   return 0;
}
```

When the above code is compiled and executed, it produces the following result:

```bash
Value of var[0] = 10
Value of var[1] = 100
Value of var[2] = 200
```

## Array of Pointers

- There may be a situation when we want to maintain an array, which can store pointers to an int or char or any other data type available. Following is the declaration of an array of pointers to an integer:

```c
int *ptr[MAX];
```

It declares **ptr** as an array of MAX integer pointers. Thus, each element in ptr, holds a pointer to an int value. The following example uses three integers, which are stored in an array of pointers, as follows:

```c
#include <stdio.h>
 
const int MAX = 3;
 
int main () {

   int  var[] = {10, 100, 200};
   int i, *ptr[MAX];
 
   for ( i = 0; i < MAX; i++) {
      ptr[i] = &var[i]; /* assign the address of integer. */
   }
   
   for ( i = 0; i < MAX; i++) {
      printf("Value of var[%d] = %d\n", i, *ptr[i] );
   }
   
   return 0;
}
```

When the above code is compiled and executed, it produces the following result:

```bash
Value of var[0] = 10
Value of var[1] = 100
Value of var[2] = 200
```
<b>Consider the following example:</b>

```c
#include <stdio.h>
int main() {
   int x[4];
   int i;

   for(i = 0; i < 4; ++i) {
      printf("&x[%d] = %p\n", i, &x[i]);
   }

   printf("Address of array x: %p", x);

   return 0;
}
```

**Output**

```bash
&x[0] = 1450734448
&x[1] = 1450734452
&x[2] = 1450734456
&x[3] = 1450734460
Address of array x: 1450734448
```

There is a difference of 4 bytes between two consecutive elements of array x. It is because the size of int is 4 bytes (on our compiler).<br>

Notice that, the address of &x[0] and x is the same. It’s because the variable name x points to the first element of the array.

<span style="padding:150pt"><img src="https://cdn.programiz.com/sites/tutorial2program/files/array-pointers.jpg"></span>

From the above example, it is clear that &x[0] is equivalent to x. And, x[0] is equivalent to *x.

Similarly,

- &x[1] is equivalent to x+1 and x[1] is equivalent to *(x+1).

- &x[2] is equivalent to x+2 and x[2] is equivalent to *(x+2).

- …

- Basically, &x[i] is equivalent to x+i and x[i] is equivalent to *(x+i).

## Difference between pointer to an array and array of pointers

Pointer to an array is also known as array pointer. We are using the pointer to access the components of the array.

```c
int a[3] = {3, 4, 5 }; 
int *ptr = a; 
```

We have a pointer ptr that focuses to the 0th component of the array. We can likewise declare a pointer that can point to whole array rather than just a single component of the array.

<b>Syntax:</b>

```sh
data type (*var name)[size of array];
```

Declaration of the pointer to an array:

```c
// pointer to an array of five numbers
 int (* ptr)[5] = NULL;     
```

The above declaration is the pointer to an array of five integers. We use parenthesis to pronounce pointer to an array. Since subscript has higher priority than indirection, it is crucial to encase the indirection operator and pointer name inside brackets.

<b>Example:</b>

```c
// C program to demonstrate
// pointer to an array.
  
#include <stdio.h>
  
int main()
{
  
    // Pointer to an array of five numbers
    int(*a)[5];
  
    int b[5] = { 1, 2, 3, 4, 5 };
  
    int i = 0;
  
    // Points to the whole array b
  
    a = &b;
  
    for (i = 0; i < 5; i++)
  
        printf("%d\n", *(*a + i));
  
    return 0;
}
```

**Output:**

```sh
1
2
3
4
5
```

“Array of pointers” is an array of the pointer variables. It is also known as pointer arrays.

**Syntax:**

```c
int *var_name[array_size];
```

**Declaration of an array of pointers:**

```c
 int *ptr[3];
```

We can make separate pointer variables which can point to the different values or we can make one integer array of pointers that can point to all the values.

**Example:**

```c
// C program to demonstrate
// example of array of pointers.
  
#include <stdio.h>
  
const int SIZE = 3;
  
void main()
{
  
    // creating an array
    int arr[] = { 1, 2, 3 };
  
    // we can make an integer pointer array to
    // storing the address of array elements
    int i, *ptr[SIZE];
  
    for (i = 0; i < SIZE; i++) {
  
        // assigning the address of integer.
        ptr[i] = &arr[i];
    }
  
    // printing values using pointer
    for (i = 0; i < SIZE; i++) {
  
        printf("Value of arr[%d] = %d\n", i, *ptr[i]);
    }
}
```

**Output:**

```sh
Value of arr[0] = 1
Value of arr[1] = 2
Value of arr[2] = 3
```

**Example:** We can likewise make an array of pointers to the character to store a list of strings.

```c
#include <stdio.h>
  
const int size = 4;
  
void main()
{
  
    // array of pointers to a character
    // to store a list of strings
    char* names[] = {
        "Akshay",
        "Harsh",
        "Arnav",
        "Tarun"
    };
  
    int i = 0;
  
    for (i = 0; i < size; i++) {
        printf("%s\n", names[i]);
    }
}
```

**Output:**

```sh
Akshay
Harsh
Arnav
Tarun
```
