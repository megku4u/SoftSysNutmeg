# Chapter 2: Memory and Pointers

## What does this chapter cover?

- Pointers
- the structure of memory allocation
- array variables and functions
- `sizeof`
- `scanf` and `fgets`
- string literals

## Pointers

This chapter starts right off by introducing **pointers** as a **form of indirection**. There's also several warnings on page 42 that the reader should "go slowly".

1. Instead of passing around a whole copy of the data, you can just pass a pointer.
2. You might want two pieces of code to work on the same piece of data rather than a separate copy.

These two points are illustrated using people having conversations.

### Understanding Memory Allocation

The next page aims to provide more context for pointers by giving a visual for the computer's memory. The visual of the stack structure is a helpful one, although there aren't any examples of values stored in the heap.

    int y = 1; //Stored in globals section

    int main() {
      int x = 4; //Stored in stack
      return 0;
    }

> That's why an address is also called a ***pointer***, because it ***points*** to the variable in memory.

Now, the `&` operator is introduced:

    printf("x is stored at %p\n", &x); // %p prints in hex format

An exercise is then used to show the utility of pointers with functions (the "Bermuda Rectangle"). The code won't work in terms of updating the ships location because of the following:

> C sends arguments as values. When you call a function, you don't send the *variable* as an argument, just its *value*

The chapter further uses the analogy of lockers to demonstrate how pointers work.

> This is one of the main reasons for using pointers - to let functions *share* memory.

    int address_of_x = &x; // pointer variable for an address that stores an int

    int value_stored = *address_of_x; // read the contents at the memory address given by address_of_x.

    *address_of_x = 99; // change contents of original x value to 99

Now that this context is provided, the book returns to the ship example to have the reader fix the code using pointers.

## Array Variables

The reader is shown a new code snippet related to fortune cookies to demonstrate the use of strings as function parameters.

    void fortune_cookie(char msg[]) {
      printf("Message reads: %s\n", msg);
    }
    char quote[] = "Cookies make you fat";
    fortune_cookie(quote);

The function `size_of()` does something weird with arrays, though, which transitions to the point that array variables are similar to pointers in some ways.

> The computer will set aside space on the stack for each of the characters in the string, plus the \0 end character. But it will also associate the **address of the first character** with the variable. Every time the array variable is used in the code, the computer will substitute it with the address of the first character in the string. In fact, the array variable is *just like a pointer*.

The book goes into a dialogue with the "computer" to elaborate on the underlying interpretation of the above code. The degree of usefulness for this page (55) may vary from reader to reader.

In the "there are no Dumb Questions" section, there is a bit of explanation as to the difference between a function and an operator as well as other questions.

Another exercise (NOTE: I'm not a fan of this one at all) called "The Mating Game" (see what I mean) is used to show indexing and pointers with arrays by doing a lot of it. I think it would have been really nice to see what the array looked like after all of the modifications.

### Differences Between Array Variables and Pointers

There are three points the book covers in a bullet-like list.

    char s[] = "How big is it?";
    char *t = s;

1. `sizeof(an array)` is the size of an array.

        sizeof(s) // = 15

        sizeof(t) // = 4 or 8 (pointer)

2. The address of the array... is the address of the array.

        &s == s
        &t != t

3. An array variable can't point anywhere else.
        s = t; // Will give compile error


There's a note on the side of page 59 about pointer **decay**.

> Every time you pass an array to a function, you'll decay to a pointer, so it's unavoidable.

The book uses a "Five-Minute Mystery" to introduce the idea of many ways to index an array.

    int drinks[] = {4, 2, 3};

`drinks[0] == *drinks`

`drinks[2] == *(drinks + 2) = *(2 + drinks) + 2[drinks]`

If you're able to make the above logical leap based on the commutative property of addition, then "solving the mystery" will be very easy.

There's a half-page dedicated to understanding why pointers have types.

> The reason is that pointer arithmetic is *sneaky*. A `char` occupies **1 byte of memory** ... `int`s usually take **4 bytes of space**...

> Pointer types exist so that **the compiler knows how much to adjust the pointer arithmetic.

### `scanf` and `fgets`

With this established, we can revisit the function `scanf()` to understand how it works. Because `scanf()` is updating the contents of the array it is passed, it requires a pointer as a parameter.

> Functions that need to *update* a variable don't want the value of the variable itself - they want its **address**.

    int age;
    printf("Enter your age: ");
    scanf("%i", &age);

While we're talking about `scanf()`, the chapter decides to dive into the limitations of `scanf()`.

> `scanf` can cause buffer overflows if `scanf` writes data beyond the end of the space allocated to the array.

`fgets` is the alternative as it must be given a maximum length.

    char food[5];
    printf("Enter favorite food: ");
    fgets(food, sizeof(food), stdin); // sizeof includes the string null character

There is a note to be careful with using `sizeof` with `fgets` - you need to be sure that it will return what you actually want (ie. using pointers instead of array variables).

Page 68 is a side-by-side comparison between the two methods.

> If you need to enter *structured data* with several fields, you'll want to use `scanf()`.

> If you're entering a *single unstructured string, you'll want to use `fgets()`.

## Immutability of String Literals

That aside, the chapter moves to the immutability of strings using a card game example.

The visual of computer memory as layers in the earth returns, but this time, the cards variable in the stack points to the string literal stored in the constants section of memory.  This is a very drawn out example, which makes sense given how new these concepts may be for students.

There's a "Geek Bits" section suggesting that setting pointers to string literals should be done with the `const` keyword

    const char *s = "some string";

so that a compile error will be raised if you try to modify it.

Another "Five-Minute Mystery" is used to help explore that multiple pointers can point to the same thing, and if the value gets changed at that location, then all pointers will point to that update information.

## Memory Memorizer

The image on page 80 is a very nice reference to help memorize the order of sections in memory.
