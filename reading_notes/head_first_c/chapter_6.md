# Chapter 6: Data Structures and Dynamic Memory

## What does this chapter cover?

- Linked lists
- Other data structures (light)
- Heap storage
  - `malloc()`
  - `free()`
  - `valgrind`
- `strdup()`s

## Linked Lists

The problem is presented as a situation (plane tours) where you'll need a way to store a *flexible* amount of data. Arrays are fixed length, which makes them difficult to work with, especially if you don't know *exactly* how long you want the array to be.

A **linked list** is an example of an *abstract data structure*. It stores a piece of data and a link to another piece of data.

The book has a sketching exercise to explain the linkage at the highest level possible.

> **Inserting data into a linked list is very quick**.

The book has a visual showing the difference between insertion for arrays and linked lists.

"Each one of the `struct`s in the list will need to connect to the one next to it. A `struct` that contains a link to another `struct` of the same type is called a **recursive structure**."

Using the island example, the chapter provides multiple visuals to illustrate containing a pointer to the next island.

In the "Watch it!" section, the chapter reminds the reader that recursive structures need names, because you need to give the `struct` a pointer to the same type.

Now, using more islands, the chapter shows how you can initialize the islands by setting the *next* pointer to `NULL`. Then, the islands can be linked by updating *next*.

The "Code Magnets" exercise shows how to iterate through the list using a `for` loop.

## Dynamic Storage

This is where the book introduces storing data in the **heap**.

`malloc()` is introduced, reusing the key and locker analogy from the pointers chapter (chapter 2).

`free()` is introduced after explaining how the heap differs from the stack, and introduces memory leaks.

> Remember: if you allocated memory with malloc() in one part of your program, you should always release it later with the free() function.

The exercise with the return of the out-of-work actors demonstrates the need to duplicate a string, which segways to the introduction of `<string.h>`'s `strdup()` function, which can reproduce a complete copy of the string given somewhere on the heap.

> That means that strdup() always creates space **on the heap**.

> **Always remember to release the storage with the `free()` function.**

Building on the island example, the code tackles taking island information from a file, and then also has another exercise to emphasize freeing space (and doing so in the right order).

> **Dynamic memory allocation lets you create the
memory you need at RUNTIME. And the way you
access dynamic heap memory is with `malloc()` and
`free()`**.

There's a "Fireside Chat" with *stack* and *heap*…

There's another matching exercise that compares a visual block diagram of a data structure to a written explanation of its utility. The structures represented are: SLLs, DLLs, binary trees, and maps/associated arrays.

This exercise is concluded with a warning about keeping track of memory in the heap.

The chapter introduces a denser exercise that has a larger code snipped. It also introduces binary trees.

It also introduces `valgrind` as a tool to check memory leaks (page 302). The book explains what `valgrind` does at a high level, enough to understand the rudimentary mechanics.

The `-g` switch adds debug information into the executable, and makes `valgrind`'s reports more readable.

    gcc -g spies.c -o spies

The exercise steps through a possible thought process of isolating the memory leak in the `spies` code.
The recommended process is as follows:

- spot when leaks happen
- identify the location where they happen
- check to make sure the leak is fixed
