# Chapter 6: Derived Data Types

## What does this chapter cover?
- Grouping objects into arrays
- Using pointers as opaque types
- Combining objects into structures
- Giving types new names with `typedef`

### 6.1 Arrays

This section relates arrays and pointers to a *chicken and egg* problem. This book will aim to stay with arrays for as long as possible. The reader learns what arrays evaluate to and what arrays can and can't do. VLAs and FLAs are distinguished, and more takeaways are given for those specifications.

#### Challenge 6 (linear algebra)

Write functions that do vector-to-vector or matrix-to-vector products.

While on the topic of arrays, **strings** are now formally introduced. Pages 68-69 offer useful comparisons between different initializations of a string.

`<string.h>` and its relative functions are now introduced.

#### Challenge 7 (Adjacency matrix)

Use an adjacency matrix to conduct a breadth-first search in a graph.

#### Challenge 8 (Shortest path)

Find the shortest path between two nodes.

### 6.2 Pointers as opaque types

Pointers are defined as *opaque* objects, which means that we can only deal with them through the operations that C allows.

> Takeaway 1.6.2.6  *Always initialize pointers.*

### 6.3 Structures

If arrays combine items that have the same base type, `structs` combine items that have different base types. The declarations within the `struct` are called **members**.

### 6.4 Type aliases

> Takeaway 1.6.4.2   *A* `typedef` *only creates an alias for a type, but never a new type.*
