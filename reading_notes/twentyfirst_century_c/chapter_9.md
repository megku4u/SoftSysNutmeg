# Chapter 9: Easier Text Handling

## What does this chapter cover?

### Making String Handling Less Painful with asprintf

`asprintf` allocates the amount of string space you will need and then fills the string. This is not part of the C standard, but is available on systems with the GNU and BSD library. It's elegant because `malloc` gets called for you, so there is no need to do the manual setup (as shown in code on page 186).

If `asprintf` is not available, using `vsnprintf` twice will do a good job.

### Security

Overwriting using `sprintf` = bad. `snprintf` limiting data written = good.

### Constant Strings
"The difference between constant and variable strings is subtle and error-prone, and it makes hardcoded strings useful only in limited contexts. I can’t think of a scripting language where you would need to care about this distinction."

The solution? `strdup()`.

```c
char *s3 = strdup("Thread");
```
In the above snippet, "Thread" is still hardcoded, but `s3` is a copy of that constant blob and can be modified.

### Extending Strings with asprintf

The code example on page 191 provides a form to handle an unknown number of strings of unknown length, as well as handling edge cases.

### A Paean to strtok

*Tokenizing* is defined as splitting a string into parts at delimiters. There is a function to do this called `strtok`, but the authors suggest that we consider it deprecated. This section goes into using the alternatives: `strtok_r` and `strtok_s`, depending on which standard you're using. There are several thorough code examples and annotations to go along with them in this section.

### Unicode

This section provides a lot of context around Unicode and how its standards have evolved. This is pretty text-dense.

The takeaways for the programmer are the following:
- Work out what encoding the host system is using
- Successfully store text somewhere, unmangled
- Recognize that one character is not a fixed number of bytes
- Have on hand utilities to do any sort of text comprehension

### The Encoding for C Code

UTF-8 was designed for the programmer, for many reasons outlined in detail in this chapter. Page 200 has a list of UTF-8 safe standard library functions.

### Unicode Libraries, etc.

*skip; out of scope of current SoftSys understanding*
