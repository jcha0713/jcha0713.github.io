---
title: "Linux & C Programming"
permalink: /lectures/c_chapter1/
---

## Basic of shell & C

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
