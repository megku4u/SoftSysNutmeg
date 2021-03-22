# Chapter 2.5: Strings

## What does this chapter cover?

- <string.h> (some of it)
- arrays of arrays and arrays of pointers
- pointer arithmetic

## Array of Arrays

Using the example of track names, the chapter shows how you can make an array of arrays. In this case, it is an array of strings.

    char tracks[][80] = {
      "I left my heart in Harvard Med School",
      "Newark, Newark - a wonderful town",
      "Dancing with a Dork",
      "From here to maternity",
      "The girl from Iwo Jima",
    };

The book has a nice visual of this by making a grid for the reader to imagine the characters being stored.  The book also gives examples on how to index with the array of arrays:

    tracks[4] // "The girl from Iwo Jima"
    tracks[4][6] // 'r'

## The `string.h` library

This is where Head First C introduces the name **header** file.

The book saves verbage by listing several string functions from `string.h` without explaining them, but rather asking the reader to match them to their purpose (the function names are pretty self explanatory anyway).

- `strchr()`: find the location of a character inside a string
- `strcmp()`: compare two strings
- `strstr()`: find the location of a string inside of another string
- `strcpy()`: copy one string to another
- `strlen()`: find the length of a string
- `strcat()`: concatenate two strings

For the jukebox example that is extended over this chapter, the exercise demonstrates how to use `strstr()`. The exercises that follow help to build the program.

There's another built-in exercise to demonstrate **pointer arithmetic** by reversing a string.

There are also *arrays of pointers* in the C world,

    char *names_for_dog[] = {"Bowser", "Bonza", "Snodgrass"};

and these can be accessed just like how arrays of arrays can be accessed.

There's a "crossword" exercise to help grapple with accessing values in an array of pointers.
