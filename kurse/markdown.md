# Kurze Einführung in Markdown im Kontext von Datenanfragen.de

<!-- Diese Punkt erst einfach ohne große Visualisierung erzählen. Den Beispielcommit unten live auf GitHub zeigen. -->

- Markdown ist Auszeichnungssprache für Texte
- Nicht wirklich eindeutig spezifiziert\*, es gibt verschiedene Varianten. Wir fokussieren uns auf die Dinge, die wir für die Arbeit an Datenanfragen.de brauchen und lernen auch einige Sachen, die über 'normales' Markdown hinausgehen.
- Kontrast zu WYSIWYG, Steuerzeichen im Text
- Grundidee: Menschenlesbar, auch ohne Rendering soll die gewünschte Formatierung erkennbar sein
- Vorteile
  * Einheitliches und intuitives Format, das für viele unterschiedliche Zwecke genutzt werden kann (Artikel auf Webseiten, Printdokumente, Notizen, E-Mail-Nachrichten, technische Dokumentation, Präsentationen, …)
  * Einfacher und klarer als andere Auszeichnungssprachen (z. B. HTML)
  * Plaintext
    - portabel, betriebssystem- und softwareunabhängig
    - future-proof: Kann auch ohne spezielle Software gelesen und verändert werden
    - Nutzer_in kontrolliert genau, was passiert. Keine versteckten Steuerzeichen oder dergleichen, die zu schwer diagnostizierbaren Formatierungsfehlern führen.
    - wunderbar in Versionskontrolle integrierbar <!-- Demonstrieren mit: https://github.com/datenanfragen/website/commit/094d0cc413c6e467d9cdce99eedf27d4ab4f9df4 -->  
      ![Übersicht der Änderungen an einem Markdowndokument](/res/screenshot-github-markdown-diff.png)

## Markdown an einem Beispiel erklärt

<!-- Das folgende Markdown live im Editor im Repo "entwickeln" mit preview der gerenderten Seite daneben. -->

Datei anlegen: `content/blog/musterartikel-markdown.de.md` -> `content/blog/sample-post-markdown.de.md`

```md
<!-- Header kopieren aus `sample-letter-gdpr-direct-marketing-objection.de.md`. -->
{
    "title": "Musterartikel als kurze Einführung in Markdown im Kontext von Datenanfragen.de",
    "slug": "musterartikel-markdown",
    "aliases": [ "sample-post-markdown" ],
    "date": "2019-10-25T14:59:57+02:00",
    "last_edited": "2019-10-26T14:59:57+02:00",
    "type": "blog",
    "description": "Dieser Musterartikel gibt eine kurze Einführung in die Auszeichnungssprache Markdown. Er fokussiert sich dabei auf die Inhalte, die für die Mitarbeit an Datenanfragen.de wichtig sind.",
    "tags": [ "markdown", "auszeichnungssprache" ],
    "authors": [ "baltpeter" ],
    "license": "cc-by-4.0"
}

Blocktext wird ganz normal geschrieben.

Absätze werden durch eine Leerzeile erreicht.

Zeilenumbrüche erforden zwei Leerzeichen am Ende der Zeile.  
Vergisst man die zwei Leerzeichen, wird der Zeilenumbruch ignoriert.
Dieser Satz wird also direkt nach dem letzten weitergehen, ohne eine Leerzeile dazwischen.

## Überschriften

Überschriften werden mit entsprechend ihres Levels vielen Rauten eingeleitet.

Dieser Absatz wurde mit einer Überschrift zweiter Ebene eingeleitet. Pro Seite gibt es nur eine Überschrift erster Ebene, die wird aber automatisch aus dem Titel generiert.

### Das ist eine Überschrift dritter Ebene

Es gibt theoretisch Überschriften bis zur sechsten Ebene. In der Regel benutzen wir sie aber nur bis zur dritten oder maximal vierten Ebene.

Zwischen Überschriften und den darauffolgenden Absätzen sollte eine Leerzeile stehen.

## Hervorhebungen

Ein oder mehrere Worte können kursiv dargestellt werden, indem man sie mit Sternchen (`*`) umschließt:  
Die *DSGVO* stärkt Deine Rechte.

Sollen ein oder mehrere Worte fett dargestellt werden, umschließt man sie mit je **zwei** Sternchen:  
Für Anfragen entstehen grundsätzlich **keine** Kosten.

Fett und kursiv können eigentlich auch kombiniert werden, darauf verzichten wir aber aus stylistischen Gründen.

## Links und Bilder

Links sehen wie folgt aus:  
Unsere Repositories findest Du bei [GitHub](https://github.com/datenanfragen).

Um auf eine anderen *interne* Seite zu verweisen, benutzen wir den `ref`-Shortcode und geben darin den *Dateinamen* dieser anderen Seite an:  
Die [Datenschutz-Aufsichtsbehörden]({{< ref "supervisory-authorities" >}}) sind unabhängige Stellen in jedem EU-Land, deren Aufgabe es ist die Einhaltung der Datenschutzgesetze sicherzustellen.

Bilder hingegen wie folgt: `![Beschreibung des Bildes](URL des Bildes)`, also z. B.:  
![Eine Beschwerde über Datenanfragen.de verschicken.](/img/blog/mahnung-senden.png)

## Auflistungen

Auflistungen funktionieren genauso wie man es sich denkt:

1. Dies ist der erste Punkt.
2. Und dies der zweite.
    1. Rücken wir ein Element mit zwei oder vier Leerzeichen ein, fängt es eine neue Aufzählungsebene an.
    2. Das ist Punkt 2.2.
3. Um wieder auf der ursprünglichen Ebene weiterzumachen, entfernen wir einfach die Einrückung.

Analog funktioniert das auch mit nicht-nummerierten Listen.

* Dafür verwenden wir entweder `*`
* oder `-`.
* Diese sollten wir aber innerhalb einer Ebene nicht mischen.
    - Es bietet sich vielmehr an, zwischen den Ebenen die Zeichen zu wechseln.
    - So haben wir eine deutlichere Abgrenzung dazwischen.

## Zitate

Zitate werden einfach durch ein `>` davor markiert. Auch hier müssen wir die zwei Leerzeichen am Ende der Zeile für eine Leerzeile beachten. Auch leere Zeilen für Absätze werden mit einem `>` begonnen.

Um am Ende eine Quelle für das Zitat anzugeben, umschließen wir diese in `<cite>` und `</cite>`. Das ist kein Teil von Markdown, sondern wir verwenden hier einfach normales HTML innerhalb unseres Markdowns.

> Rasche technologische Entwicklungen und die Globalisierung haben den Datenschutz vor neue Herausforderungen gestellt. Das Ausmaß der Erhebung und des Austauschs personenbezogener Daten hat eindrucksvoll zugenommen. […]  
> Zunehmend machen auch natürliche Personen Informationen öffentlich weltweit zugänglich.
>
> Die Technik hat das wirtschaftliche und gesellschaftliche Leben verändert und dürfte den Verkehr personenbezogener Daten innerhalb der Union sowie die Datenübermittlung an Drittländer und internationale Organisationen noch weiter erleichtern, wobei ein hohes Datenschutzniveau zu gewährleisten ist.  
> – <cite>Erwägungsgrund 6 zur DSGVO</cite>

## Fußnoten

Wir können auch Fußnoten in den Text einfügen.[^1] Die Fußnoten werden automatisch durchnummiert.

[^1]: Der *Identifier* der Fußnote muss dabei keine Zahl sein, sondern wir können auch ein Wort verwenden.

Der Inhalt der Fußnote kann theoretisch an einer beliebigen Stelle im Dokument stehen, der besseren Lesbarkeit halber sollte er aber direkt auf die Fußnote folgen.

## Linien

Eine Linie erzeugen wir einfach durch drei aufeinanderfolgende `-`:

---

Danach geht es weiter.

## Kommentare

Manchmal wollen wir eine Notiz hinterlassen, die aber nicht auf der Webseite erscheint. Das geht mit einem Kommentar.

<!-- TODO: Diesen Abschnitt sollten wir bei Gelegenheit noch mit einem Bild versehen. @zner0L: Machst du das? -->
```

## Wie geht es weiter?

Wer sich noch weiter mit Markdown auseinandersetzen möchte, kann sich eines der zahlreichen Tutorials anschauen, bspw. [dieses](https://www.markdowntutorial.com/).

Bei Unklarheiten hilft es oft, sich einen anderen Artikel zu suchen, der etwas Ähnliches erreicht. Wir haben mittlerweile für die meisten use cases Beispiele in anderen Artikel, an denen man sich gut orientieren kann. Ansonsten stehen wir bei Fragen natürlich auch immer gerne zur Verfügung.

## Anhang

### Unterstützte Lizenzen

Aktuell unterstützt unsere Webseite die folgenden Lizenzen (wir können bei Bedarf aber auch gerne weitere hinzufügen):

* `cc-by-4.0`: Creative Commons Namensnennung 4.0 International Lizenz
* `cc-by-nd-4.0`: Creative Commons Namensnennung - Keine Bearbeitungen 4.0 International Lizenz
* `cc-by-sa-4.0`: Creative Commons Namensnennung - Weitergabe unter gleichen Bedingungen 4.0 International Lizenz
* `cc0-1.0`: CC0 1.0 Universell Public Domain Dedication

Ist keine Lizenz explizit angegeben, wird automatisch CC BY 4.0 genutzt.
