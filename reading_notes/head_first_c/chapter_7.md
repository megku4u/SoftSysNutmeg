variadic# Chapter 7: Advanced Functions

## What does this chapter cover?

- Function pointers
- Function array pointers
- Variadic functions
  - <stdarg.h> library

## Functions as Parameters

The chapter starts by stating that "C functions can make your code **do more things** but *without* writing a lot more code." (312)

The given example is a bit dated, but we'll avoid going into that.

The chapter uses a "Code Magnets" exercise to have the reader build the code to be evaluated later on.

After the reader completes this exercise, the chapter notes the limitations of the implementation due to the fact that the code can only handle two strings and needs to be copied every time we want to filter for different strings.

The book then gives a visual for "passing code to a function" and relates it to a "testing machine". The benefit of this is that the student-built `find()` function would stay the same.

The code for testing if the strings are met is isolated and then the book proposes that the reader find a way to **inject** the code by passing the name of the function to use it in the larger program.

And here is where we get to the big surprise:

> **Every function name is a _pointer_ to the function**

The memory model is displayed again to show that when you create a function, you are also creating a pointer variable, located in the constants section of memory, that contains the address of the function.

    int go_to_warp_speed(int speed) {
      ...
    }

    int (*warp_fn)(int);
    warp_fn = go_to_warp_speed;
    warp_fn(4);



    char** album_names(char *artist, int year) {
      ...
    }

    char** (*names_fn)(char* int);
    names_fn = album_names;
    char** results = names_fn("Sacha Distel", 1972);

The chapter notes that the syntax is a bit complex, but also justifies its complexity because "you need to tell C the return type and the parameter types the function will take."

Another exercise is presented that lets the reader write functions for other search criteria.

With this information, the `find()` code is updated.

There's a diagram to help more clearly describe the individual parts of the function pointer syntax, although "The Hunter's Guide" might not be the best.

The chapter asks about sorting data, and it's unfortunate that they focus on objectifying men and reinforcing stereotypes, but it transitions to introducing `qsort()` from the C Standard Library.

    qsort(void *array, // array to sort
          size_t length, // size of array
          size_t item_size, // size of array elements
          int (*compar)(const void *, const void *)); // pointer to function that compares two items in array

The comparator option tells `qsort()` which order a pair of elements should be in. There's an image using stick figures to show what the values are when a the first value is greater than (+), less than (-), or equal to (0) the second value.

The chapter uses the example of sorting integers to show how to use **void pointers**.

> A void pointer can store the address of *any kind of data*, but you always need to *cast* it to something more specific before you can use it.

    int compare_scores(const void* score_a, const void* score_b) {
      int a = *(int*)score_a; // Cast the pointer to an integer pointer
      int b = *(int*)score_b; // The first * gets the int stored at address store_b
      return a-b;
    }

    qsort(scores, 7, sizeof(int), compare_scores);

There are exercises for the reader to fill in comparing function code.

The next example involves writing letter responses given certain criteria. The chapter shows the limitations of using `switch` statements to compare values, because every time the criteria changes, the `switch` statement has to be remade. Also, the `switch` statements are limited by the size they were initialized as; if you had a new option, for example, you'd have to manually add it.

The solution? An array of function pointers that match different response types.

    enum response_type {DUMP, SECOND_CHANCE, MARRIAGE};

    void (*replies[])(response) = {dump, second_chance, marriage};

> **Return type** | (* **Pointer variable** )( **Param types** )

The book notes the function names must be in **exactly the same order as the types in the enum**.

"When C creates an `enum`, it gives each of the symbols a number starting at 0. So DUMP==0, SECOND_CHANCE==1, and MARRIAGE==2. And that's really neat, because it means you can get a pointer to one of your sets of functions using a `response_type`:"

    replies[SECOND_CHANCE] == second_chance;

The chapter prefaces the exercise on page 339 by saying that the exercise. The goal of the exercise is to show how the use of a function pointer array can increase the versatility of code and even save code space.

Also, the book highlights how the programmer needs to only update `response_type` and `replies` if they have new functions.

Revisiting the `printf()` function, the chapter notes that this function can take as many arguments as are needed to print, making it extremely useful and versatile. The next example demonstrates a need for this type of flexibility.

This is the time to introduce **variadic** functions, which are functions that take a variable number of parameters,

> The C Standard Library contains a set of **macros** that can help you create your own variadic functions.

To demonstrate the utility of the macros, the following exercise gets the reader to create a function that prints out series of `int`s.

The code is given and broken down with a visual that spans two pages of a textbook.

    #include <stdarg.h> //code to handle variadic Functions

    void print_ints(int args, ...) //the ellipsis after the argument of a function means there are more arguments to come
    {
      va_list ap; // create a va_list to store extra arguments
      va_start(ap, args); // tell C the name of the last fixed argument
      int i;
      for (i=0; i<args; i++) // read off the variable arguments, one at a time
      {
        printf("argument: %i\n", va_arg(ap, int));
      }
      va_end(ap); // end the list
    }

    print_ints(3, 79, 101, 32);

> A **macro** is used to rewrite your code before it's compiled. The macros you're using here (`va_start`, `va_arg`, `va_end`) might look like functions, but they actually hide secret instructions that tell the *preprocessor* how to generate lots of extra smart code inside your program, just before compiling it.

The reader then solves the problem of calculating drink tabs with the use of `enum`s and varadiac functions.
