# Syllabus

The specific data structures covered by this course include:
- Arrays
- Linked lists
- Queues
- Stacks
- Trees
- Binary trees
- AVL trees
- B-trees
- Heaps 

This course also shows, through algorithmic complexity analysis, how these structures enable the fastest algorithms to **search** and **sort** data.



# 1 - Linear Structures

## Key Concepts

Linear data structures for maintaining an ordered list of items, including
- Arrays
- Linked lists
- Queues and stacks

and their algorithmic analysis of **time complexity** for key operations such as **inserting** or **deleting** an item.

## Arrays

An array stores data in blocks of **sequential memory**.

**Array Limitation**
- All data in an array must be of the **same type**
- The **size** (number of bytes) of the type of data is known.
	- `sizeof(x)` to find the byte size of a variable
- Arrays have a fixed **capacity**.
	- Arrays **must** store their data sequentially in memory.
	- The **capacity** of an array is the maximum number of elements that can be stored.
	- The **size** of an array is the current number of elements stored in the array.

The **only way** to add another element when an array is full is to allocate a new, larger array and **copy** over all of the data.

### Arrays in C++
The `std::vector` implements an array that dynamically grows in size automatically. However, all properties remain true:
- Array elements are a fixed data type.
- At any given point, the array has a fixed capacity.
- The array must be expanded when the capacity is reached.

## Linked Memory

Linked memory stores data together with a "link" to the location (in memory) of the next list node:

![enter image description here](https://imgur.com/ZmT0csM.png)

### List Nodes

A **list node** refers to pair of both the date and the link.
![enter image description here](https://imgur.com/yUvdDrJ.png)


### Linked List

Zero or more `ListNode` elements linked together form a **Linked List**.

![](https://i.imgur.com/dqhyFoW.png)

- A pointer called the **"head pointer"** stores the link to the beginning of the list.
- A pointer to `nullptr` ($\bold{\mathbb{∅}}$) marks the end of the list.

### `List::get`

**Objective**: Return the element at index $k$.

![](https://i.imgur.com/mnD7ZY0.png)

```c
template <typename T>
const T & List<T>::operator[](unsigned index) {
    // Start a `thru` pointer to advance thru the list:
    ListNode *thru = head_;
    
    // Loop until the end of the list (or until a `nullptr`):
    while (index > 0 && thru->next != nullptr) 
    {
        thru = thru->next;
        index--;
    }
    
    // Return the data:
    return thru->data;
}
```

### List Run-time

In a list, the time it takes to access a given index grows based on the size of the list.

In contrast, an array can access any element in a constant fixed amount of time. Therefore, for accessing a given index, an array is faster than a list.

### `List::insert`

**Objective**: Add an element to the list.

The header file `List.h` looks like

```c
template <typename T>
void List<T>::insertAtFront(const T & data) {
    // Create a new ListNode on the heap:
    ListNode *node = new ListNode(data);

    // Set the new node's next pointer point the current
    // head of the List:
    node->next = head_;

    // Set the List's head pointer to be the new node:
    head_ = node;
}
```

### List Capacity

In a list, the **capacity** is bounded only by the memory available on the system.

In contrast, an array has a fixed capacity. A list is a more flexible data structure than an array.

### Data Types

In both arrays and lists, all data within an instance of a container must be the same type.

- An integer {array, list} be only contain integers.
- A string {array, list} must only contain strings.
- ...

### Summary

- Linked memery stores data in "nodes" linked together by "links" (pointers).
- A basic linked memory structure is a Linked List, which consists of zero or more `ListNodes` linked together and a **head** pointer.
- A linked list provides a flexible alternative to an array.

## Run Time Analysis

**Run-time Analysis** allows us to formalize a method of comparing the speed of an algorithm as the size of input grows.

We summarize the runtime in "Big-O notation", leaving only the term that dominates the growth:
- $O(1)$, constant time
- $O(n)$, linear time
- $O(n^2)$, polynomial time

## Array and List Operations

![](https://i.imgur.com/YGJmd0U.png)

### Access a Given Index

**Objective**: Access a given index:

- Array: $O(1)$
- Linked List: $O(n)$

### Array Resize Strategy

**Objective**: Resize an array:

Strategy #1: When the array is full, make a copy of the array and add two to the capacity.

- The total number of copies made is $\frac{n^2+2n}{4}$
- $O(n^2)$

Strategy #2: When the array is full, double the capacity.

- The total number of copies made is $2(n-1)$
- $O(n)$
- Average work per element: $\frac{O(n)}{n}=O(1)$

### Insert at Front

**Objective**: Insert an element at the front

- Array: $O(1)$ - amortized constant time when array size is doubled when copied
- List: $O(1)$ - fixed constant time by adding the new data at the head of the list

### Find Data

**Objective**: Given data, find the location of that data in the collection.

- Array: $O(n)$ - requires searching up to the full array, one-by-one, to find a match
- List: $O(n)$ - requires searching up to the full list, one-by-one, to find a match

### Find Data in a Sorted Array

**Objective**: Given data, find the location of that data in the collection.

- Unsorted Array: Linear Search: $O(n)$
- Sorted Array: Binary Search: $O(\text{lg}(n))$
- All Lists: $O(n)$

### Insert After

**Objective**: Given an element (ListNode or index), insert a new element immediately afterwards.

- Arrays: $O(n)$ - requires copying up to half of the array to make space for the new element
- Lists: $O(1)$ - fixed constant time to add a new element after finding the previous element

### Delete After 

**Objective**: Given an element (ListNode or index), delete the element immediately afterwards.

- Arrays: $O(n)$ - requires copying up to half of the array to remove the blank space
- Lists: $O(1)$ - fixed constant time to remove a ListNode and repair the list.

### Summary

Arrays and lists are both ordered collections that have complex trade-offs between run-time and flexibility.

We will build data structures using these primitive structures.

## Queue (Data Structure)

A queue is a first-in-first-out (FIFO) data structure that is similar to waiting in a line or "queue".

![](https://i.imgur.com/mRPMu2k.png)

### Abstract Data Type

In data structures, we will always begin our analysis asking "how can this structure be used with data?"

A structures's **Abstract Data Type** (ADT) is how data interacts with the structures.

- An ADT is **not** an implementation, it is a description.

### Queue ADT

- `create` --> Creates an empty queue
- `push` --> Adds data to the back of the queue
- `pop` --> Removes data from the front of the queue
- `empty` --> Returns `True` if the queue is empty

### Queue in C++

C++ has built-in queue data type in the standard library, e.g. `std::queue<std::string> q` creates a string queue `q`.

**Example**
```c
#include <iostream>
#include <queue>

int main() {
    // Create a std::queue:
    std::queue<std::string> q;

    // Add several strings to the queue:
    q.push( "Orange" );
    q.push( "Blue" );
    q.push( "Illionis" );

    // Print the front of the queue out and pop it off:
    std::cout << "First pop(): " << q.front() << std::endl;
    q.pop();

    // Add another string and then print out the front of the queues:
    q.push( "Illini" )
    std::cout << "Second pop(): " << q.front() << std::endl;
    
    
    return 0;
}
```
```
First pop(): Orange
Second pop(): Blue
```


### Implementation
 
Array-based queue
- $O(1)$ 
- Amortized run-time for `push` and `pop`; occasional need to double the capacity of the array.

List-based queue
- $O(1)$
- Doubly-linked list required for $O(1)$ run-times.

### Summary

A queue may be implemented with an array or a doubly-linked list. 

Both implementation can be built to run in constant, $O(1)$ time.



## Stack (Data Structure)

A stack is a **last-in**-first-out (LIFO) data structure that is similar to a pile ("stack") of papers.

![](https://i.imgur.com/3kR7MEG.png)

### Stack ADT

- `create` --> Creates an empty stack
- `push` --> Adds data to the top of the stack
- `pop` --> Removes data from the top of the stack
- `empty` --> Returns `True` if the stack is empty


### Stack in C++

C++ has built-in stack data type in the standard library, e.g. `std::stack<std::string> a` creates a string stack `s`.

**Example**

```c
#include <iostream>
#include <stack>

int main() {
    // Create a std::stack:
    std::stack<std::string> s;

    // Add several strings to the stack:
    s.push( "Orange" );
    s.push( "Blue" );
    s.push( "Illionis" );

    // Print the front of the stack out and pop it off:
    std::cout << "First pop():" << s.top() << std::endl;
    s.pop();

    // Add another string and then print out the top of the stack:
    s.push( "Illini" )
    std::cout << "Second pop():" << s.top() << std::endl;
    
    return 0;
}
```

```
First pop(): Illionis
Second pop(): Illini
```

### Implementation

**Objective:** Create a Stack Data Structure

Array-based

- $O(1)$
- Store the index of the top element only
- Amortized run-time for `push` and `pop`; occasional need to double the capacity of the array.

List-based

- $O(1)$
- Singly-linked list is sufficient

### Summary

A stack may be implemented with an array or a linked list.

Both can be built to run in constant, $O(1)$, running time.

# 2 - Intro to Tree Structures

// Nothing

# 3 - Advanced Tree Structures

// Nothing


# 4 - Heap Structures

// Nothing

> Written with [StackEdit](https://stackedit.io/).
