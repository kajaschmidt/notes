---
layout: page
title: "C Crash Course"
category: introprog
date: 2018-10-15 23:30:31
order: 2
---

# 1. ["hello, world"](https://isis.tu-berlin.de/pluginfile.php/1088795/mod_resource/content/2/ws1819-ckurs-tag1-hello-world.pdf)

### C
* Entwickelt zwischen 1969 und 1973 von Dennis Ritchie (Bell Labs); Touring-Award Gewonnen
* Standardisierung:
  * ANSI C Standard 1989 durch American National Standards (wurde standardisiert)
  * Update 1999 (C99)
  * Update 2011 (C11)
* Systemsprache für systemnahe Programmierung (man darf alles tun, muss aber aufpassen was man tut)
* Eng mit Unix verbunden

### Computersysteme
Bestandteile um Anwendungsprogramme auszuführen:
  * Hardware (Prozessor, Arbeitsspeicher)
  * Software (Betriebssystem, Textverarbeitungsprogramme, ...)

### Create, Compile, Execute

1. **Create and save .c file** in directory with source code
  ```cpp
  #include <stdio.h> /* imports (libraries indicated by ".h"); stdio = "standart input output" ("ea" Eingabe/Ausgabe auf Deutsch) */
  #include <stdlib.h>
  int main() {
    printf("hello, world!\n");
    exit(0);
  }
  ```
  - Backslash `\` indicates that following letter is a command, not a (string) character
  - Editors: emacs for Ubuntu
  - `main`: function, indicated by `{}`, which contains commands
  - Hat die Funktion `main` kein Rückgabewert, sagen wir ihm das mit der Vorgabe `void main`

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

# 2. [Die ersten Schritte](https://isis.tu-berlin.de/pluginfile.php/1095843/mod_resource/content/2/ws1819-ckurs-tag2.pdf)

#### Algorithmus vs. Programm
<span style="color:red">__*Def*__ Algorithmus:</span> Liste von Anweisungen, die Essenz eines Programms und wird in Pseudocode aufgeschrieben

**Wichtige Aspekte:**
1. Korrektheit
2. Vollständigkeit
3. Komplexität
4. Effizienz
5. Terminierung

**Pseudocode**
```
m = 0;
p = 1;
while (p<n)
  Ausgabe: "2^m ist p";
  m = m + 1;
  p = p * 2;
```

**C-Code**
```cpp
#include <stdio.h>
int main() {
  m = 0;
  p = 1;
  while (p < n) {
    printf("2^%d ist %d\n", m, p);
    m = m + 1;
    p = p * 2;
  }
}
```

### C-Sprachelemente

**Speziell in C:**
```cpp
int a = 0;
if ( a ) {
  printf("True\n");
}
```
Dann gibt dieses Programm *nichts* aus (anders als in anderen Programmiersprachen)

* Typen
  * `int`
    * 32 Bit
    * Range: [–2'147'483'648, 2'147'483'647]
    * printf Platzhalter: `%d`
  * `char`
    * printf Platzhalter: `%c`
  * `float`
  * `void`
  * ...
* Mathematische Operationen
  * `+`
  * `=`
  * `%` (Modulo; Rest nach Division)
  * ...
* Kontrollstrukturen
  * `while`
  * `for`
  * `if`
  * `else`
  * ...
* Kommentare
  * `/* <comment> */`
  * `//`

**Einzelzeichen**
* `%c`: char
* `%d`: int
* `%u`: unsigned int
* `%lu`: unsigned long
* `%ld`: long int
* `%lld`: long long int
* `%f`: float
* `%lf`: double
* `%s`: char * / string

**Sonderzeichen**
* `\n`: new line
* `\t`: tabulator
* `\0`: EOS; Endzeichen in String

**Reservierte Zeichen**
* `\'`: '
* `\"`: "
* `\\`: \
* `%%`: %

# 3. 

## Vocab
| **Deutsch** | **English** | **Definition** |
---
| Algorithmus | Algorithm | Liste von Anweisungen; die Essenz eines Programms; wird in Pseudocode aufgeschrieben |
| --- | Compiler | translation program, translates source code to machine code for a processor |
| Kernbetriebssystem | Kernel |
| Quellcode | Source code | unformatted ASCII text; should be well documented |
| --- | LLVM | ... |
| --- | ASCII | ... |
| --- | GCC | ... |
| Pseudocode | Pseudocode | ... |

## Syntax & Semantics
| **Component** | **Detail** | **Example** |
---
| Function | indicated by `()` and followed by `{}` which contains commands/variables essential for the function | `main()`, `if (<condition>) {<block-to-execute>}`|
| Block | `{}`


## Further shell commands
```shell
// echo
echo $SHELL
echo $?

// SVN
svn --username kms743 checkout https://teaching.inet.tu-berlin.de/services/svn/playground-wise1819 // installiert repo
svn status // check status
svn add <file/directory> // add changes made
svn commit -m '<commit-message>' // commits (and seems to push) changes
svn log -r1:HEAD // see commit log

// other
more <Dateiname> // druckt Dateiinhalt aus --> in-terminal text editor?
cat <Dateiname> // auch ein in-terminal text editor ?

```
