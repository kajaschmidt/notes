---
layout: page
title: "C Crash Course"
category: introprog
date: 2018-10-15 23:30:31
order: 2
---

## Vorlesungsmaterial
1. ["hello, world"](https://isis.tu-berlin.de/pluginfile.php/1088795/mod_resource/content/2/ws1819-ckurs-tag1-hello-world.pdf)
2. [Die ersten Schritte](https://isis.tu-berlin.de/pluginfile.php/1095843/mod_resource/content/2/ws1819-ckurs-tag2.pdf)
3. [Kontrollstrukturen & Funktionen](https://isis.tu-berlin.de/pluginfile.php/1098309/mod_resource/content/3/ws1819-ckurs-tag3.pdf)
4. [Rekursive Funktionen & Bibliotheken](https://isis.tu-berlin.de/pluginfile.php/1101335/mod_resource/content/2/ws1819-ckurs-tag4.pdf)
5. [Arrays & Adressen](https://isis.tu-berlin.de/pluginfile.php/1106762/mod_resource/content/1/ws1819-ckurs-tag5.pdf)
6. [Dynamische Speicherverwaltung](https://isis.tu-berlin.de/pluginfile.php/1109686/mod_resource/content/1/ws1819-ckurs-tag6.pdf)

#### C Code
* Entwickelt zwischen 1969 und 1973 von Dennis Ritchie (Bell Labs); Touring-Award Gewonnen
* Standardisierung:
  * ANSI C Standard 1989 durch American National Standards (wurde standardisiert)
  * Update 1999 (C99)
  * Update 2011 (C11)
* Systemsprache für systemnahe Programmierung (man darf alles tun, muss aber aufpassen was man tut)
* Eng mit Unix verbunden

#### Computersysteme
Bestandteile um Anwendungsprogramme auszuführen:
  * Hardware (Prozessor, Arbeitsspeicher)
  * Software (Betriebssystem, Textverarbeitungsprogramme, ...)

#### Create, Compile, Execute

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


##### Algorithmus vs. Programm
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

#### C-Sprachelemente

**Speziell in C:** Diese Programm gibt *nichts* aus (anders als in anderen Programmiersprachen)

```cpp
int a = 0;
if ( a ) {
  printf("True\n");
}
```

#### Syntax Beschreibung: Backus-Naur form
- B&N wird zur Syntax-Definition von Programmiersprachen genutzt.
- Strukturierte Programmierung: "pretty printing"
  - Modularisierung
  - Kapselung
  - Dokumentation
  - Vermeidung von komplexen Kontrollstrukturen

```cpp
<block> ::= {<statements>}
<statements> ::= <statement> |
    <statements> <statement>
```

##### `i++ vs. ++i`
Semantisch sind `i++`  und `++i` korrekt, syntaktisch sind sie aber unterschiedlich
```cpp
j = ++i; // Inkrementiert i zuerst, dann weist es i zu j zu
j = i++ // Weist zuerst i zu j, dann inkrementiert es i
```

##### If-Statements and Loops
- While und For Loops sind semantisch äquivalent

```cpp
// For loop
int i = <start>; // Gute Programmierformatierung den Integer bereits vor dem for-loop zu initiieren!
for (i = <start>; i <= <Abbruchkondition>; i++) {
  <block>
}

// While loop
int i = <start>;
while (i <= <Abbruchskondition>) {
  <block>
  i++;
}

// if statement
if (<Kondition>)
    <Block>
  else if (<Kondition>)
    <Block>
  else
    <Block>
```

#### Funktionen

- Modularisierung
- Kapselung
- Dokumentation
- Vermeidung von komplexen Kontrollstrukturen
- Variablen einer Funktion werden nur innerhalb der Funktion gespeichert, nicht außerhalb (--> in dem Fall kann mein Speicheradressen nutzen)

**Funktion definieren**
```cpp
// function to do ...
int max(int a, int b) {
  if (<condition>)    // condition
    <block>;
    return <content>; // explain return
  else
    <block>;
    return <content>; // explain return
}

// Ex. 1: function to implement addition
int add(int x, int y) {
  int result;
  result = x + y;

  return result;
}

// Ex. 2: function to implement subtraction
int sub(int x, int y) {
  return x - y;
}

// Ex. 3: function to implement powers
int power(int x, int n) {
  if ( !(x >= 0 && n >= 0) ) {
    return -1;
  }
  int result = 1;
  for (int i = 1, i == n; i++) {
    result *= x; // result = result * x
  }
  return result;
}
```

##### Rekursive Funktionen
- Funktion ruft sich selber auf

Beispiel:
```cpp
int recursion(int a) {
  if (a > 41) { //Abbruchbedingung
    return a;
  }
  return recursion(a+1) //rekursiver Aufruf
}
```
Diese Funktion ist *nicht* endlos, da a sich nicht selber überschreibt. Sobald `a > 41` wird `a` ausgedruckt, und das war es dann.

Beispiel: Faktorial Funktion
```cpp
int fak(int n) {
  if (n <= 1) { // Abbruchbedingung
    return 1;
  } else {
    return n * fak(n - 1); // rekursiver Aufruf
  }
}

// ODER
int fak(int n) {
  if (n >= 1) return 1;
  return n * fak(n - 1);
}
```

##### Scanf
```cpp
int lese_int() {
    int number = 0;
    int ret = 0;
    char c;
    printf("Bitte geben sie eine Nummer ein: ");
    while(ret == 0) {
        ret = scanf("%d%c", &number, &c);
        while (c != '\n' && getchar() != '\n') { };
        if (ret == 0)
            printf("\nDas war keine Nummer. Versuchen sie es erneut: ");
    }

    return number;
}
```
- or check out "getchar" function


**Komplexität:** <br>
z.B. eine Baumstruktur zu nutzen um Zahlenreihen erst zu sortieren, und dann zu filtern. Dadurch kann man viel effizienter Programmieren. Solche Konstrukte zu erkennen und zu erstellen machen gute Programmierer aus.


#### Bibliotheken

**Modularisierung:** C Programme bestehen aus einer Menge von FUnktionen die in verschiedene Module (Dateien) getrennt werden. Dies dient der Übersichtlichkeit, Erweiterbarkeit, Wiederverwendbarkeit und Wartbarkeit des Codes. <br>
z.B. Statt `datei.c` zu nutzen welches eine `max()`-Funktion und `int main()`-Funktion beinhaltet, kann man mehrere Dateien erstellen:
* `name-header.h`- Bibliothek
* `name-main.c` - Hauptdatei (beinhaltet `#include "name-header.h"`)
* `name-function.c` - Funktion

##### Präprozessoren
* Bearbeitet die Direktiven
* Bspl: `#define, #include`
* z.b. `#define MAXLEN 10`

Note: um weitere Directories hinzuzufügen: explizit mittels `-L`für Bibliotheken und `-I` für Headerdateien beim Kompilieren angeben.

### Speicher

#### Speicher & Adressen von Variablen
- Speicher besteht aus Reihe von Bytes
  - `int` besteht aus 4 aufeinanderfolgenden Bytes
- Deklaration vs. Zuweisung einer Variablen (siehe Vocab-Liste)
- Arrays
  - Implizit ein Pointer
  - Haben eine fest definierte Länge; es gibt keine Möglichkeit auf mehr Speicher zuzugreifen nachdem sie definiert wurde
  - Sehr schnell
  - z.B. `char a[128];` oder `int b[5] = {3, 8, 2, 0, 9};` reserviert 128 bzw. 5 Bytes für die jeweiligen Arrays; Zugriff auf Werde mit Index (`a[57] = 98;`)
  - <span style="color:red">**Es gibt beim Zugriff auf Arrays keinerlei Überprüfungen auf dessen Grenzen!!!**</span> Sprich, der Compiler (das ist aber nur in C der Fall) schützt uns nicht davor auf Array-Felder zuzugreifen, die gar nicht existieren. Das treibt die Speichergröße in die Höhe. Deßwegen muss man selber testen ob die Array-Grenzen überschritten werden oder nicht.
    - In vielen Fällen ist das der Grund für eine Sicherheitslücke in einem Programm: die Indexe eines Arrays in C wurden nicht überprüft.

- **Call by Value:**
  - Parameterübergabe als Wert
  - Werte der Variablen werden übergeben
  - Werte der Variablen stehen als lokale Kopie zur Verfügung
  - Änderung sichtbar innerhalb der Funktion
- **Call by reference**
  - Parameterübergabe als Adresse
  - Adressen der Variablen werden übergeben
  - Adresse steht lokal zur Verfügung und Zugriff auf Speicherort der übergebenen Variable ist möglich
  - Änderungen sichtbar über die Funktion hinaus
  - Nutzt Pointers

##### Pointer und Adressen

- **Adressen**
  - `&<variable>`
  - Integervariable eines Arrays: hat eine Adresse im Array (z.B. der Prozessor übersetzt `a[0][0]` auf `0`). Der Compiler weist jedem Array, jedem Variablen etc. einen Speicherplatz im Prozessor zu. Das nennt man dann eine Adresse der Variablen.
  - Adressen werden als Hexadezimalzahlen dargestellt
    - `printf("%p", &number)` von Adressen/Pointer auf Variablen nutzen das Zeichen `%p`
- **Pointer**
  - `*<variable>` (oder `array[]`)

Folgende Beispiele zeigen wie man eine Variable neu definieren kann sie direkt zu referenzieren (sondern nur ihre Adresse) durch die Nutzung von Pointers und Adressen:

**EXAMPLE 1**
```cpp
#include <stdio.h>

int main() {

  // Define variables (and their adresses)
  int a, b;
  int *p1, *p2;
  a = 1; b = 17; p1 = &a, p2 = &b;

  // Before assigning a pointer
  printf("a = %d, b = %d, p1 = %d, p2 = %d\n", a, b, *p1, *p2 ); // output: a = 1, b = 17, p1 = 1, p2 = 17

  // After assigning a pointer
  *p1 = *p2;
  printf("a = %d, b = %d, p1 = %d, p2 = %d\n", a, b, *p1, *p2 ); // output: a = 17, b = 17, p1 = 17, p2 = 17

}

void add2 (int s, int a, int b) {
  s = a + b;
}
```

**EXAMPLE 2**
```cpp

// Adressen / Pointer
void add3 (int *s, int a, int b) {
  *s = a + b; // an die Adresse des int, weist den Wert von a + b zu
}

int main () {
  int x = 5, y = 3, sum = 0;

  add2(sum, x, y);
  printf(sum) // druckt sum = 0 aus weil die Variable s aus der add2-Funktion nicht gespeichert wird

  add3(&sum, x, y); // weise der Variablen "Sum" eine neue Adresse zu
  printf(sum) // druckt sum = 8 aus weil das * und das & Zeichen
}
```

**EXAMPLE 3**

```cpp
int main() {

  // Define int number
  int number = 5;
  printf("Nummer: %d, Adresse: %p\n", number, &number); // Output: Nummer: 5, Adresse: 0x7ffeef2008f4

  // Assign pointer to address of variable "number"
  int *pointer = &number;

  // Redefine pointer
  *pointer = 7;
  printf("Nummer: %d, Adresse: %p\n", number, &number); // Output: Nummer: 7, Adresse: 0x7ffeef2008f4

}
```

#### Dynamische Speicherverwaltung

Arrays haben eine feste Dimension mit festem Speicherort; Pointer müssen erst dynamisch allokiert werden.

##### Abstraktion
- Virtueller Speicher: Ein Bytearray
- Programmsicht
  - Theorie:
    - Jedes Programm hat seinen eigenen Speicher mit (potentiell) unbegrenzter Speichermenge
    - Zugriff auf Speicherbereiche ist gleich schnell
  - Praxis:
    - Physikalischer Speicher wird geteilt
    - Betriebssystem allokiert und verwaltet Speichers
    - Anwendungen sind speicherdominiert
    - Speicherhierarchie: Cache, RAM, Platte
    - Speicherzugriffsfehler sind besonders schwer zu finden da Effekte oft fern der Ursache sind

##### Effiziente Speicherverwaltung (für C Programme)

- Zuteilung von Speicher nach Bedarf (da Ressourcen begrenzt sind)
- Programmkomponente
  - C-Code (Programm)
  - Datenstrukturen
  - C-Bibliotheken, externe Funktionen

##### Dynamische Speicherallokation (in C)
- Zuteilung von Speicher nach Bedarf (da begrenzte Ressourcen)
- Problematiken
  - Compilezeit: währed des Compilieren
  - Laufzeit: während des Laufens des Programms

1. Implizite Speichernutzung:
- Sa wir nicht vorab wissen wie viel Speicher das Programm braucht, nutzen wir eine dynamisch wachsende Datenstruktur für die SPeicherung der Variablen ("User-Stack") <br>

2. Explite Speichernutzung:
- Speicher muss explizit wieder freigegeben werden
- z.B. `malloc` mit `#include <stdlib.h>` oder `calloc`

**Malloc**
- Gibt einen "nullpointer" zurück
- Ist `void` (generischer Typ)
- Hilfsfunktionen (mit #include <stderr.h>)
  - `errno`: Codes von 1 bis 127 mit Fehlern, siehe `errno.h`-Datei
  - `perrno`: eine für Menschen leserliche Fehlermeldung
  ```cpp
  #include <stdlib.h>
  void* malloc(size_t size)
  // return: Pointer zum Speicherblock mit mindestens size bytes
  ```
  - Errormessages ausdrucken:
  - `cat values.txt | HELLOWORLD >> result`: druckt stdout
  - `cat <values.txt | HELLOWORLD 2> result`: druckt stderr
  - `|`: Umleitung der Ausgabe in eine Datei (z.B. HELLOWORLD)

**Calloc**
- "clear allocation"


**Free**
-






---
## Vocab

| **Deutsch** | **English** | **Definition** |
| --- | --- | --- |
| Algorithmus | Algorithm | Liste von Anweisungen; die Essenz eines Programms; wird in Pseudocode aufgeschrieben |
| . | Compiler | translation program, translates source code to machine code for a processor |
| Kernbetriebssystem | Kernel |
| Quellcode | Source code | unformatted ASCII text; should be well documented |
| . | LLVM | ... |
| . | ASCII | Jedes Zeichen hat eine ASCII-Nummer, die in einen binären Code (xxx xxx {0,1}) umgewandelt wird. |
| . | GCC | ... |
| Pseudocode | Pseudocode | ... |
| . | Syntax | legt fest, welche Zeichenketten Teil der Sprache sind |
| . | Semantik | legt fest die Zeichenkette (Syntax) bedeutet |
| Deklaration einer Variablen | . | Speicherreservierung für Variable |
| Zuweisung einer Variablen | . | Belegung des Speichers mit dem Wert einer Variablen |

## Syntax & Semantics

- Bei Semantikfehlern kompiliert das Programm, gibt aber eine Warnung ab
- Bei Syntaxfehlern kompiliert das Programm nicht.

| **Component** | **Detail** | **Example** |
| --- | --- | --- |
| Function | indicated by `()` and followed by `{}` which contains commands/variables essential for the function | `main()`, `if (<condition>) {<block-to-execute>}`|
| Block | `{}` | . |
| Funktion hat eigentlich keinen Rückgabewert | Rückgabe alles OK == 0; Fehler != 0| `int add (int *sum, int a, int b)` |
| Funktion hat Rückgabewert | Rückgabe alles OK != 0; Fehler == 0 | `void *melloc(size_t size)` |
| Setzen des Fehlercode `errno` | `perrno` nutzen um Fehlercode/-meldung auf der Konsole via `stderr` auszugeben | . |

* Typen
  * `int`
    * 32 Bit
    * Range: [–2'147'483'648, 2'147'483'647]
    * printf Platzhalter: `%d`
  * `char`
    * printf Platzhalter: `%c`
  * `float`
  * `void`
  * Pointer: `*`
  * Adresse: `&`
  * Notiz: Boolean gibt es nicht; `int boolean = 0` repräsentiert `false`
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

**Casten:** Datentypen können umgewandelt werden durch ein sogenanntes "casten"


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

---

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
--> Keine globalen Variablen erstellen!
