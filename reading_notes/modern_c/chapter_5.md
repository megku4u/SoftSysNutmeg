# Chapter 5: Basic values and data

## What does this chapter cover?

- Understanding the abstract state machine
- Working with types and values
- Initializing variables
- Using named constants
- Binary representations of types

This chapter come with a warning: "If you already have experience in C and in manipulating bytes and bits, you will need to make an effort to actively "forget" your knowledge for most of this section. Thinking about concrete representations of values on your computer will inhibit you more than it helps."

### 5.1 The abstract state machine

This section talks about the *observable* values as the ones stored in an *adressable* memory. Then, the concept of **optimization** at compile time, and that a valid optimized executable must reproduce all **observable states**. This mechanism of change is called the **abstract state machine**.

Now we dive into the definition of value.

> Takeaway 1.5.1.1  *All values are numbers or translate to numbers.*

"The *data* of a program execution consists of all the assembled values of all objects at a given moment."

The *state* is dependent on the executable, the current point of execution, the data, and any outside intervention (I/O from user).

Now we formally define *types*:

> Takeaway 1.5.1.2  *All values have a type that is statically determined.*

The chapter lifts the hood and covers the *binary representation* of a type. It is observable, but still an *abstract representation*. " As a consequence, all computation is fixed through the values, types, and their binary representations that are specified in the program."

> Takeaway 1.5.1.7 (as-if)  *Programs execute as if following the abstract state machine.*

Returning to optimization, we tie the concepts of overflow and previous mentions of the compiler cutting corners to provide the following takeaway:

> Takeaway 1.5.1.8  *Type determines optimization opportunities.*

### 5.2 Basic types

This section separates the types into two levels: those provided by C syntax and those that are specified through header files. Page 43 has a table of the basic types. Types are separated in many ways: **narrow** vs. not (can you do arithmetic on it?), **integers** vs. **floating point** (do you get decimal precision?), and **signed** vs. **unsigned** (can the value be less than 0?).

The takeaways in this section are all about which types to use for what occasions. Page 45 has a tale related to semantic arithmetic types for special use cases.

### 5.3 Specifying values

The takeaways in this chapter are very low-level, maybe even too low level for someone who just wants to code. For example:

> Takeaway 1.5.3.4   *A decimal integer constant has the first of the three signed types that fits it.*

> Takeaway 1.5.3.11   *`I` is reserved for the imaginary unit.*

### 5.4 Implicit conversions

To be honest, most of this section went over my head; that being said, here are some useful takeaways:

> Takeaway 1.5.6.3   *An object of `const`-qualified type is read-only.*

> Takeaway 1.5.6.4  *String literals are read-only.*

Enums, surprisingly, are also introduced here as a mechanism to name small integers.

### 5.6 Named constants

The use of **integer constant expressions**, or ICE, is also introduced here.

> Takeaway 1.5.6.7  *An integer constant expression doesn't evaluate any object.*

**Macros** are introduced and their implementation is shown. To build off of that, **compound literals** are shown to express types that don't have literals that describe their constants.

### 5.7 Binary representation

This section dives into binary arithmetic, bitwise operations, bit shifting, overflow, and other binary related things. Sign representations, including One's and Two's complement, are also introduced here.

The limitations of floating-point representations are also discussed in this section.
