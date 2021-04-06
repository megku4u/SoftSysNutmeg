# Chapter 12: The C memory model

# What does this chapter cover?

- Understanding object representations
- Working with untyped pointers and casts
- Restricting object access with effective types and alignment

This chapter focuses on the *C memory model* - an abstraction of the environment and state in which a C program is executed.

The concept of *virtual* memory is also touched upon, but all of this to emphasize that the C memory model is an abstraction and we should not care about the details; rather, we should focus on the abstracted behavior to help us design C programs that work, and that work well.

> Takeaway 2.12.0.1   *Pointer types with distinct base types are distinct.*

### 12.1 A uniform memory model

Here, we formally define **bytes** and establish that `sizeof(char)` is one, as these, by definition, take up one byte. In general, the `sizeof()` function can be used to determine the number of bytes that an object takes up.

### 12.2 Unions

This section recommends the `union` as the preferred tool to examine the individual bytes of objects.
"The difference here is that suche a `union` doesn't collect objects of different types into one bigger object, but rather *overlays* an object with a different type interpretation."

```c
#include <inttypes.h>

typedef union unsignedInspect unsignedInspect;
union unsignedInspect {
  unsigned val;
  unsigned char bytes[sizeof(unsigned)];
};
unsignedInspect twofold = {.val = 0xAABBCCDD, };

printf("value is 0x %.08 X\n", twofold.val);
for( size_t i = 0; i < sizeof twofold.bytes; ++i)
  printf("byte[%zu]:_0x %.02hhX\n", i, twofold.bytes[i]);
```

With the above example, the author's code printed something like:

value is 0xAABBCCDD
2 byte[0]: 0xDD
3 byte[1]: 0xCC
4 byte[2]: 0xBB
5 byte[3]: 0xAA

This is implementation-defined behavior. **Endianness** is defined as the storage order. In the above example, the storage order is called **little-endian**. If a system stores higher-order representation digits first, it's called **big-endian**. Both are common, and some processors are even able to switch between the two. The above output also assumes that one representation digit can be printed nicely by using two hexadecimal digits.

### 12.3 Memory and state

Here is where the concept of **aliasing**, or accessing the same object using different pointers, is defined.

> Takeaway 2.12.3.1 (Aliasing)  *With the exclusion of character types, only pointers of the
same base type may alias.*

This chapter actually suggests that you avoid using the `&` operator so as to protect variables from being aliased.

### 12.4 Pointers to unspecific objects

> Takeaway 2.12.4.1   *Any object pointer converts to and from void*\*.

There are some best practices described when using (or not using) `void*` in this section. What's important to note is that type information is valuable and if we lose that it can give us unexpected results.

### 12.5 Explicit conversions

"In general, the compiler can't know what type of object is behind the pointer."

Also, don't use casts. We don't favor information loss.

### 12.6 Effective types

> Takeaway 2.12.6.1 (Effective Type)  *Objects must be accessed through their effective type or through a pointer to a character type.*

> Takeaway 2.12.6.4   *Variables and compound literals must be accessed through their declared
type or through a pointer to a character type.*

### 12.7 Alignment

**Alignment** refers to the fact that objects of most non-character types usually start at a **word boundary**. "The alignment of a type then describes the possible byte positions at which an object of that type can start."

There's code in this section showing what happens when you mess with alignment. The author recommends crashing a feature to support in the development of portable code. `alignof()` is rarely used in real live code. Contrastingly, `alignas()` may be useful if you know that your platform can perform operations more efficiently with a different alignment.
