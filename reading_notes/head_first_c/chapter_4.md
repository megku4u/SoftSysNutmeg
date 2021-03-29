# Chapter 4: Using Multiple Source Files

## What does this chapter cover?

- Data types
- Casting
- Header Files
- Compilation Process
- `make`

## Data Type Quick Reference

The chapter starts by revisiting what data types are useful for different functions. Page 162 is a useful quick reference for this information.

## Numbers in C

The chapter talks briefly about making sure the right sized type is used for the right numerical value. The cups analogy is very helpful here.

The chapter also talks about **casting** to convert numbers. There is also a section dedicated to the keywords **unsigned** and **long**.

This chapter introduces the libraries `<limits.h>` and `<float.h>`, which contain values for integer types and floats/doubles, respectively. This is introduced within a code snippet that simply prints out the values.

The "Out-of-Work Actors" (think of these exercises as 'figure out what is wrong') return to demonstrate the limitations of C compilations with *implicit declarations*.

The chapter quickly recommends the student not resolve this issue by reordering functions. Rather, the student should **split the declaration from the definition**. This is illustrated by the head on the table.

## Creating Header Files

The book walks through the steps of creating and including a header file for a program, distinguishing between the `#include <...>` and the `#include ""` syntax.

This is followed by a "Be the Compiler" exercise to build intuition of possible bugs due to declarations and order of definitions.

There's a small section on page 181 dedicated to the reserved words in C.

For the following exercises, the chapter introduces XOR encryption to make an encrypting program.

The code to encrypt the message needs to be used by multiple files, and so the solution is to make a program from multiple files so that the programs can *share code*.

## How Compilation *Really* Works

Pages 184-185 describe the compilation process, where the computer is a "chef" making a dish. The steps are numbered and spaced out over the few pages:

1. Preprocessing
2. Compilation
3. Assembly
4. Linking

Page 186 details how to use this process to one's advantage by including the proper header file and passing the source files into `gcc`.

The chapter then suggests that large programs are a double-edge source, so how could the programmer speed up the time needed to recompile?

This is where the concept of creating **object code** for each source file comes in.

The next few pages outline how to compile the source code using the `-o` tag and then link them together afterwards.

The exercise on pages 192-195 focus on using the timestamp as a way to easily check which files need to be updated.

The manual process may seem even more time consuming to the reader, and the book makes sure to use this point as a transition to introducing `make`.

## `make`

In the book, `make` is represented as a robot friend. `make` compiles **targets**, which are files that are generated from some other files.

The big bullets on the page are the *two things* that `make` needs:

- the dependencies
- the recipe

Together, these form a **rule**.

Page 199 aims to step a little deeper in explaining how `make` works, while page 200 focuses on building the Makefile. The code is tested on page 201. There is a "Make Magnets" exercise for some brief Makefile writing practice.
