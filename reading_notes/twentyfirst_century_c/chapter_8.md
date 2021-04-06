# Chapter 8: Important C Syntax that Textbooks Often Do Not Cover

## What does this chapter cover?

- What other textbooks don't
  - macros
  - preprocessor
  - linkage
  - const

### Cultivate Robust and Flourishing Macros

Two types of macros exist
- expands to an expression
- block of instructions

Rules for macros
- Parentheses! Put all inputs in parentheses unless you have a specific reason not to.
- Avoid double usage to ensure macros expand properly.
- Use curly braces for blocks.
  - there are edge cases here, but the best solution is to warn the user.

### The Preprocessor

The preprocessor uses the `#` token to
- mark directives
- stringize an input
- concatenate tokens

The preprocessor also merges two string literals if they are adjacent.

You can use a two octothorps to join two things that are not strings.

The code on page 168 leverages different features of the preprocessor to provide variables that kept track of array lengths.

There's a subsection related to macro arguments as well.

### Test Macros

*skip; out of scope of current SoftSys understanding*

### Header Guards

This section introduces the power of `#ifndef` and `#endif` to prevent multiple declarations.

You can simplify this even further by using `#pragma once` at the head of the file to be included once.

You can also use the preprocessor to comment out code in a nested fashion, but the nesting must be correct or you will get an error.

### Linkage with static and extern

Use the `extern` keyword to indicate external linkage.

Use the `static` keyword to indicate static linkage.
- file scope variables - only affects linkage
- block scope variables - only affects memory model
- functions - only affects linkage

You can also precede the declaration of your function in your .h to be included everywhere, so to speak.

### Externally Linked Variables in Header Files

To use `extern`,
- declare the variable with the keyword `extern` in a header to be included anywhere the variable will be used
- declare the variable as usual in only one .c file.

### The const Keyword

The `const` keyword is a "literary device" for the programmer. The author recommends to use it when possible. to make sure that data that shouldn't change, doesn't.

Caveats:
1. Data marked as `const` under one name can be modified using a different name.

### Noun-Adjective form

This section introduces the "right-to-left" rule. With this, the author notes that you can switch a type name and `const` and they will mean the same thing. This section recommends `int const` as opposed to `const int` because it helps with the right-to-left rule.

### Tension

This highlights the tension that arises when you pass a `const` as a non-`const` parameter. You have to first ask yourself if the function could modify the `const`. If not, the book suggests that you could cast the `const` to a non-`const` to quiet the compiler.

### Depth

If you really need to protect only the lowest level in your hierarchy of types, your best bet is to put a note in the documentation.

### The `char const**` Issue

This section talks about the need to make an explicit cast when using a `char const**`. It boils down to the previous point that `const`s can be changed under a different name.

There is a subsection on booleans, and what is important to know is that you can read `if(x)` to be "if x is true".
