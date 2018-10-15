---
layout: page
title: "C Crash Course"
category: introprog
date: 2018-10-15 23:30:31
---

## Basic process

1. Create .c file and save it in directory

```cpp
#include <stdio.h> // imports (libraries indicated by ".h"); stands for "standart input output" ("ea" Eingabe/Ausgabe auf Deutsch)

int main() {
  printf("Hello, world!")
}
```

2. Compile .c file using gcc
- *Compile document:* convert programming language to binary code for computer to be able to read what it's supposed to execute.
- Execute compile-command using `gcc <name>.c -o <program-name>` or `gcc -Wall <name>.c -o <program-name>`. This compiles the .c file into a programm called (`<programm-name>`)
  - `-o`: output
  - `-Wall`: ensures that you see *all* error messages (even if you can still execute the code)

3. Execute programm with command `./<programm-name>`
