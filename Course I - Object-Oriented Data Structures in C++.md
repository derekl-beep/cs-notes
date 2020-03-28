# 1 - Writing a C++ Program

## Some Basics concepts
- In C++ a function declared with type `void` does not return a value.
- Every variable in C++ has to be associated with a specific type.
- When you write a C++ program, the program begins when the operating system calls the function `main()`.
- A class can consist of multiple member data variables of different types, but each type must be specified when the class is defined.
- The member functions of a class always have access to every member data variable of that class.

## Making Comments in C++

Single-line comments with `//`
```c
int x = 2; // A single-line comment can appear at the end of a line.

// Single-line comments can also appear by themselves on a line.
```
Multi-line comments with `/* */`
```c
int x = 2;

/* This is a multi-line comment.
   It will continue for as many lines as necessary
   until it's closed with the closing marker. */

int y = 3;
```

## If-else

Basic structure:
```c++
if (condition) {
    // true case
}
else {
    // false case
}
```
If-else combination 1:
```c++
if (condition1) {
    
}
else if (condition2) {
    
}
else if (condition3) {
    
}
else {
    // If none of the other conditions were met...
}
```
If-else combination 2:
```c
int x = 100;
if (x > 0) {
    // This will execute
}
if (x > 10) {
    // This will execute
}
if (x > 50) {
    // This will execute
}
else {
    // This is the only section that won't execute!
}
```
### ternary operator
You should also be aware of the strange-looking "ternary operator," also called the "conditional operator," which is actually a combination of two operators, "?" and ":" (question mark and colon). The basic format for this syntax is:

[Boolean-valued condition] ? [expression to evaluate if true] : [expression to evaluate if false]

```c
// Since (5<10) is true, the expression before the colon will be selected, which is 1.
int x = 5 < 10 ? 1 : 2;
// Now x is equal to 1.

// Note, the following syntax is NOT allowed in C++, which is why the ternary operator can be useful in these cases:
int y = if (5<10) {1;} else {2;}
```

## Comparison Operators and Arithmetic Operators
```c
#include <iostream>

int main() {
  if (3 <= 4) {
    std::cout << "3 is less than or equal to 4" << std::endl;
  }
  
  int x = 3;
  x += 2; // This increases x by 2. It's the same as writing: x = x + 2;
  std::cout << "x should be 5 now: " << x << std::endl;
  
  return 0;
}
```
```
3 is less than or equal to 4
x should be 5 now: 5
```

## Type Casting

An important concept to understand in C++ is "casting." This is the phenomenon where a value is automatically converted to a different type in order to allow an operation to continue. For example, if you try to add together a floating point **double** value and an integer **int** value, the int will be converted to double first, and then the result of the addition will have type double as well. But if you save a double value to an int variable, the floating point value will be truncated to an integer! For example:

```c
#include <iostream>
int main() {
  int x = 2;
  double y = 3.5;
  std::cout << "This result will be a double with value 5.5: " << (x+y) << std::endl;
  
  int z = x+y; // This expression is calculated as a double, but then it's cast back to int!
  std::cout << "This result will be an int with value 5: " << z << std::endl;
  return 0;
}
```
```
This result will be a double with value 5.5: 5.5
This result will be an int with value 5: 5
```

It's also the case that various values can be cast to the Boolean  **bool** type. So, they can be used as a condition. For example, usually, nonzero numeric values will be considered  **true**, and zero will be considered  **false**.
```c
#include <iostream>
int main() {
  if (0) {
    std::cout << "You won't see this text." << std::endl;
  }
  if (-1) {
    std::cout << "You WILL see this text!" << std::endl;
  }
  return 0;
}
```
```
You WILL see this text!
```

You need to be aware that casts are happening invisibly in your code! Sometimes this can cause hard-to-find bugs. If you want to read more details about the casting operation, especially if you are curious about a debugging situation later, see these references:

A more detailed primer on the casting topic:  [http://www.cplusplus.com/doc/tutorial/typecasting/](http://www.cplusplus.com/doc/tutorial/typecasting/ "C++ Tutorial: Type casting")

In-depth documentation:  [https://en.cppreference.com/w/cpp/language/implicit_conversion](https://en.cppreference.com/w/cpp/language/implicit_conversion "Implicit Conversions")

## Block Scope

After viewing the lecture about stack memory, you should be already have an intuitive idea about how  **block scope**  works. The idea is that certain blocks of code, signified by  **{ }**, create an inner stack on top of the previous stack, which can hide the pre-existing values. The lifetime of stack variables inside a block is called the variable's  **scope**. Variables created on the stack inside the inner block are only in existence for the duration of the block. When the block ends, the inner stack is removed, and the pre-existing values in the outer scope are available again (because they are still in scope!).

Here is an example:

```c
#include <iostream>
int main() {
  
  // You can actually make an inner scope block anywhere in a function.
  // Let's do it to show how scope works.
  
  // In the initial, outer scope:
  int x = 2;
  std::cout << "Outer scope value of x (should be 2): " << x << std::endl;
  
  // Create an inner scope and make a new variable with the name "x".
  // This is not an error! We can redeclare x because of the inner scope.
  // Also, make an extra variable named "y".
  {
    int x = 3;
    int y = 4;
    std::cout << "Inner scope vaue of x (should be 3): " << x << std::endl;
    std::cout << "Inner scope vaue of y (should be 4): " << y << std::endl;
  }
  
  // Now that the inner block has closed, the inner x and y are gone.
  // The original x variable is still on the stack, and it has its old value:
  std::cout << "Outer scope value of x (should be 2): " << x << std::endl;
  
  // We can't refer to y here, because it doesn't exist in this scope at all!
  // If you un-comment this line, there will be a compile error.
  // std::cout << "This line causes an error because y doesn't exist: " << y << std::endl;
  
  return 0;
}
```
```
Outer scope value of x (should be 2): 2 
Inner scope vaue of x (should be 3): 3 
Inner scope vaue of y (should be 4): 4 
Outer scope value of x (should be 2): 2
```

Some keywords like **if** can have a block in { } afterwards, which does create an inner block scope for the duration of the conditional block:
```c
#include <iostream>
int main() {
  int x = 2;
  std::cout << "Outer scope value of x (should be 2): " << x << std::endl;
  
  if (true) {
    int x = 3;
    std::cout << "Inner scope vaue of x (should be 3): " << x << std::endl;
  }

  std::cout << "Outer scope value of x (should be 2): " << x << std::endl;

  return 0;
}
```
```
Outer scope value of x (should be 2): 2
Inner scope vaue of x (should be 3): 3 
Outer scope value of x (should be 2): 2
```

### for loops

The  **for** loop is a common loop type that lets you specify an iteration variable, a range for that variable, and an increment instruction. The syntax is:

**for (** **_declaration_** **;** **_condition_** **;** **_increment operation_** **) {** **_loop body_** **}**

Be careful about whether you are redeclaring the iteration variable at block scope or not! Here's an example:
```c
#include <iostream>
int main() {
  
  // outer scope version of "x" to show the for-loop block scoping
  int x = -1;
  
  std::cout << "[Outside the loop] x is now (should be -1): " << x << std::endl;
  
  // The for loop lets us declare a variable in the first part of the
  // loop statement, which will belong to the inner block scope:
  for (int x = 0; x <= 2; x++) {
    std::cout << "[Inside the loop] x is now: " << x << std::endl;
  }
  
  // The outer scope x is still -1
  std::cout << "[Outside the loop] x is now (should be -1): " << x << std::endl;
  
  // This version doesn't redeclare x, so it just inherits access to the
  // same x variable from the outer scope. This modifies the outer x directly!
  for (x = 0; x <= 2; x++) {
    std::cout << "[Inside the loop] x is now: " << x << std::endl;
  }
  
  // In the last iteration where the condition x<=2 was true, x had the value 2.
  // After that iteration, x was incremented one more time and became 3.
  // Then the condition was false and the loop body did not execute.
  // Afterwards, the outer scope x is still 3 because the loop modified it.
  std::cout << "[Outside the loop] x is now (should be 3): " << x << std::endl;
  
  return 0;
}
```

```
[Outside the loop] x is now (should be -1): -1
[Inside the loop] x is now: 0 
[Inside the loop] x is now: 1 
[Inside the loop] x is now: 2 
[Outside the loop] x is now (should be -1): -1 
[Inside the loop] x is now: 0 
[Inside the loop] x is now: 1 
[Inside the loop] x is now: 2 
[Outside the loop] x is now (should be 3): 3
```

### while loops

Another loop is the simple  **while**  loop, which has this syntax:

**while (** **_condition_** **) {** **_loop body_** **}**

```c
#include <iostream>
int main() {
  int x = 0;
  std::cout << "This should show 0, 1, 2, 3:" << std::endl;
  while (x <= 3) {
    std::cout << "x is now: " << x << std::endl;
    x++; // increment x by 1
  }
  return 0;
}
```
```
This should show 0, 1, 2, 3: 
x is now: 0 
x is now: 1 
x is now: 2 
x is now: 3
```

### Preview: Modern "range-based" for loops

You might see another very common type of  **for**  loop in recent C++ code, that has this syntax:

**for (** **_temporary variable declaration_** **:** **_container_** **) {** **_loop body_** **}**

We'll wait to talk more about that in a later reading lesson.



## Declaring a Class

```c++
#include  <iostream>

// You should define Pair here:
// (Use as many lines as you need!)
class Pair {
  public:
    int a, b;
    int sum() {return a + b;}
};

// This main() function will help you test your work.
// Click Run to see what happens.
// When you're sure you're finished, click Submit for grading
// with our additional hidden tests.
int main() {
  Pair p;
  p.a = 100;
  p.b = 200;
  if (p.a + p.b == p.sum()) {
    std::cout << "Success!" << std::endl;
  } else {
    std::cout << "p.sum() returns " << p.sum() << " instead of " << (p.a + p.b) << std::endl;
  }
  return 0;
}
```


# 2 - Understanding the C++ Memory Model

## Key Concepts

-   Pointers and dereferencing
-   Local (stack) memory
-   Allocated (heap) memory

Every C++ variable has four things:
- A name
- A type
- A value
- A location in memory (= memory address)

Example: ` int primeNumber = 7 `

To retrieve the memory address, we can use `&` operator:
```c++
#include <iostream>
int main() {
	int num = 7;
	
	std::cout << "Value: " << num << std::endl;
	std::cout << "Address: " << &num << std::endl;
	
	return 0;
}
```
Output:
```bash
Value: 7
Address: 0x7ffcd9a4c224
```

## Stack Memory
By default, every variable in C++ is place in **stack memory**.

Stack memory is associated with the **current function** and the memory's life-cycle is tied to the function:
- When the function returns / ends, the stack memory of that function is released.

Stack memory always starts from high address (e.g. `0xffff00f0`) and grows down towards `0`.


```c++
#include  <iostream>

void  foo() {
	int x = 42;
	std::cout << " x in foo(): " << x << std::endl;
	std::cout << "&x in foo(): " << &x << std:: endl;
}

int  main() {
	int num = 7;
	std::cout << " num in main(): " << num << std::endl;
	std::cout << "&num in main(): " << &num << std::endl;

	foo();
	return  0;
}
```
Expected:
- the memory address of `num` in `main()` is larger than that of `x` in `foo()` because the former is allocated first in the program.

Output
```
 num in main(): 7
&num in main(): 0x7ffdefd85b74
 x in foo(): 42
&x in foo(): 0x7ffdefd85b54
```

## Pointer
A point is a variable that stores the memory address of the data.
- Simply put: pointers are a level of indirection from the data

In C++, a pointer is define by adding an `*` to the type of the variable.
- Integer pointer: `int * p = &num;`

## Dereference Operator
Given a pointer, a level of indirection can be remove with the dereference operator `*`
```c++
int num = 7;
int * p = &num;		// store the memory address of num in a pointer
int value_in_num = *p;	// retrieve the value from a pointer
*p = 42;	// change the value of num with its pointer
```

```c++
/**
 * C++ program printing various memory values with references and pointers.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

int main() {
  int num = 7;
  std::cout << " num: " <<  num << std::endl;
  std::cout << "&num: " << &num << std::endl;

  int *p = &num;
  std::cout << " p: " <<  p << std::endl;
  std::cout << "&p: " << &p << std::endl;
  std::cout << "*p: " << *p << std::endl;

  *p = 42;
  std::cout << "*p changed to 42" << std::endl; 
  std::cout << " num: " <<  num << std::endl;

  return 0;
}
```
**Output:**
```
 num: 7
&num: 0x7fff6f060a9c
 p: 0x7fff6f060a9c
&p: 0x7fff6f060a90
*p: 7
*p changed to 42
 num: 42
```

## Heap Memory
Heap memory allows us to create memory **independent** of the life-cycle of a function.

If memory needs to exist for longer than the life-cycle of the function, we must use **heap memory**.
- The ***only*** way to create heap memory in C++ is with the `new` operator.
It returns a **pointer** to the memory storing the data - ***not*** an instance of the data itself.

The code below allocates two chunks of memory:
- Memory to store an **integer pointer** on the **stack**
- Memory to store an **integer** on the **heap**
```c++
int * numPtr = new int;
```

```c++
/**
 * C++ program printing various memory values using heap-allocated memory.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

int main() {
  int *numPtr = new int;

  std::cout << "*numPtr: " << *numPtr << std::endl;
  std::cout << " numPtr: " <<  numPtr << std::endl;
  std::cout << "&numPtr: " << &numPtr << std::endl;

  *numPtr = 42;
  std::cout << "*numPtr assigned 42." << std::endl;

  std::cout << "*numPtr: " << *numPtr << std::endl;
  std::cout << " numPtr: " <<  numPtr << std::endl;
  std::cout << "&numPtr: " << &numPtr << std::endl;

  return 0;
}
```

```
*numPtr: 0
 numPtr: 0xcefc20
&numPtr: 0x7ffc0441d358
*numPtr assigned 42.
*numPtr: 42
 numPtr: 0xcefc20
&numPtr: 0x7ffc0441d358
```


### C++'s New Operator
The `new` operator in C++ will always do three things:
1. Allocate memory on the heap for the data structure
2. Initialize the data structure
3. Return a pointer to the start of the data structure

The memory is only ever reclaimed by the system when the pointer is passed to the `delete` operator.

### Null Pointer (nullptr)
The C++ keyword `nullptr` is a pointer that points to the memory address `0x0`.
- `nullptr` represents a pointer to "nowhere"
- Address `0x0` is reserved and never used by the system
- Address `0x0` will always generate an "segmentation fault" when accessed.
- Calls to `delete 0x0` are ignored

### Arrow Operator (->)
When an object is stored via a pointer, access can be made to member functions using the `->` operator:
```c++
c->getVolume();
// is the same as
(*c).getVolume();
```

### Heap Memory Puzzles

#### Puzzle 1
```c++
#include <iostream>

using std::cout;
using std::endl;

int main() {
  int  i =  2,  j =  4,  k =  8;
  int *p = &i, *q = &j, *r = &k;

  k = i;
  cout << i << j << k << *p << *q << *r << endl;

  p = q;
  cout << i << j << k << *p << *q << *r << endl;

  *q = *r;
  cout << i << j << k << *p << *q << *r << endl;

  return 0;
}
```
Output:
```
242242
242442
222222
```


#### Puzzle 2
```c++
/**
 * C++ puzzle program.  Try to figure out the result before running!
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

using std::cout;
using std::endl;

int main() {
  int *x = new int;
  int &y = *x;
  y = 4;

  cout << &x << endl;
  cout << x << endl;
  cout << *x << endl;

  cout << &y << endl;
  cout << y << endl;
  // This line gives a compiling error
  // cout << *y << endl;

  return 0;
}
```
Output
```
0x7ffd87706000
0x20ddc20
4
0x20ddc20
4
```


#### Puzzle 3

```c++
/**
 * C++ puzzle program.  Try to figure out the result before running!
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

using std::cout;
using std::endl;

int main() {
  int *p, *q;
  p = new int;
  q = p;
  *q = 8;
  cout << *p << endl;

  q = new int;
  *q = 9;
  cout << *p << endl;
  cout << *q << endl;

  return 0;
}
```
Output
```
8
8
9
```

#### Puzzle 4

```c
/**
 * C++ puzzle program.  Try to figure out the result before running!
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>

using std::cout;
using std::endl;

int main() {
  int *x;
  int size = 3;
  x = new int[size];

  for (int i = 0; i < size; i++) {
    x[i] = i + 3;
  }

  delete[] x;
}
```

## Headers and Source Files in C++
`.h` files are "header files". These usually have the definitions of objects and declarations of global functions. 
```c
/**
 * Simple C++ class for representing a Cube.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

// All header (.h) files start with "#pragma once":
#pragma once

// A class is defined with the `class` keyword, the name
// of the class, curly braces, and a required semicolon
// at the end:
class Cube {
  public:  // Public members:
    double getVolume();
    double getSurfaceArea();
    void setLength(double length);

  private: // Private members:
    double length_;
};
```
`#` are special commands for the compiler, called pre-processor directives.

`#pragma once` prevents the header file from being automatically included multiple times in a complex project, which could cause errors.

Only the signature of the function is given, to declare its input argument types and return type. Instead, the function will be defined in the `.cpp` source code file.





`.cpp` files are often called the implementation files, or simply the "source files". This is where most function definitions and main program logic go.
```c++
/**
 * Simple C++ class for representing a Cube.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include "Cube.h"

double Cube::getVolume() {
  return length_ * length_ * length_;
}

double Cube::getSurfaceArea() {
  return 6 * length_ * length_;
}

void Cube::setLength(double length) {
  length_ = length;
}
```
`#include "Cube.h"` includes all the text from the `Cube.h` file in the same directory.

The `main.cpp` file

```c
/**
 * C++ code for creating a Cube of length 2.4 units.
 * - See ../cpp-std/main.cpp for a similar program with print statements.
 * 
 * @author
 *   Wade Fagen-Ulmschneider <waf@illinois.edu>
 */

#include <iostream>
#include "Cube.h"

int main() {
  Cube c;

  c.setLength(3.48);
  double volume = c.getVolume();
  std::cout << "Volume: " << volume << std::endl;

  return 0;
}
```
When you write `#include <iostream>`, the compiler will look for the `iostream` header file in a system-wide library path that is located outside of your current directory.

You shouldn't use `#include` to literally include one `.cpp` file in another, because the function definitions in the `.cpp` file will be compiled separately and then linked to the code from the `main.cpp` file.

![How a C++ compiler works](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/WWEDqDMkEemplgpfqc6zSA_81f646b7ba6aa3a7d1e2ae99397b5f25_compilation_chart_lo-res.png?expiry=1583798400000&hmac=IFG4N6TjG08zA8wy6CaCYVEe6xLAV83wBpbaIntBLC4)

## Week 2 Quiz Remarks
### Question 1
```c
int *i;
i = new  int;
*i = 0;
```
```
 i: 0x55a50d9feeb0
&i: 0x7ffe33f66180
*i: 0
```
The variable type is a pointer to an integer, `int *`.
The type of a pointer includes the type of the value in the memory location that it is pointing to.

Even though `p` points to a memory address containing the integer value 0, **the value of the pointer is the memory address itself**.

### Question 3
Suppose we are writing the following function that is intended to return a pointer to a location in memory holding an integer value initialized to zero.
How should variable `i` be declared?
```c
int *allocate_an_integer() {
    // declare variable i here
    int * i = new int;
    *i = 0;
    return i;
}
```
The variable `i` should be a pointer to a memory location to an integer allocated from the heap so the **memory location continues to be allocated** after the function has returned.

### Question 4

Suppose we have this alternative function that returns a pointer to a memory location to an integer value of zero.

```c
int *allocate_an_integer() {
    int i = 0;
    return &i;
}

int main() {
    int *j;
    j = allocate_an_integer();
    int k = *j;
    return 0;
}
```
What value is variable k assigned and why?

Variable `i` is allocated with a memory location on the **stack**. When `allocate_an_integer()` returns, its memory on the **stack** including the memory holding the value of `i` is **freed** and may be used for other purposes, and may be overwritten with a new value.

### Question 8
`j` is a direct reference to the same actual integer that `i` points to indirectly.
```c
int *i = new int;
*i = 0;
int &j = *i;
j++;
```
```
 i: 0x558761750eb0
&i: 0x7fff4980a658
*i: 1
 j: 1
&j: 0x558761750eb0
```

## Week 2 Challenge
Create a function that returns a pointer to an instance on the heap.

```c
#include <iostream>

// This class Pair has already been defined for you.
// (You may not change this definition.)
class Pair {
public:
  int first, second;
  void check() {
    first = 5;
    std::cout << "Congratulations! The check() method of the Pair class \n has executed. (But, this isn't enough to guarantee \n that your code is correct.)" << std::endl;
  }
};

// Insert your declaration and implementation of the function pairFactory()
// below, by replacing "..." with proper C++ code. Be sure to declare the
// function type to return a pointer to a Pair.

Pair *pairFactory() {
    Pair *p = new Pair;
  return p;
}

// Your function should be able to satisfy the tests below. You should try
// some other things to convince yourself. If you have a bug in this problem,
// the usual symptom is that after you submit, the grader will crash with a
// system error. :-)
int main() {

  Pair *p;
  p = pairFactory();
  
  // This function call should work without crashing:
  p->check();
  
  // Deallocating the heap memory. (Assuming it was made on the heap!)
  delete p;

  std::cout << "If you can see this text, the system hasn't crashed yet!" << std::endl;  

  return 0;
}
```

# 3 - Developing C++ Classes

## Key Concepts

-   Constructors and destructors
-   Methods and operators
-   Access through pointers and references

## Class Constructors

### Automatic Default Constructor
If we do not provide any custom constructors, the C++ compiler provides an **automatic default constructor** for our class.
The automatic default constructor will only initialize all member variables to their **default values**.

If **any** custom constructor is defined, an automatic default constructor is **not** defined.


### Custom Default Constructor
The simplest constructor we can provide is a **custom default constructor** that specifies the state of the object when the object is constructed. 
We define one by creating:
- A member function with the **same name of the class**
- The function takes **zero parameters**.
- The function **does not have a return type.**
```c
Cube::Cube() // custom default constructor
```
Inside the header file `Cube.h`, the code should look like:

```c++
#pragma once

namespace uiuc {
	class Cube{
		public:
			Cube();	// Custom default constructor
			
			double getVolume();
			double getSurfaceArea();
			void setLength(double length);
		
		private:
			double length_;
	};
}
```

The implementation file `Cube.cpp` looks like:
```c
#include "Cube.h"

namespace uiuc {
	Cube::Cube() {
		length_ = 1;
	}
}
```

The `main` function looks like:
```c
#include "Cube.h"
#include <iostream>

int main() {
	uiuc::Cube c;
	std::cout << "Volume: " << c.getVolume() << std::endl;
	return 0;
}
``` 
```
Volume: 1
```

### Custom Constructors
We can also specify custom, non-default constructors that require client code to supply arguments:
```c
Cube::Cube(double length)
// one-argument ctor specifying initial length
```

Inside the header file `Cube.h`, the code should look like:

```c++
#pragma once

namespace uiuc {
	class Cube{
		public:
			Cube();	// Custom default constructor
			Cube(double length); // One-argument constructor
			
			double getVolume();
			double getSurfaceArea();
			void setLength(double length);
		
		private:
			double length_;
	};
}
```
The implementation file `Cube.cpp` looks like:
```c
#include "Cube.h"

namespace uiuc {
	Cube::Cube() {
		length_ = 1;
	}
	Cube::Cube(double length){
		length_ = length;
	}
}
...
```
The `main` function looks like:
```c
#include "Cube.h"
#include <iostream>

int main() {
	uiuc::Cube c(2);
	std::cout << "Volume: " << c.getVolume() << std::endl;
	return 0;
}
``` 
```
Volume: 8
```


## Copy Constructors

In C++, a **copy constructor** is a special constructor that exists to make a copy of any existing **object**.


### Automatic Copy Constructor
If we do not provide a custom copy constructor, the C++ compiler provides an **automatic copy constructor** for our class.

The automatic copy constructor will copy the contents of all member variables.


### Custom Copy Constructor
A custom copy constructor is:
- A class constructor
- Has exactly one argument
	- The argument must be constant reference of the same type as the class.
```c
Cube::Cube(const Cube & obj)
```
The implementation file `Cube.cpp` looks like:
```c
#include "Cube.h"

namespace uiuc {
	// Custome constructor
	Cube::Cube() {
		length_ = 1;
	}
	// Custome copy constructor
	Cube::Cube(const Cube & obj){
		length_ = obj.length;
	}
}
...
```

### Copy Constructor Invocation
Often, copy constructors are invoked automatically:
- Passing an object as a parameter (by value)
- Returning an object from a function (by value)
- Initializing a new object

#### Example 1
The implementation file `Cube.cpp` looks like:
```c
#include "Cube.h"
#include <iostream>

namespace uiuc {
	// Custome constructor
	Cube::Cube() {
		length_ = 1;
		std::cout << "Default constructor invoked!" << std::endl;
	}
	// Custome copy constructor
	Cube::Cube(const Cube & obj){
		length_ = obj.length;
		std::cout << "Copy constructor invoked!" << std::endl;
	}
}
...
```
The `main.cpp` looks like:
```c
#include "Cube.h"
using uiuc::Cube;

void foo(Cube cube){
	// Nothing
}

int main() {
	Cube c;
	foo(c);

	return 0;
}
```
```
Default constructor invoked!
Copy constructor invoked!
```
#### Example 2

The `main.cpp` looks like:
```c
#include "../Cube.h"
using uiuc::Cube;

Cube foo(){
	Cube c;
	return c;
}

int main() {
	Cube c2 = foo();
	return 0;
}
```
```
Default constructor invoked!
Copy constructor invoked!
Copy constructor invoked!
```
![enter image description here](https://i.imgur.com/618MNlS.png)

#### Example 3
The `main.cpp` looks like:
```c
#include "../Cube.h"
using uiuc::Cube;

int main() {
	Cube c;
	Cube myCube = c;
	
	return 0;
}
```
```
Default constructor invoked!
Copy constructor invoked!
```

#### Example 4
The `main.cpp` looks like:
```c
#include "../Cube.h"
using uiuc::Cube;

int main() {
	Cube c;
	Cube myCube;
	
	// The following is an assignment, not a construction of object
	myCube = c;
	
	return 0;
}
```
```
Default constructor invoked!
Default constructor invoked!
```

## Copy Assignment Operator

In C++, a **copy assignment operator** defines the behavior when an object is copied using the assignment operator `=`.

### Copy Constructor vs. Assignment 
A copy constructor **creates a new object** (constructor).

An assignment operator assigns a **value to an existing object**.
- An assignment operator is always called on an object that has already been constructed.

An object can only be created once. To change an object that has been created, we need to use assignment.

### Automatic Assignment Operator
If an assignment operator is not provided, the C++ compile provides an automatic assignment operator.

The automatic assignment operator will copy the contents of all member variables.

### Custom Assignment Operator
A custom assignment operator:
- Is a public member function of the class
- Has the function name `operator=`
- Has a return value of a reference of the class' type
- Has exactly one argument
	- The argument must be const reference of the class' type

```c
Cube & Cube::operator=(constr Cube & obj)
``` 

The implementation file `Cube.cpp` looks like:
```c++
#include "Cube.h"
#include <iostream>

namespace uiuc {

	// Custome constructor
	Cube::Cube() {
		length_ = 1;
		std::cout << "Default constructor invoked!" << std::endl;
	}
	
	// Custome copy constructor
	Cube::Cube(const Cube & obj){
		length_ = obj.length;
		std::cout << "Copy constructor invoked!" << std::endl;
	}
	
	// Custom assignment operator
	Cube & Cube::operator=(const Cube & obj){
		length_ = obj.length;
		std::cout << "Assignment operator invoked!" << std::endl;
		// Always return a dereference value of this
		// This is the instance of the class itself
		return *this;
	}
}
...
```
#### Example 1
```c
#include "Cube.h"
using uiuc::Cube;

int main() {
	Cube c;
	Cube myCube;

	myCube = C;

	return 0;
}
```
```
Default constructor invoked!
Default constructor invoked!
Assignment operator invoked!
```
So there's a small nuanced difference b/w a copy constructor and an assignment operator.
Their functionality is largely the same, that their job is to copy the contents of one instance of a class to another. 
The invocation of an assignment operator means the object already exists and doesn't need constructed.

## Variable Storage
In C++, an instance of a variable can be stored directly in memory, accessed by a pointer, **or** accessed by a reference.

![enter image description here](https://i.imgur.com/2Fs61xF.png)

### Direct Storage
By default, variables are stored directly in memory.
- The **type** of a variable has no modifiers.
- The object takes up exactly its size in memory.
```c
Cube c;	// Stores a Cube in memory
int i;	// Stores an integer in memory
uiuc::HLSAPixel p;	// Stores a pixel in memory
```

### Storage by Pointer
- The **type** of a variable is modified with an asterisk `*`
- A pointer takes a "memory address width" of memory (ex: 64 bits on a 64-bit system)
- The pointer "points" to the allocated space of the object
```c
Cube *c	// Pointer to a Cube in memory
int *i	// Pointer to an integer in memory
uiuc::HSLAPixel *p	// Pointer to a pixel in memory
```
### Storage by Reference
- A reference is an **alias** to existing memory and is denoted in the type with an ampersand `&`.
- A reference **does not store memory** itself, it is only an alias to another variable.
- It takes zero memory.
- The alias must be assigned when the variable is initialized.
```c
Cube &c = cube;	// Alias to the variable 'cube'	
int &i = count;	// Alias to the varible 'i'
uiuc::HSLAPixel &p;	//Illegal! must alias sth when variable is initialized.
```
![enter image description here](https://i.imgur.com/jSsadjY.png)

The implementation file `Cube.cpp` looks like:
```c++
#include "Cube.h"
#include <iostream>

namespace uiuc {

	// Custom one-parameter constructor
	Cube::Cube(double length) {
		length_ = length;
		std::cout << "Created $" << getVolume() << std::endl;
	}
	
	// Custom copy constructor
	Cube::Cube(const Cube & obj){
		length_ = obj.length_;
		std::cout << "Created $" << getVolume() << " via copy" << std::endl;
	}
	
	// Custom assignment operator
	Cube & Cube::operator=(const Cube & obj){
		length_ = obj.length_;
		std::cout << "Transformed $" << getVolume() << "-> $" << obj.getVolume() << std::endl;
		return *this;
	}
}
...
```
In computer science, instead of creating $$, these three operations create extra memories.

#### Example 1 - by value
```c
int main() {
	// Create a 1,000-valued cube
	Cube c(10);
	// Transfer the cube
	Cube myCube = c;
	return 0;
}
```
```
Created $1000
Created $1000 via copy
```

![enter image description here](https://imgur.com/MWi5hk3.png)

#### Example 2 - by reference
```c
int main() {
	// Create a 1,000-valued cube
	Cube c(10);
	// Transfer the cube
	Cube & myCube = c;
	return 0;
}
```
```
Created $1000
```
![enter image description here](https://imgur.com/ihGbDOe.png)

#### Example 3 - by pointer
```c
int main() {
	// Create a 1,000-valued cube
	Cube c(10);
	// Transfer the cube
	Cube * myCube = &c;
	return 0;
}
```
```
Created $1000
```
![enter image description here](https://imgur.com/lyvx5ir.png)


### Pass by ______
Identical to storage, arguments can be passed to functions in three different ways:
- Pass by value (default)
- Pass by pointer (modified with `*`)
- Pass by reference (modified with `&`, acts as an alias)


#### Example 1 - by value
```c
bool sendCube(Cube c) {
	// ... logic to send a Cube somewhere ,,,
	return True;
}

int main() {
	// Create a 1,000-valued cube
	Cube c(10);
	
	// Send the cube to someone
	sendCube(c);
	
	return 0;
}
```
```
Created $1,000
Created $1,000 via copy
```
![enter image description here](https://imgur.com/6xhJBnM.png)

#### Example 2 - by reference
```c
bool sendCube(Cube & c) {
	// ... logic to send a Cube somewhere ,,,
	return True;
}

int main() {
	// Create a 1,000-valued cube
	Cube c(10);
	
	// Send the cube to someone
	sendCube(c);
	
	return 0;
}
```
```
Created $1,000
```
![enter image description here](https://imgur.com/y2iYg5u.png)




#### Example 3 - by pointer
```c
bool sendCube(Cube * c) {
	// ... logic to send a Cube somewhere ,,,
	return True;
}

int main() {
	// Create a 1,000-valued cube
	Cube c(10);
	
	// Send the cube to someone
	sendCube(&c);
	
	return 0;
}
```
```
Created $1,000
```
![enter image description here](https://imgur.com/BY2nfE5.png)

### Return by ______
Similarly, values can be returned all three ways as well:
- Return by **value** (default)
- Return by **pointer** (modified with `*`)
- Return by **reference** (modified with `&`, acts as an alias)
	- Never return a reference to a stack variable created on the stack of your current function!

## Class Destructor

When an instance of a class is cleaned up, the **class destructor** is the last call in a class's life-cycle.

An destructor should __never__ be called directly. Instead, it is automatically called when the object's memory is being reclaimed by the system:
- If the object is on the **stack**, when the function returns
- If the object is on the **heap**, when `delete` is used

### Automatic Default Destructor
An **automatic default destructor** is added to your class if no other destructor is defined.
The only action of the automatic default destructuor is to call the default destructor of all member objects.

### Custom Destructor
To add custom behavior to the end-of-life of the function, a custom destructor can be defined as:
- A custom destructor is a member function.
- The function's destructor is the name of the class, preceded by a tilde `~`.
- All destructors have zero arguments and no return type.
```c
Cube::~Cube();	// Cutom destructor
```

A custom destructor is essential when an object allocates an external resource that must be closed or freed when the object is destroyed. Examples:
- Heap memory
- Open files
- Shared memory


The implementation file `Cube.cpp` looks like:
```c++
#include "Cube.h"
#include <iostream>
using namespace std;

namespace uiuc {
	// Default constructor
	Cube::Cube() {
	cout << "Created $1 (default)" << endl;
	}
	
	// Custom one-parameter constructor
	Cube::Cube(double length) {
		length_ = length;
		cout << "Created $" << getVolume() << endl;
	}
	
	// Custom copy constructor
	Cube::Cube(const Cube & obj){
		length_ = obj.length_;
		cout << "Created $" << getVolume() << " via copy" << endl;
	}

	// Custom destructor
	Cube::~Cube() {
	cout << "Destoryed $" << getVolume() << endl;
	}
	
	// Custom assignment operator
	Cube & Cube::operator=(const Cube & obj){
		length_ = obj.length_;
		cout << "Transformed $" << getVolume() << "-> $" << obj.getVolume() << endl;
		return *this;
	}
}
...
```

#### Example 1
```c
double cube_on_stack() {
	Cube c(3);
	return getVolume();
}

void cube_on_heap() {
	Cube * c1 = new Cube(10);
	Cube * c2 = new Cube;
	delete c1;
}

int main() {
	cube_on_stack();
	cube_on_heap();
	cube_on_stack();
	return 0;
}
```
```
Created $27
Destoryed $27
Created $1000
Created $1 (default)
Destoryed $1000
Created $27
Destoryed $27
```

## C++ Syntax Notes

1.  Uninitialized Pointers, Segfaults, and Undefined Behavior
[https://www.coursera.org/learn/cs-fundamentals-1/supplement/lIrXl/c-syntax-notes-uninitialized-pointers-segfaults-and-undefined-behavior](https://www.coursera.org/learn/cs-fundamentals-1/supplement/lIrXl/c-syntax-notes-uninitialized-pointers-segfaults-and-undefined-behavior)

2. The Modern Range-Based "for" Loop
[https://www.coursera.org/learn/cs-fundamentals-1/supplement/AtqEE/c-syntax-notes-the-modern-range-based-for-loop](https://www.coursera.org/learn/cs-fundamentals-1/supplement/AtqEE/c-syntax-notes-the-modern-range-based-for-loop)

3. Unsigned Integer Types: Be Care
[https://www.coursera.org/learn/cs-fundamentals-1/supplement/zGkwp/unsigned-integer-types-be-careful-updated-dec-16](https://www.coursera.org/learn/cs-fundamentals-1/supplement/zGkwp/unsigned-integer-types-be-careful-updated-dec-16)

## Quiz Remarks

### Question 3
The **assignment operator** is a member function of the class of the target object, and this member function must be **public** in order for the assignment operator to be used in contexts outside of the class's own implementation as shown in the example in this question.

### Question 9
`*this` is a pointer to the current object instance.

In fact, members of the current object can be accessed as `this->membername` . For example, if you define a member function whose argument is the same name as a member variable, any use of that name in the local scope of the function refers to the argument and not the member variable, but you can still access the member variable as `this->membername` . Hence the following example works.

```c
class Just_a_double {
    double val;
public:
    void setValue(double val) {
        this->val = val;
    }
}
```

# 4 - Engineering C++ Software Solutions

## Key Concepts

-   Object-oriented design
-   Templates
-   Class hierarchies and inheritance

## Template Types

A **template type** is a special type that can take on different types when the type is initialized. `std::vector` uses a template type.

![enter image description here](https://imgur.com/ENYVfU4.png)

### std::vector

`std::vector` standard library class that provides the functionality of a dynamically growing array with a "templated" type.
|  Key ideas 	|   Code	|
|---	|---	|
|   Define in	|   `#include <vector>`	|
|   Initialization	|   `std::vector<T> v;`	|
|   Add to (back) of array	|   `::push_back(T);`	|
|   Access specific element|   `::operator[] (unsigned pos);`	|
|   Number of elements|  `::size()` 	|

When initializing a "templated" type, the template type goes inside of `< >` at the end of the type name:
```c
std::vector<char> v1;
std::vector<int> v2;
std::vector<uiuc::Cube> v3;
```


#### Example 1
```c
#include <vector>
#include  <iostream>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v;
    for (int i = 0; i < 100; i++) {
        v.push_back( i * i );
    }
    
    std::cout << v[12] << std::endl;

    return 0;
}
int  main() {
	std::vector<int> v;
	v.push_back(2);
	v.push_back(3);
	v.push_back(5);

	std::cout << v[0] << std::endl;
	std::cout << v[1] << std::endl;
	std::cout << v[2] << std::endl;

	return  0;
}
```
```
2
3
5
```

#### Example 2
```c
#include  <vector>
#include  <iostream>

int  main() {
	std::vector<int> v;
	for (int i = 0; i < 100; i++) {
		v.push_back( i * i );
	}
	std::cout << v[12] << std::endl;
	return  0;
}
```
```
144
```

## Tower of Hanoi

Consider the Tower of Hanoi problem, where multiple cubes must be transferred to a new location is such a way that a larger cube cannot be placed on top of a smaller cube:

<p align="center"> 
	<img src="https://imgur.com/OJh3MOl.png">
</p>

### Programmatic Structure
The Tower of Hanoi problem involves three district entitles that must be represented in code:
1. Game
2. Stacks
3. Cubes

```coop diagram
namespace uiuc {
	class Cube {
		public:
		// Class constructor: 2 parameters
		Cube(double length, HSLAPixel color);
		
		double getLength() const;
		void setLength(double length);
		
		double getVolume() const;
		double getSurfaceArea() const;

		private:
		double length_;
		HSLAPixel color_;
	}
}
```

A new class must be created to represent each of the stacks in the Tower of Hanoi game:

A single stack must contain:
- An vector of cubes
- Operations to interact with the top of the stack

```c
class Stack {
    public:
    void push_back(const Cube & cube);
    Cube removeTop();
    Cube & peekTop();
    unsigned size() const;

    // An overloaded operator <<, allowing us to print the stack
    // via `cout<<`:
    friend std::ostream& operator<<(std::ostream & os,
                                    const Stack & stack);

    private:
    std::vector<Cube> cubes_;
}
```

Finally the game is built from the components we have already built:
- An array of three stacks
- The initial state has four cubes in the first stack

The `Game.h` header file looks like:
```c
#pragma once

#include "Stack.h"
#include <vector>

class Game {
    public:
    Game();
    void solve();

    friend std:ostream& operator<<(std::ostream & os, const Game & game);

    private:
    std::vector<Stack> stacks_;
};
```

The `Game.cpp` implementation file looks like:
```c
Game::Game() {
    // Create the three empty stacks:
    for (int i = 0; i < 3; i++) {
        Stack stackOfCubes;
        stacks_.push_back( stackOfCubes );
    }

    // Create the four cubes, placing each on the [0]-th stack:
    Cube blue(4, uiuc::HSLAPixel::BLUE);
    stacks_[0].push_back(blue);

    Cube oragne(3, uiuc::HSLAPixel::ORANGE);
    stacks_[0].push_back(orange);

    Cube purple(2, uiuc::HSLAPixel::PURPLE);
    stacks_[0].push_back(purple);

    Cube yellow(1, uiuc::HSLAPixel::YELLOW);
    stacks_[0].push_back(yellow);
}
```

The `main.cpp` file looks like
```c
#include "Game.h"
#include <iostream>

int main() {
    Game g;

    std::cout << "Initial game state: " << std::endl;
    std::cout << g << std::endl;

    g.solve();

    std::cout << "Final game state: " << std::endl;
    std::cout << g << std::endl;

    return 0;
}
```


## Templated Functions

A template variable is defined by declaring it before the beginning of a class or function:

```c
template <typename T>
class List {
	...
	private:
	T data_;
};
```

```c
template <typename T>
int max(T a, T b) {
	if (a > b) {return a;}
	return b;
}
```

### Compile-Time Binding

Templated variables are checked at compile time, which allows for errors to be caught before running the program:

```c++
template <typename T>
T max(T a, T b) {}
	if (a > b) {return a;}
	return b;
```

## Inheritance

**Inheritance** allows for a class to inherit all member functions and data from a **base class** into a **derived class**.

A **base class** is a generic form of a specialized, **derived class**.




A base class example `Shape.h` looks like:
```c
#pragma once

class Shape {
    public:
    Shape();
    Shape(double width);
    double getWideth() const;

    private:
    double width_;
}
```

A derived class example `Cube.h` looks like:
```c
#pragma once

#include "Shape.h"
#include "HSLAPixel.h"

namaspace uiuc {
	// Inherites from the Shape class
    class Cube : public Shape {
        public:
        Cube(double width, uiuc::HSLAPixel color);
        double getVolume() const;

        private:
        uiuc::HSLAPixel color_;
    };
}
```


When a derived class is initialized, the derived class **must** construct the base class:
- `Cube` must construct `Shape`
- By default, uses default constructor
- Custom constructor can be used with an **initialization list**

### Access Control

When a base class is inherited, the derived class:
- Can access all **public** members of the base class
- **Cannot** access **private** members of the base class

### Initializer List

The syntax to initialize the base class is called the initializer list and can be used for several purposes:
- Initialize a base class
- Initialize the current class using another constructor
- Initialize the default values of member variables

```c
#include "Shape.h"

Shape::Shape() : Shape(1) {
	// Nothing.
}

Shape::Shape(double width) : width_(width) {
	// Nothing.
}

double Shape::getWidth() const {
	return width_;
}	
```

# References

- Prof. [Wade Fagen-Ulmschneider](https://www.coursera.org/instructor/fagen)
*The University of Illinois at Urbana-Champaign*
Object-Oriented Data Structures in C++
[https://www.coursera.org/learn/cs-fundamentals-1](https://www.coursera.org/learn/cs-fundamentals-1)

> Written with [StackEdit](https://stackedit.io/).
