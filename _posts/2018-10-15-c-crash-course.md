---
layout: page
title: "C Crash Course"
category: introprog
date: 2018-10-15 23:30:31
order: 2
---

# ["hello, world"](https://isis.tu-berlin.de/pluginfile.php/1088795/mod_resource/content/2/ws1819-ckurs-tag1-hello-world.pdf)

## C
* Entwickelt zwischen 1969 und 1973 von Dennis Ritchie (Bell Labs); Touring-Award Gewonnen
* Standardisierung:
  * ANSI C Standard 1989 durch American National Standards (wurde standardisiert)
  * Update 1999 (C99)
  * Update 2011 (C11)
* Systemsprache für systemnahe Programmierung (man darf alles tun, muss aber aufpassen was man tut)
* Eng mit Unix verbunden

## Computersysteme
Bestandteile um Anwendungsprogramme auszuführen:
  * Hardware (Prozessor, Arbeitsspeicher)
  * Software (Betriebssystem, Textverarbeitungsprogramme, ...)

## Create, Compile, Execute

1. **Create and save .c file** in directory with source code
  ```cpp
  #include <stdio.h> /* imports (libraries indicated by ".h"); stands for "standart input output" ("ea" Eingabe/Ausgabe auf Deutsch) */
  #include <stdlib.h>
  int main() {
    printf("hello, world!\n");
    exit(0);
  }
  ```
  - Backslash `\` indicates that following letter is a command, not a (string) character
  - Editors: emacs for Ubuntu

2. **Compile .c file to a programm** using gcc
- <span style="color:red">__*Def*__ Compile document:</span> converting programming language to binary code to enable processor to read what it's supposed to execute.
- Execute compile-command using `gcc -Wall <name>.c -std=C11 -o <program-name>` to compiles the .c file into a programm called (`<programm-name>`)
  - Flags (optional)
    - `-o`: output
    - `-Wall`: ensures that you see *all* error messages (even if you can still execute the code)
    - `std=c11`: makes compiler "nicer"
- Compilers for C: ggc (GNU compiler), clang (language family frontend for LLVM)
- Compiler phases
  - Preprocessor: Aufbereitung
  - Compiler: Übersetzt C in gcc/llvm (intermediate representation IL)
  - (Optimizers) optimiert sprachunabhängige llvm il
  - (Backend) übersetzt llvm il in assemblercode
  - Assembler übersetzt assemblercode in maschinensprache
  - Linker nachbearbeitung / kombination verschiedener module

3. **Execute programm** with command `./<programm-name>` using processor


## Vocab
* Compiler: translation program, translates source code to machine code for a processor
* Kernbetriebssystem – Kernel
* Quellcode – Source code | unformatted ASCII text; should be well documented
* LLVM
* ASCII
*

## Further shell commands
```shell
echo $SHELL
echo $?

```
