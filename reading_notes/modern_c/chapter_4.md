# Chapter 4: Expressing computations

## What does this chapter cover?

- Performing arithmetic
- Modifying objects
- Working with booleans
- Conditional compilation with the ternary operator
- Setting the evaluation order

> Takeaway 1.4.0.1  *The type* `size_t` *represents values in the range* [0, `SIZE_MAX`].

Page 30 offers a nice table of all operators as well as their inputs and outputs.

> Takeaway 1.4.1.1  _Unsigned arithmetic is always **well defined**_

The discussion around operations also brings up the existence of mathematical **overflow**. The following takeaways center on overflow.

One helpful style tip that is offered is the following takeaway:

> Takeaway 1.4.2.3  *Never modify more than one object in a statement.*

Logic operators, like `&&` and `||`, are now introduced, with the term **short-circuit evaluation** to pair with them.

The ternary (conditional) operator follows the and/or discussion:
```c
size_t size_min(size_t a, size_t b) {
    return (a < b) ? a : b;
}
```
> Takeaway 1.4.5.1  `&&`, `||`, `?:`, and `,` evaluate their first operand first.

The `,` operator is noted as a trap for beginners and is rarely used in clean code. For example, `A[i, j] == A[j]`.

> Takeaway 1.4.5.3  Most operators don't sequence their operands.

Neither do functions (in terms of their argument expressions).

### Challenge 4: Union Find

This is a pretty involved challenge, focusing on implementing multiple functions on a base set.
