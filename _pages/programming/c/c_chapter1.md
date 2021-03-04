---
title: "Linux & C Programming"
permalink: /lectures/c_chapter1/
---

## Chapter 1

### Installation and setups

- VM set up
- Create a git branch
  - `git checkout -b <ID-week1>`
  - Which is a shorthand for:
  ```sh
  git branch <ID-week1>
  git checkout <ID-week1>
  ```
  - add / commit and push
  ```
  git add .
  git commit -m "MESSAGE"
  git push origin <ID-week1>
  ```
  - Open a (draft) merge request on Gitlab to merge your branch into `main` branch.

### Shell basics

- `ls`
  - list files in current directory
- `pwd`
  - print working directory
- `cd`
  - change working directory
  - `.` means current directory
  - `..` means parent directory
    - ex) `cd ../..`
  - with no argument: move to user's home directory
- `cat`
  - w/ one argument: `cat FILENAME` - print the contents
  - w/o argument: read from stdin and print to stdout
- `less`
  - shell file viewer
  - w/ one argument: view the file
    - use arrow keys to scroll up/down
    - `q` to quit
    - `/` to search by words
    - `h` for help

### More on shell commands

- `#` is the comment character in the shell
- `echo`: takes arguments and prints(echos) them out
- `man`
  - takes a command name as an argument
    - ex) `man ls`
  - opens up a less viewer to read the manual about the command
- `cp`: copies files
  - takes two arguments: source and destination
    - ex) `cp A B` makes a new filed called `B` with the same contents as `A`
- `mv`: moves(renames) files
  - takes two arguments: source and destination
- `nano`: opens up a shell editor to edit files in terminal (kind ver. of Vim)
  - one argument: file to edit
  - in `nano`, `^O`(`Ctrl-O`) to save
  - `^X` to quit
- `wc`: word counter
  - takes file name as an argument
  - if no file name is given, it uses `stdin`
  - reports line numbers, words, and characters in the file(or input)
- redirection
  - if a command contains `> file`, the when the command prints to stdout, the output is redirected to `file` instead
    - ex) `ls > file` -> make a file with the output of `ls` command
  - `< files` works the other way, it reads the given file and prints it to the terminal
- pipelines
  - combine two commands by sending the output of one into the input of the other
    - ex) `ls | wc` counts lines, words, characters of the output of `ls` command

### Hello (C) World! - C basics

```c
#include <stdio.h>

int main() {
  printf("hello world!\n");
  return 0;
}
```

- In this course, we use `clang374`, a custom compiler, to compile.
  - ex) `clang374 -o hello hello.c`
  - `-o` means "hey compiler, write the executable program to a file called `hello`
- To run the program, do `./hello`
- `#include <stdio.h>` imports the **STD**andard **I**nput/**O**utput library
- C programs are organized as a set of functions, not classes/methods
  - `main` function is a top-level thing in the file, not inside a class
- `main` returns an `int` in C
  - returning `0` means "success" and any non zero value indicates failure
- `printf`:

```c
printf("hello\n");
```

- it does not automatically append a newline
- print the text to `stdout`
- `getc` takes an argument and read one character(!) from that file
  - return type of `getc` is `int`
  - it returns a special value `EOF` (End Of File), which indicates the end of input(or file)
- `putc` takes two argument: a character and a file - writes given charcter to that file

# Week 2

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
