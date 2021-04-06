# Chapter 7: Inessential C Syntax that Textbooks Spend a Lot of Time Covering

## What does this chapter cover?

- What it doesn't want to cover in other chapters...

### Don't Bother Explicitly Returning from `main`

- reaching the `}` that terminates the main function returns a value of 0 by default.

### Let Declarations Flow

- Make code easier to read by declaring variables when you need them, not all at once at the beginning

There's a note that this will *not* slow down your program.

### Set Array Size at Runtime

Take the following example:
```c
int thread_count = atoi(argv[1]);
pthread_t threads[thread_count];
```
It reads really nicely, and there are fewer places for mistakes.

### Cast Less

Here's some code for a function that takes a void pointer:
```c
int use_parameters(void *params_in){
  param_struct *params = params_in; //Effectively casting pointer-to-NULL
  ... //to a pointer-to-param_struct.
}
```

Casting is still valuable when converting between float and int for arithmetic or indexing purposes.

### Enums and Strings

Enums, when done right, can be useful when writing code, but strings can also do the same job without cluttering the namespace or users' memory.

### Labels, gotos, switches, and breaks

This is a bit of a diversion to assembly code, which is more of a Computer Architecture topic.

### goto Considered

`goto` can be useful if you want a clean getaway in case of errors. "It is generally harmful but is a common present-day idiom for cleaning up in case of different kinds of errors, and it is often cleaner than the alternatives."

The section below this covers the different kinds of exits.

### switch

This book recommends if/else statements instead of `switch` statements to avoid unwanted fall-through.

### Deprecate float

This section recommends using double instead of float, and in intermediate values in calculations, `long double` doesn't hurt. The examples following this show different levels of precision. This argument isn't as strong for using `long int`s instead of `int`s.

### Comparing Unsigned Integers

Don't get caught up in the many layers of variable types. In this section's code example, we see that comparing a signed type to an unsigned type will force the signed type to be unsigned.

### Safely Parse Strings to Numbers

While `atof` and `atoi` are the most common, they don't have error checking. This section recommends `strtol` and `strtod`, which take more work but can check for errors.

```c
#include "stopif.h"
#include <stdlib.h> //strtod
#include <math.h> //pow

int main(int argc, char **argv){
    Stopif (argc < 2, return 1, "Give me a number on the command line to square.");
    char *end;
    double in = strtod(argv[1], &end);
    Stopif(*end, return 2, "I couldn't parse '%s' to a number. "
        "I had trouble with '%s'.", argv[1], end);
    printf("The square of %s is %g\n", argv[1], pow(in, 2));
}
```
There's a section dedicated to clarifying `NaN`'s utility and logical use. Use `isnan(x)` to test whether `x` is `NaN`.
