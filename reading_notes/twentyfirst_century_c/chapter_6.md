# Chapter 6: Your Pal the Pointer

## What does this chapter cover?

- pointers
- avoiding `malloc`

This chapter is "intended for all those people who feel a little uneasy when working with pointers."

### Automatic, Static, and Manual Memory

This chapter introduces the three basic models of memory management in C: automatic, static, and manual. There's a table on pages 124-125 related to the relative uses of these models (note that manual memory makes Jesus weep).

There's a boxed out section to break down the difference in memory storage between the stack and the heap.

This is different from the variables themselves. Using the `static` keyword will make a variable static; otherwise, its automatic. Pointers are likely auto or static themselves, but could be pointing to any kind of memory.

Now, an important concept: distinguishing a pointer from an array. This chapter considers both `int an_array[]` and `int *a_pointer` and thinks about what happens when they are declared. This book recommends using pointer form in function headers because it's one less thing to think about.

### Persistent State Variables

Static variables can have local scope, but keep their value after a function exits. This is really nice for having an internal counter or reusable scratch space.

The book provides an example of this utility with the Fibonacci sequence:

```c
static _Thread_local int counter; // ensure thread-safety

long long int fibonacci(){
    static long long int first = 0;
    static long long int second = 1;
    long long int out = first+second;
    first=second;
    second=out;
    return out;
}

int main(){
    for (int i=0; i< 50; i++)
        printf("%lli\n", fibonacci());
}
```

The box on page 129 clarifies that static variables are initialized at runtime, so the cannot be initialized with a non-constant value unless you use a macro to start at zero.

### Pointers Without `malloc`

This section starts by distinguishing making a copy of a variable or aliasing when using pointers.

One benefit is to call something that has a rather clunky syntax, like something within a structure. Another benefit is to use automatic memory allocation simplify work to avoid using `malloc` in the case where you could simply pass a pointer and be good.

### Structures Get Copied, Arrays get Aliased

This section demonstrates the heading. But it's important to realize when you're changing a structure or a pointer - in that case, you may be aliasing instead of copying like you intended to. Also, you can return a struct from a function, but not an array.

To get around the array snafu, the chapter recommends using `memmove` from the `string.h` library.

### `malloc` and Memory-Twiddling

This book is pretty anti-`malloc`, but lists reasons for using it on page 134. These reasons include returning an array from a function, the need for objects persisting after their initialization function, and large chunks of data.

### The Fault Is in Our Stars

This section talks about the syntactical ickiness of using pointers, specifically the difference between declaration and nondeclaration. Here's some valid code:

```c
int i = 13;
int *j = &i;
int *k = j;
*j = 12;
```

### All the Pointer Arithmetic You Need to Know

Important arithmetic things include:
- Declare arrays with:
  - explicit pointer form: `double *p`
  - static/automatic form: `double p[100]`
- The *n*th array item is `p[n]` either way.
  - first item is zero!!!
- The address of the *n*th item is `&p[n]`.

"We can use the fact that p++ means “step to the next pointer” to streamline for loops."

There's a subsection dedicated to multidimensional arrays and provides a "more workable way" to implement an N1-by-N2-by-N3 array.

### Typedef as a teaching tool

Typedef just makes awkward code a little less so.

```c
#include <stdio.h>
typedef char* string;

int main(){
    string list[] = {"first", "second", "third", NULL};
    for (string *p=list; *p != NULL; p++){
        printf("%s\n", *p);
    }
}
```
Typedef can even make working with pointers to functions less daunting.
