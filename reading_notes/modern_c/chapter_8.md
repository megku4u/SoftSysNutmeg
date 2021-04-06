# Chapter 8: C library functions

## What does this chapter cover?

- Doing math, handling files, and processing strings
- Manipulating time
- Managing the runtime environment
- Terminating programs

### 8.1 General properties of the C library and its functions

This section starts off by roughly separating library functions into two categories:

- Platform abstraction layer
- Basic tools

Page 91 has a table of all of the C library headers.

This section dives into error and bounds checking as well.

### 8.2 Mathematics

Pages 94 and 95 have a table for all mathematical functions from `<tgmath.h>`. It is advised not to make programmer-generated versions of these functions as the ones that already exist are efficient and portable.

### 8.3 Input, output, and file manipulation

The function `putchar` is a more baseic function than `puts`, and you can use `putchar` to build your own version of `puts`.

The new type `FILE*` for **streams** is introduced. As such, functions `fputs` and `fputc` generalize the idea of unformatted output to streams.

Formally, the two default streams, `stdout` and `stderr`, are now introduced to the reader.

> Takeaway 1.8.3.3  `puts` *and* `fputs` *differ in their end-of-line handling*.

Now that these have all been introduced, the reader can now see how they can use `fopen` and `freopen` to attach files to the program execution. From there, the user can use `fputs` to write to those files.

The modifiers for `fopen` and `freopen` are on page 98. Page 99 has a table for the mode strings that are the valid combinations based off of page 98.

`freopen` can associate a given stream to a different file and change the mode. `fclose` closes the stream; by doing so, all buffers are guaranteed to be **flushed**. `fflush` pushed output immediately to ensure that what we have written has reached its destination.

Returning back to formatted output, the function `fprintf` is given to increase the ability to send formatted output to different places. Page 101 has format specifiers for `printf` and similar functions. The takeaways following this table relate to commonly used format specifiers. There is also a table on page 102 for format modifiers, and it's important to use the correct one. Finally, there are format flags on page 103.

Transitioning to input methods, firstly, the user should not use `gets`. Rather, `fgets` and `fgetc` are introduced.

`feof` can be used to test whether a stream's position has reached its end-of-file marker.

There are code implementations of `fgets` and `cat` on pages 104 and 105, respectively.

### 8.4 String processing and conversion

Page 106 has a nice table of character classifiers, as well as a table of special characters in character/string literals.

There are many `strto_`functions that convert strings to other types. These can be found on page 107.

### 8.5 Time

The `<time.h>` header introduces functions that can be used to express and utilize time stamps. This section goes into using `mktime` and making sure that values are implemented correctly.

Page 112 has a table for `strftime` format specifiers.

#### Challenge 10 (sorting algorithm performance)

Referring to challenge 1, use the implemented sorting algorithms and compare their runtimes.

### 8.6 Runtime environment settings

This section introduces the **environment list**, which holds the **environment variables**: variables that transmit specific information from the runtime environment.

Common variables include "HOME", "PATH", and "LANG".

You can use `setlocale` to modify the **locale** (language) setting. Categories for this function are on page 114.

### 8.7 Program termination and assertions

This section covers regular program termination (`return`) and irregular termination (`exit`). There is also explanation on how to create your own handlers. Assertions are also explained more in detail here as being helpful to confirm runtime properties and reduce the risk of an unwanted bug. Also, `NDEBUG` is introduced to inhibit `assert` and `abort` statements.

#### Challenge 11 (Image segmentation)

See book for many, many prompts related to segmenting images to partition pixels. (page 116)
