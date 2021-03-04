---
title: "Linux & C Programming"
permalink: /lectures/c_chapter2/
---

## More C basic and bitwise operations

### Defensive programming (Just like defensive driving)

```c
#include <stdio.h>

int main() {
  int c;
  int n = 0;
  while ((c = getc(stdin)) != EOF) {
    if (c == '\n') {
      printf("%d", n);
      n = 0;
    } else {
      n++;
    }
  }
  return 0;
}
```

- C is not a kind language
- one needs to constantly be slightly paranoid and vigilant about mysterious errors.
- In this program that counts the length of every line, one might consider
  - how to handle last line of file when there is no `\n`
  - What if we forget to initiate the count?

### Number representation

- The machine operates on numbers using a binary (base 2) representation.
- Every integer type in C uses a certain number of binary digits
- Example: No. 5 represented in 4 bit binary is 0101
  - In binary we have the ones place, twos place, fours place, etc., for each power of two.
  - 5 = 4 + 1

### Bitwise operations

- It is kinda useful to think of an integer as a number versus as a sequence of bits.
- Several operations available in C are best thought of as operating on sequences of bits. we call these operations the "bitwise operations" because they operate "bit by bit".
- Bitwise and
  - It uses the single ampersand character in C: `&`
  - takes two sequences of bits and lines up their columns, and computes the boolean "and" of each column to get the corresponding bit in the output.
  - The output bit is 1 if both input bits in that column are 1, otherwise that column's bit is a zero.
  - for example, 5 & 12 = 4 because we can write out the bits like this
    ```
      0101
    & 1100
    ------
      0100 = 4
    ```
