# Chapter 7: functions

## What does this chapter cover?

- Introduction to simple functions
- Working with `main`
- Understanding recursion

### 7.1 Simple functions

This chapter breaks down what it means to make a prototype of a function.

### 7.2 `main`

This section talks about the two main prototypes of `main`, and introduces customization with `argc` and `argv` parameters. Best practices for terminating `main` are also introduced.

### 7.3 Recursion

Here's code for finding the GCF or greatest common factor of two numbers (page 84):

```c
size_t gcd2(size_t a, size_t b) {
    assert (a <= b);
    if (!a) return b;
    size_t rem = b % a;
    return gcd2(rem, a);
}
```

This example shows the readers the beauty of recursion. Takeaways in this section relate to properly designing a recursive algorithm. The diagram on page 85 is very clear and helpful.

The chapter suggests that to ensure that a <= b from the onset, we use a wrapper function for the first call:

```c
size_t gcd(size_t a, size_t b) {
  assert(a);
  assert(b);
  if (a < b)
    return gcd2(a, b);
  else
    return gcd2(b, a);
}
```

> Takeaway 1.7.3.3  *Ensure the preconditions of a recursive function in a wrapper function.*

Page 87 has a visual for a recursive implementation of the Fibonacci sequence.

> Takeaway 1.7.3.4  *Multiple recursion may lead to exponential computation times.*

There are other implementations of the Fibonacci sequence that use a sort of cache to avoid doing the same computations over and over again and to increase runtime.

#### Challenge 9 (factorization)
Print out all of the prime factors of the number N.
