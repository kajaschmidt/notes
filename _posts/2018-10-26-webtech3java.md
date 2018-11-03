---
layout: page
title: "JavaScript"
category: webtech
date: 2018-10-26 12:15:45
order: 3
---

JavaScript
- Funktionale Programmiersprache
- Interpretersprache: bring das Programm zur Ausführung (z.b. Browser, Server) und überführt Code erst am Ziel in Maschinensprache (erspart Kompilierung)
- Dynamische Typisierung: Datentyp wird bei der Zuweisung *nicht* vordefiniert (so wie in C oder Java --> statische Typisierung)


  - Asynchrone Kommunikation
  - Nutzungsbeispiele
    - In-Browser Validierung von eingegebenen Daten


### Daten & Datentypen
**Daten:** Aneinanderreihung von Bits mit zugrundeliegendem Datentyp <br>
**Bits:** {0, 1} die als niedrige oder hohe elektrische Signale weitergegeben werden

##### Basic Data Types (Primitive Datentypen)
1. Numbers:
  * 64-Bit-Fließkommazahl (keine Differenzierung zwischen int und float)
  * 2^{64} = 18 Trillion (18 Nuller) Zahlen können dargestellt werden
    * inkl. Komma, Minus-Zeichen
    * Max. Nummer: 9 quadrillionen (15 Nuller)
  * `infinity`, `-infinity`, `NaN`
  * Arithmetische Operatoren: `+, -, *, /, %, ...`
  * Berechnungen mit ganzen Zahlen sind präzise, mit Dezimalzahlen nicht.
2. Strings
  * 16-Bit-Zeichen (nach Unicode: USC-2 / UTF-16 Kodierung)
  * 2^{16} Charaktere
  * Operator: `+`
  * Erstellt mit ``, "", oder ''
    * ``: template literals, die auch in-line Berechnungen machen können (z.B. `half of 100 is ${100 / 2}`)
3. Booleans
  * Falsy: `false`, `undefined`, `0`, `NaN`, `null`
  * Truthy: `true`, all the rest
  * **Note:**
    * `Nan == false` --> `false`
    * `NaN == true` --> `false`
    * `NaN == NaN` --> `false`
    * `null == undefined` --> `true`
    * `null == 0` --> `false`
  * Können durch binäre Operatoren erstellt werden. z.B. `console.log(3 > 2)`
4. Undefined Values: `undefined` (als Wert und als Typ) --> der Wert mit dem das System arbeitet
5. Empty Values: `null` (nur als Wert) --> der Wert mit dem wir arbeiten sollten

##### Operatoren
Hierarchie der Operatoren:
1. Rest
2. Vergleichsoperatoren (`<, >, ==, ...`)
3. `&&`
4. `||`

**Automatische Typkonvertierung:** kann oftmals ausversehen passieren, und nennt sich *type coercion*
* `"5" - 1` output `4` (number) weil es nur eine zugewiesene Funktion für `-` gibt
* `"5" + 1` output `51`(string) weil es sowohl für Strings als auch für Numbers zugewiesene Funktionen für `+` gibt
* OHNE automatischer Typenkonvertierung:
  * `===` und `!==`: testen ob die Werte *genau* gleich sind (ohne Typkonvertierung)

**Unary, Binary, Ternary Operatoren**
* Unary operator: benötigen nur ein Argument
  * `typeof 4.5` oder `typeof "x"`
* Binary operator: benötigen 2 Argumente
  * `10-2`
* Ternary/Conditional: 3 Argumente
  * `?` und `:`
  * z.B. `true ? 1 : 2` --> if `true` operator picks middle value. else operator picks right value.

**Logische Operatoren:**
* and `&&`
* or `||`
  * `<empty-value> || <value>` --> `<value>`: serves as replacement value
  * `<number-value> || undefined` --> `NaN`
  * `<string1> || <string2>` --> `<string1>`:
* not `!`

**Short-Circuit Evaluation:**


##### Derived Data Types (Komplexe Datentypen)
Referenzen (nicht Werte) werden übergeben
1. Objects `{}`
2. Functions
  * `parseInt()`

### Programmstrukturen
* Expression: 1+ Operationen; gibt immer einen Wert zurück
* Statement: Befehl der Interpreter veranlasst etwas zu tun (z.B. Zuweisung, Funktionsaufruf, ...)
* Programm: sequentielle Ausführung von Anweisungen
* Variables: `var`, `let`, `const` (erneute Zuweisung nicht möglich)
  * Call-by-Value: Wert der Variablen gespeichert
  * Call-by-reference: Referenz auf Wert gespeichert
  *  Unterschied `let` vs. `var`
      ```javascript
      {
        var x = 1;
        console.log(x); // wird ausgeführt weil innerhalb des Block Scopes
        let y = 2;
        console.log(y); // wird ausgeführt
      }
      console.log(x); // ist auch sichtbar
      console.log(y); // wird nichtausgefürht; Gültigkeit nur auf Block Scope beschränkt
      ```
* Block Scope: Bereich (innerhalb von `{}`) in dem eine Variable genutzt werden kann
* DOM: Document Object Model

#### Kontrollflüsse
* ```javascript
  switch (...) {
    case "case 1":
      // <condition 1>
      break;
    case "case 2":
      // <condition 2>
      break;
    default:
      // <condition else>
      break;
  }
  ```
* `do`+ `while` vs. `while`
*

## Resources

### Eloquent JavaScript
1. [Ch 1: Values, Types and Operators](http://eloquentjavascript.net/01_values.html)
