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

## Assignments

- Write a function to reverse a queue
`std::queue<int> reverse_queue(std::queue<int> q)`
- Write a function to reverse a stack
`std::stack<int> reverse_stack(std::stack<int> s)`
- Linked Lists and Merge Sort Project

# 2 - Binary Search Trees

## Key Concepts

Organizing ordered lists into a hierarchical structure, with algorithmic analysis of time complexity to show that searching is more efficient.

Also covers various tree traversal methods for serializing the hierarchical data.


## Tree Terminology

A tree is a linked structure with a sense of ancestry (parents, children, siblings, and more).

![](https://i.imgur.com/IF8QS3T.png)

Each element in our tree is a **node**. The nodes will store data and may be labeled.

Each connection between two nodes is an **edge**: $\rightarrow$. Edges do not have names, but are referred to by the nodes they connect.

Trees must always contain a **root node** that has no incoming edges.

Nodes that contain no outgoing edges are called **leaf nodes**.

Every node, except the root node, has exactly one **parent node**.

A node's **children** are the nodes with that node as it's parent. *(It's possible to have anywhere from 0 to infinite children.)*

Three conditions for a tree:

1. Must have a root
2. Must have directed edges
3. Must not have a cycle


We say a tree is "**rooted**, **directed**, and **acyclic**" structure.

### Summary

- Trees formed with nodes and edges.
- Trees must be rooted, directed, and acyclic.
- The relationship between nodes in a tree follow classical ancestry terms (parent, child, etc.).


## Binary Trees

A **binary tree** is a tree where every node has **at most** two children.

![](https://i.imgur.com/YBT7oxS.png)

### Binary Tree Children

In binary trees, we will label every child as either the **"left child"** or **"right child"** of its parent.

Binary trees can be thought as linked lists where each nodes has two outward links, e.g.:

```c
template <typename T>
class BinaryTree {
    public:
    //...

    private:
    class TreeNode {
        public:
        T & data;
        TreeNode *left, *tight;
        TreeNode(T & data) :
                data(data), left(nullptr), right(nullptr) {}
    };

    TreeNode *root_;
};
```

### Binary Tree Property: Height

The **height** of a binary tree is the number of edges in the **longest** path from the root to a leaf.

### Binary Tree Property: Full

A binary tree is **full** if and only if every node has either zero children or two children.

![](https://i.imgur.com/90QW67I.png)

### Binary Tree Property: Perfect

A binary tree is **perfect** if and only if all interior nodes have two children and leaves are at the same level.

### Binary Tree Property: Complete

A binary tree is **complete** if and only if the tree is perfect up until the last level and all leaf nodes on the last level are pushed to the left.

![](https://i.imgur.com/jmgPxgQ.png)

### Puzzles:

Is a **full** tree **complete**? No.

Is a **complete** tree **full**? No.

### Summary

- Binary Trees are a special case of a tree where each node has at most two children.
- The children of a binary trees are referred to as the "left child" and "right child".
- Binary Trees have a **height** and a definition for being **full**, **perfect**, and **complete**.

## Tree Traversals

Tree traversals deal with problems such as

- How to get the data?
- How to visit every single node?
- In what order do we visit these nodes?

![](https://i.imgur.com/AaYnSzW.png)

Strategy #1: Pre-order: Shout --> Left --> Right

```c
template <class T>
void BinaryTree<T>::preOrder(TreeNode * cur)
{
	if (cur != NULL) {
		shout( cur );
		preOrder( cur->left );
		preOrder( cur->right );
	};
};
```
```
+ - a / b c * d c
```

Strategy #2: In-order: Left --> Shout --> Right

```c
template <class T>
void BinaryTree<T>::inOrder(TreeNode * cur)
{
	if (cur != NULL) {
		inOrder( cur->left );
		shout( cur );
		inOrder( cur->right );
	};
};
```
```
a - b / c + d * e
```

Strategy #3: Post-order: Left  --> Right --> Shout

```c
template <class T>
void BinaryTree<T>::postOrder(TreeNode * cur)
{
	if (cur != NULL) {
		postOrder( cur->left );
		postOrder( cur->right );
		shout( cur );
	};
};
```
```
a b c / - d e * +
```

Strategy #4: Level-order: 
```
+ - * a / d e b c
```


## Binary Search Trees

A binary search tree (BST) is an **ordered** binary tree capable of being used as a search structure.

### BST Order Property

A binary tree is a BST if **for every node in the tree:**

- Nodes in the **left** subtree are **less** than itself.
- Nodes in the **right** subtree are **greater** than itself.

![](https://i.imgur.com/CMnHDyQ.png)

### Dictionary

A dictionary associates a **key** with **data**:


| Key (Unique)                	| Data         	|
|--------------------	|--------------	|
| Login email        	| Profile data 	|
| Phone number       	| Phone record 	|
| URL                	| Web-page      	|
|Street address     	| Your home    	|
|||


### Dictionary ADT

`find` --> Finds the data associated with a key in the dictionary
`insert` --> Adds a key/data pair to dictionary
`remove` --> Removes a key from the dictionary
`empty` --> Returns `True` if the dictionary is empty

### BST-Based Dictionary

A BST used to implement a dictionary will store both a key and data at every node:

![](https://i.imgur.com/3EAhlZs.png)

Implementation in C++

```c
template <typename K, typename D>
class Dictionary {
    public:
    Dictionary();
    const D & find(const K & key);
    void insert(const K & key, const D & data);
    const D & remove(const K & key);

    private:
    class TreeNode {
        public:
        const K & key;
        const D & data;
        TreeNode *left, *right;
        TreeNode(const K & key, const D & data)
                : key(key), data(data), left(nullptr), right(nullptr) {}
   };

   TreeNode *head_;
   ...
}
```

### Runtime of `BST::find`

Worst-case outcome of find:

Visiting the longest path:

 $$O(h) \leq O(n)$$
 
, where $h$ is the height of the tree and $n$ is the size of data.

Implementation in C++:

```c
template <typename K, typename D>
const D & Dictionary<K, D>::find(const K & key) {
    TreeNode *& node = _find(key, head_);
    if (node == nullptr) { throw std::runtime_error("key not found"); }
    return node->data; 
}

...

template <typename K, typename D>
typename Dictionary<K, D>::TreeNode *& Dictionary<K, D>::_find(
const K & key, TreeNode *& cur) const {
    if      (cur == nullptr)    { return cur; }
    else if (key == cur->key)   { return cur; }
    else if (key < cur->key)    { return _find(key, cur->left); }
    else                        { return _find(key, cur->right); }    
}
```

### Insert into a BST

```c
/**
 * insert()
 * Inserts `key` and associated `data` into the Dictionary.
 */
template <typename K, typename D>
void Dictionary<K, D>::insert(const K & key, const D & data) {
    TreeNode *& node = _find(key, head_);
    node = new TreeNode(key, data);
}
```

### In-Order Predecessor (IOP)

The in-order predecessor is the previous node in an in-order traversal of a BST.

![](https://i.imgur.com/AK9Byc4.png)

In-order Traversal: `2 4 11 19 20 37 51 55`

The IOP of a node will **always** be the right-most node in the node's left sub-tree.

### Remove from a BST

**Zero children:** Simple, delete the node.

**One child:** Simple, works like a linked list.

**Two children:** 

- Find the IOP of the node to be removed.
- Swap with the IOP.
- Remove the node in it's new position.

```c
/**
 * remove()
 * Remove `key` from the Dictionary. Returns the associated data.
 */
template <typename K, typename D>
const D & Dictionary<K, D>::remove(const K & key) {
    TreeNode *& node = _find(key, head_);
    return _remove(node);
}

template <typename K, typename D>
const D & Dictionary<K, D>::_remove(TreeNode *& node) {
    // Zero child remove:
    if (node->left == nullptr && node->right == nullptr){
        const D & data = node->data;
        delete(node);
        node = nullptr;
        return data;
    }

    // One-child (left) remove
    else if (node->left != nullptr && node->right == nullptr)
    {
        const D & data = node->data;
        TreeNode *temp = node;
        node = node->left;
        delete(temp);
        return data;
    }

    // One-child (right) remove
    else if (node->left == nullptr && node->right != nullptr)
    {
        const D & data = node->data;
        TreeNode *temp = node;
        delete(temp);
        return data;
    }

    // Two-children remove
    else
    {
        // Find the IOP
        TreeNode *& iop = _iop( node->left );

        // Swap the node to remove and the IOP
        _swap( node, iop );

        // Remove the new IOP node that was swapped
        return _remove( node ); 
    }
}
```


## BST Analysis

Binary Search Trees (BSTs) can take on many forms and structures, even containing the same data:

![](https://i.imgur.com/5xsEE3P.png)

Both trees contain the value $\{1, 2,3,4,5,6,7\}$ with different insert orders: `4 2 3 6 7 1 5` and `1 3 2 4 5 7 6`.

### Puzzle 

How many possible ways can we insert the same data into a BST? 

For a data-set of $n$ data, there are $n!$ ways of inserting them into a BST.

| Operation	| BST Average Case	| BST Worst Case	| Sorted Array	| Sorted List|
|----|----|----|----|----|
| `find`|$O(\text{lg}(n))$|$O(n)$| $O(\text{lg}(n))$| $O(n)$ |
| `insert`	|$O(\text{lg}(n))$|$O(n)$|$O(n)$|$O(n)$|
| `remove`	|$O(\text{lg}(n))$|$O(n)$|$O(n)$|$O(n)$|
||||||

### Height Balance Factor

The height balance factor $(b)$ of a node is the difference in height between its two sub-trees.

### Balanced BST

A balanced BST is a BST where **every node's** balance factor has a magnitude of **0 or 1:**

### Summary

There are $n!$ different ways to create BSTs with the same data.

- The worst-case BST will have a height proportional to the number of nodes.
- An average BST will have a height proportional to the logarithm of the number of nodes.

Using a height balance factor, we can formalize if a given BST is balanced.

## Assignments




# 3 - Advanced Tree Structures

// TBC


# 4 - Heap Structures

// TBC

# References

- Prof. [Wade Fagen-Ulmschneider](https://www.coursera.org/instructor/fagen)
*The University of Illinois at Urbana-Champaign*
Ordered Data Structures
[https://www.coursera.org/learn/cs-fundamentals-2](https://www.coursera.org/learn/cs-fundamentals-2)




  

> Written with [StackEdit](https://stackedit.io/).
