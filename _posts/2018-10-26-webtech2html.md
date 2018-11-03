---
layout: page
title: "2. HTTP, HTML und DNS"
category: webtech
date: 2018-10-26 10:26:53
order: 5
---

#### Vorlesungen

2. [HTML](https://isis.tu-berlin.de/pluginfile.php/1113291/mod_resource/content/1/webtech-ws18-chapter02.pdf)


## HTML

#### Markup-Sprachen
* Maschinenlesbare Sprache für Gliederung/Formatierung von Daten
* Beschreibung von Eignschaften, Semantik, Darstellungsformen von Texten/Datenmengen

##### Sprachen
* SGLM: Standardized General Markup Language
* XML: Extensible Markup Language
  * Man muss eigene Elemente/Steuerinformationen definieren (siehe XML in a Nutshell)
  * Enthält Strukturen um die Interpretation für den Computer zu ermöglichen.
* HTML: HypterText Markup Language
  * Basiert auf XML und SGML
  * Hat bereits vordefinierte Elemente
  * Kann bereichert werden durch weitere Steuerinformationen und Attribute (z.B. `type`)

In diesem Fall ist <adresse> eine Struktur die aus eingebetteten Elementen besteht:
```xml
<!DOCTYPE xml>
<adresse type="liefer" encoding="UTF-8"> // fügt Attribut hinzu, und weiß in welchem Encodingsystem es die Info widergeben soll
  <vorname>Erika</vorname>
  <nachname>Mustermann</nachname>
  <strasse>Ernst-Reuter-Platz 7</strasse>
  <stadt>10385 Berlin</stadt>
</adresse>
```

##### HTML5 vs. CSS3
* CSS:
  * "Cascading Style Sheet"
  * Design einer Website
  * Ergänzt HTML und bereitet Inhalte optisch auf
* HTML5:
  * liefert INhalte eienr Website in strukturierter Form
  * Gute HTML-Struktur: elementar für Suchmaschinen
    * Hinweise zum Inhalt der Website sollte gegeben sein (z.B. `<h1></h1>` etc.)
  * `< starttag <attribute> <attribute> > INHALT <endtag>`

HTML und CSS Beispiel:
```html
<!DOCTYPE html>
<html>
  <head> // Enthält Steuerinformation
    <title>Title 0</title>
    <meta charset="UTF-8"> // meta tag muss nicht geschlossen werden (HTML5-spezifisch)
  </head>
  <body> // Inhalt der für Nutzer sichtbar ist
    <h1 style="font-size: 30px; color: red">Bestandteil 1</h1> // Eine Zeile von CSS
    <h2>Bestandteil 2</h2> // Header 2

    <p> Bla bla Bla
    </p> // Paragraph

    <div>Weiterer Bestandteil</div>

  </body>
</html>
```

#### HTML-Syntax
* Parent element, child element
* HTML5 hat viel mehr Freiheiten als xHTML (z.B. `<img src = "source.jpg">` war nicht nötig, sondern man musste img noch schließen mit `/img>`)
* Tags:
  * `ol`: ordered list (Zahlen)
  * `ul`: unordered list (Bulletpoints)
  * `li`: list item (muss nicht mehr geschlossen werden bei HTML5)
  * `tr`: table row (neue Zeile)
  * `td`: dable data (neue Zelle in einer Zeile)
  * `type` immer nutzen
  * `required`: Eingabe wird verlangt bevor Element abgespeichert werden kann
  * `autofocus`: Zelle in die Cursor automatisch springt sobald die Website gelade ist
* In Texten/Strings müssen folgende Zeichen anders geschrieben werden
* Wenn `style` mit eingebunden wird greifen wir auf CSS zu (eingebettet in HTML) --> nicht wünschenswert

```html5
<form action="zielseite.html" method="post" name="mein-formular"> // form definierteinen Bereich, dessen Inhalt später in einer Datei namens "zielseite.html" abgespeichert wird. Dient zur Kommunikation zwischen Frontend und Backend
</form>
```


#### HTML Head
#### HTML Body
#### HTML Beispiel
