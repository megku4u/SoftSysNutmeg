# Chapter 11: Pointers

## What does this chapter cover?

- Introduction to pointer operations
- Using pointers with structs, arrays, and functions

This book warns the reader to be *patient*, as this section can be quite difficult to wrap your head around.

### 11.1 Pointer operations

Here, the operators `&` and `*` are introduced.

```c
void double_swap(double* p0, double* p1) {
    double tmp = *p0;
    *p0 = *p1;
    *p1 = tmp;
}
```

> Takeaway 2.11.1.1   *Using* \* *with an indeterminate or null pointer has undefined behavior.*

Now, we are ready to combine arrays and pointers. The following function sums all elements of an array:

```c
double sum0 (size_t len, double const* a) {
    double ret = 0.0;
    for (size_t i = 0; i < len; ++i) {
        ret += *(a + i);
    }
    return ret;
}
```
We also introduce pointer addition here, with two functions that sum the elements of the array in the same order:

```c
double sum1 (size_t len, double const* a) {
    double ret = 0.0;
    for (double const * p = a; p < a+len; ++p) {
        ret += *p;
    }
    return ret;
}
```

```c
double sum2 (size_t len, double const* a) {
    double ret = 0.0;
    for (double const*const aStop = a+len; a < aStop; ++a) {
        ret += *a;
    }
    return ret;
}
```
> Takeaway 2.11.1.2   *A valid pointer refers to the first element of an array of the reference type.*

> Takeaway 2.11.1.3   *The length of an array object cannot be reconstructed from a pointer.*

> Takeaway 2.11.1.4   *Pointers are not arrays.*

> Takeaway 2.11.1.5   *Only subtract pointers from elements of an array object.*

> Takeaway 2.11.1.6   *All pointer differences have type* `ptrdiff_t`.

> Takeaway 2.11.1.9   *Pointers have truth.*

There is even a name for when code tries to read one type as another:

> Takeaway 2.11.1.11  *Accessing an object that has a trap representation of its type has
undefined behavior.*

> Takeaway 2.11.1.12  *When dereferenced, a pointed-to object must be of the designated
type.*

There is code on page 139 to support this next takeaway.

> Takeaway 2.11.1.13  *A pointer must point to a valid object or one position beyond a
valid object or be null.*

The chapter then seeks to distinguish what a null pointer actually is. The important conclusion is that you shouldn't use `NULL`. It is recommended that you use 0 or `(void*)0` directly.

### 11.2 Pointers and structures

To demonstrate the rules and tools for pointers and structures, the book uses the `struct timespec` as explained earlier in the book.

The `->` operator is introduced. "It is equivalent to a combination of `*` and `.`." The utility of wrapper functions to protect and check inputs is shown as a useful one.

> Takeaway 2.11.2.1   *Don’t hide pointers in a* `typedef`.

#### Challenge 12 (text processor)

Use a DLL to store text and manipulate it.

### 11.3 Pointers and arrays

These next few takeaways will focus on the overlap that the book has been avoiding for a while: arrays and pointers.

> Takeaway 2.11.3.1  *The two expressions* `A[i]` *and* `\*(A+i)` *are equivalent.*

> Takeaway 2.11.3.2 (array decay)   *Evaluation of an array* `A` *returns* `&A[0]`.

> Takeaway 2.11.3.3   *In a function declaration, any array parameter rewrites to a pointer.*

So what does a good interface look like, given all of this? Here's an example from the book:

```c
double double_copy (size_t len,
                    double target[len],
                    double const source[len]);
```

> Takeaway 2.11.3.4   *Only the innermost dimension of an array parameter is rewritten*

> Takeaway 2.11.3.5   *Declare length parameters before array parameters.*

### 11.4 Function pointers

> Takeaway 2.11.4.1 (function decay)  *A function f without a following opening ( decays to a pointer to its start.*

Here are a few ways of defining/declaring the same function:

```c
typedef void atexit_function (void);
// Two equivalent definitions of the same type , which hides a pointer
typedef atexit_function * atexit_function_pointer;
typedef void (*atexit_function_pointer)(void);
// Equivalent declarations for the same function
void atexit (void f(void));
void atexit (atexit_function* f);
```

We dive into implementations for **binary search** and **quicksort**, to lead us to a very important takeaway:

> Takeaway 2.11.4.2   *Function pointers must be used with their exact type.*

This rule is strict yet very necessary because the calling conventions for different prototypes may be very different (and the pointer doesn't keep track of this).

> Takeaway 2.11.4.3   *The function call operator* `(...)` *applies to function pointers.*

The breakdown in the middle of page 148 is super helpful in terms of imagining this in the abstract state machine.

"When using pointers to functions, you should always be aware that doing so introduces
an indirection to the function call." (page 149)

#### Challenge 13 (Generic derivative)

Extend challenges 2 and 5.

#### Challenge 14 (Generic sorting)

Extend challenges 1 and 10 to other sort keys.
