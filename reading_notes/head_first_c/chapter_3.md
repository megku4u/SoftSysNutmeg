# Chapter 3: Creating Small Tools

## What does this chapter cover?

- Designing small tools
- Standard Input, Standard Output, and Standard Error
  - redirecting using `<`, `>`, and `2>`
- `fprintf()`
- Piping
- Opening, reading/writing, and closing files in C
- Command-line arguments and options


## Intro to Small Tools

> A **small tool* is a C program that does *one* task and *does it well*.

This chapter focuses on the versatility of separating code into smaller programs to increase the versatility of that code.

The reader starts by filling in code for GPS data. This code will carry through the chapter. The visual on page 108 details how the intended program should work.

> Tools that read data line by line, process it, and write it out are called **filters**.

## Standard Input and Standard Output

The **Standard Input** and **Standard Output** are represented using an ear and a mouth, respectively.

> **You can redirect the Standard Input and Standard Output so that they read and write data somewhere else, such as to and from files.**

Pages 111 and 112 show how redirecting the standard input and output with `<` and `>`, respectively, can change the location of the input and output and use files as both inputs and outputs.

After this, the chapter takes a moment to practice adding code to validate data. This helps to segway to the fact that **Standard Error** is another output stream that exists, so in the case of the visual metaphor, the program has one ear and two mouths.

This visual is shown in page 121.

To utilize `stderr`, the chapter introduces `fprintf()`.

> You can redirect the Standard Error using `2>`.

The exercise is updated to use `fprintf()`, and the chapter tells the reader the following:

> The Standard Error was created with exactly this in mind: to separate the error messages from the usual output. But remember: `stderr` and `stdout` are both just output streams. **And there’s nothing to prevent you from using them for anything.**

## Piping

A **pipe** (`|`) can be used to connect the Standard Output of one process to the Standard Input of another process.

The book, notably also use pages with "notepads" on them to simulate someone writing pseudocode.

## Multiple Data Streams

Here, the reader is introduced to `fopen()` (and it's three modes: "w", "r", "a"), `fscanf()`, and  `fclose()`, as well as the new data type `FILE` (or more specifically, a pointer to that file).

This utility is simple to understand; as such, the implementation is limited to a single fill-in code exercise (pages 138-139).

## Command-Line Arguments

The chapter introduces the following as a "second version" of the `main()` function:

    int main(int argc, char *argv[])
    {
      ... Do stuff...
    }

There is a visual block breakdown on page 141 that is helpful to understand how the main function reads the arguments as an **array of strings**, or more specifically, an *array of character pointers to strings*.

The following Code Magnets exercise gets the reader used to indexing command-line arguments (pages 142-145).

## Command-Line Options

The chapter describes **command-line options** as "little switches" that add certain enhancements.

Using the `<unistd.h>` library, the user can use the `getopt()` function to find options on the command line.

The chapter provides the necessary code to appropriately iterate through the options:

    #include <unistd.h>
    ...
    while ((ch==getopt(argc, argv, "ae:")) != EOF) // replace "ae:" with valid options
    {
      ...
      // switch statements
      ...
    }
    argc -= optind; // Skip past options we have already read
    argv += optind;

The caveat with this code is that after processing the arguments, **the 0th argument will point to the first command-line argument that follows the options**.

This new tool is practiced with code that resembles ordering pizza.
