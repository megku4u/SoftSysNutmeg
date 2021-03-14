# Chapter 5: Structs, Unions, and Bitfields

## Outline
- Structs
  - Declaration
  - Implementation
  - Using in a function with pointers
- Unions
  - Compare to Structs



Chapter 5 starts by presenting a case where passing multiple parameters related to the same thing makes code messier. In this scenario, the program is passing multiple parameters related to one fish. The book uses the language "real-world *thing*" to refer to the object that all of these attributes are for.

The book switches to a "Cubicle conversation" where three people talk about the need for a new data structure. (Personally, I think this is a bit unnecessary.)

## Structs Intro

The fish example is continued with the introduction of **`struct`**s, which are short for **structured data type**.

    struct fish {
      const char *name;
      const char *species;
      int teeth;
      int age;
    };

    void catalog(struct fish f) {
      ...
    }

    struct fish snappy = {"Snappy", "Piranha", 69, 4};

    catalog(snappy);

The content that stands out on page 220 is the two bullets associated with the definition of a `struct`:

> - It's fixed length.
> - The pieces of data inside the struct are given names.

And the biggest takeaway in this chapter so far is the following:

> Wrapping parameters in a struct makes your code more stable.

There's a side section on page 221 that demonstrates the versatility of the `struct` by adding another field to the struct.

The chapter goes to show how to read fields using the `.` operator.

    printf("Name = %s\n", snappy.name);

After explaining the implementation of structs, the chapter dives into how `struct`s work in memory, using block-like visuals to display how the computer needs to make space for the **instance** of the struct based on the **template** that was provided.

> Remember: when you're assigning struct variables, you are telling the computer to copy data.

This is where the book introduces **nesting** of `structs` by adding a new `struct` to the fish `struct`.

    struct preferences {
      const char *food;
      float exercise_hours;
    };

    struct fish {
      const char *name;
      const char *species;
      int teeth;
      int age;
      struct preferences care;
    };

    struct fish snappy = {"Snappy", "Piranha", 69, 4, {"Meat", 7.5}};

    printf("Snappy likes to exercise for %f hours", snappy.care.exercise_hours);

After these and other exercises are carried out, the reader is introduced to `typedef` to shorten code and increase legibility. The example finally shifts away from the fish and uses cell phones instead:

    typedef struct cell_phone {
      int cell_no;
      const char *wallpaper;
      floar minutes_of_charge;
    } phone;

There's a side panel to elaborate on considering what the **alias** will be, and clarifying the difference betwen the name of the `struct` and the name of the *type*, though the book has decided to keep that logic pretty high-level. It's also somewhat not obvious that if you have an alias you can have an anonymous struct (hidden in the "there are no Dumb Questions" section).

### Structs and Pointers

Now the book covers updating, or **setting**, the value of `struct`s. But the book also stretches out the example of what happens by default with functions, which is that the values get copied into a new `struct`, rather than the original struct being modified. This scenario is detailed with the use of a turtle example before reintroducing pointers as a way to modify existing structs.

With a quick exercise, the chapter takes a lot of space to talk about the need for parentheses when referencing fields from a pointer to a `struct`.

**(\*t).age != \*t.age**

> So be careful with your parentheses when using structs - parentheses really matter.

Once this principle is introduced, only then is the new syntax for pointers and structs introduced.

    // These two expressions are the same
    (*t).age
    t->age // "The age field in the struct that t points to"

There is an exercise that looks like a bank safe to help practice with the new pointer notation, which may be helpful but may leave readers needing more examples.

## Unions

With the fruit example, the chapter makes the argument for not making a struct for every type of "quantity", especially if only one value is meant to be set.

- It will take up more space in memory
- Someone might set more than one value
- There's nothing called "quantity"

page 247 shows the visual difference between a struct and a  union using the block-style visuals, which I personally think are very helpful in conveying an easily confusing topic in a concise way.

    // A union example with quantity
    typedef union {
      short count;
      float weight;
       float volume;
    } quantity;

    // Initialization
    quantity q = {4} // set count to 4

    quantity r = {.weight=1.5}

    quantity s;
    s.volume = 3.7;

> Remember, whichever way you set the union's value, there will only ever be **one piece of data stored**.

With this established, code examples can be given using a union in a struct, which they often are.

    typedef struct {
      const char *name;
      const char *country;
      quantity amount;
    } fruit_order;

    fruit_order apples = {"apples", "England", .amount.weight=4.2};
    printf("This order contains %2.2f lbs of %s\n", apples.amount.weight, apples.name);

"Mixed-Up Mixers" is an exercise (fridge-magnet-style) for familiarizing the reader with the order of fields for structs that use unions. While easier to process in the physical book, it may be difficult to interact with as a PDF. In the corner of this exercise there is another ("BE the Compiler") exercise that highlights the importance of declaring the values of a struct on the same line as the declaration, or else the code will think the values represent an array.

## Enums

Enums are briefly introduced with the use of a code exercise. They are elaborated on a bit in a dialogue called "Overheard at Head First Lounge" which is a conversation between `union`, `struct`, and `enum`... which may feel like a drawn out way of repeating already given information.

## Bitfields

In the example in the chapter, **bitfields** are presented as an alternative to representing a simple yes/no scenario as a `short` to save space.

There's a short section to give context between converting between hexadecimal and binary.

>  A **bitfield** lets you specify *how many bits* an individual field will store.

There's a side note that bitfields should usually be grouped together because the compiler might have to pad a bitfield to the size of a word if it finds a bitfield on its own.

There's an exercise to get readers familiar with the number of bits they need to store enough information related to the field.

    typedef struct {
      unsigned int first_visit:1;
      unsigned int come_again:1;
      unsigned int fingers_lost:4;
      unsigned int shark_attack:1;
      unsigned int days_a_week:3;
    }
