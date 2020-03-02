# Die Daten hinter Datenanfragen.de

* Liegt alles im [data-Repo](https://github.com/datenanfragen/data/)
* CC0-lizensiert
* Setzt sich im Wesentlichen zusammen aus:
  - Unternehmensdatenbank
  - Aufsichtsbehördendatenbank
  - Liste empfohlener Unternehmen pro Land
  - Templates für den Generator
* Änderungen an diesen Teilen werden automatisch in die Webseite übernommen

## Unternehmensdatenbank

* Die meisten Inhalte der Unternehmensdatenbank sind über die [Webseite](https://www.datenanfragen.de/company/) verfügbar.
* Änderungsvorschläge nehmen wir entweder [direkt über die Webseite](https://www.datenanfragen.de/suggest) (das verursacht aber momentan noch relativ viel Aufwand für uns) oder über das GitHub-Repo an.
* Jedes Unternehmen ist eine eigene JSON-Datei im Ordner [`companies`](https://github.com/datenanfragen/data/tree/master/companies).
  <!-- Ein paar records zeigen, ein Gefühl für die Inhalte der DB entwickeln. -->
* Die Einträge folgen dabei alle einem genauen [Schema](https://github.com/datenanfragen/data/blob/master/schema.json). <!-- (zeigen) --> Das Schema legt fest, welche Felder enthalten sein dürfen und müssen.
* Keine Sorge: Man muss weder das Schema auswendiglernen noch wissen, wie man JSON-Dateien schreibt. Wir haben ein [Tool](https://company-json.netlify.com/), welches das Erstellen von Einträgen vereinfacht.
  <!-- Company JSON generator öffnen und zeigen. --> 
* Welche Felder gibt es? (fett markierte Felder sind Pflichtfelder) <!-- Mit dem company JSON generator zeigen. -->
  - **`slug`**: Ein eindeutiger Identifier für den Eintrag, legt den Dateinamen fest. Ein Wort, keine Leer- oder Sonderzeichen (außer `-`, der ist erlaubt) und komplett kleingeschrieben.  
    Bsp.: [`"datenanfragen"`](https://www.datenanfragen.de/company/datenanfragen)
  - **`relevant-countries`**: Für welche Länder ist dieser Eintrag relevant? [Google](https://www.datenanfragen.de/company/google) bietet seine Dienste etwa in allen Ländern an, aber das [Amtsgericht Hagen](https://www.datenanfragen.de/company/amtsgericht-hagen) wird wohl eher nur in Deutschland relevant sein.
  
    Länder sind dabei als sog. ISO316-1 alpha-2-Code anzugeben. (Eine Liste davon gibt es etwa bei [Wikipedia](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements)).   
    Bsp.: `[ "de", "at", "fr", "es" ]` oder `[ "all" ]`
  - `categories`: Eine Liste von Kategorien für das Unternehmen. Bewusst vage gehalten, dürfen "großzügig" zugewiesen werden.  
    Bsp.: `[ "addresses", "collection agency" ]`
  - **`name`**: Der offizielle Name/die offizielle Bezeichnung des Unternehmens.  
    Bsp: `"Datenanfragen.de e. V."`
  - `runs`: Eine Liste von weiteren Entitäten und Diensten, für die das Unternehmen (mit-)verantwortlich ist. Das können z. B. Tochterunternehmen eines Konzerns oder Webseiten, die das Unternehmen anbietet, sein.  
    Bsp.: [`[ "HDI Versicherung AG", "HDI Lebensversicherung AG", "HDI Vertriebs AG", "HDI Global SE", "…" ]`](https://www.datenanfragen.de/company/talanx/)
  - **`address`**: Die Adresse zum Kontakt zu Datenschutzfragen. Die Adresse sollte keine "z. Hd."-Zeile enthalten, die wird automatisch im Generator hinzugefügt. Die einzelnen Elemente der Adresse werden durch Leerzeilen (im JSON als `\n` angegeben) getrennt.  
    Die Adresse muss als letzte Zeile immer das Land enthalten. Dieses sollte entweder auf Englisch oder in der Landessprache angegeben werden. Ansonsten wird die Adresse in einem für den internationalen Versand geeigneten Format angegeben, dabei ggf. an anderen Einträgen aus dem gleichen Land orientieren.  
    Bsp.: `"Schreinerweg 6\n38126 Braunschweig\nDeutschland"`
  - `phone`: Die Telefonnummer. Wenn die_der DSB eine eigene hat die, ansonsten die am besten passende.  
    Bsp.: `"+49 531 209299 35"`
  - `fax`: Die Faxnummer. Wenn die_der DSB eine eigene hat die, ansonsten die am besten passende.  
    Bsp.: `"+49 531 209299 36"`
  - `email`: Die E-Mail-Adresse. Wenn die_der DSB eine eigene hat (häufig z. B. `datenschutz@`, `privacy@`, `dpo@` o. Ä.) die, ansonsten die am besten passende.  
    Wir erlauben keine personenbezogenen Daten in den Einträgen. Also auch keine E-Mail-Adressen, die Namen enthalten (wie `kim.mustermensch@example.com`).
  - `web`: Die URL der Webseite des Unternehmens.
  - **`sources`**: Eine Liste von URLs zu den Quellen, aus denen der Eintrag zusammengestellt wurde.
  - `required-elements`: Eine Liste der Identifikationselemente, von denen wir wissen, dass sie für Anfragen nötig sind.  
    Wenn angegeben, muss immer ein Element mit dem Typ `name` vorhanden sein (das braucht der Generator). Weiterhin sollte ein Element enthalten sein, welches es dem Unternehmen ermöglicht, auf die Anfrage zu antworten (also etwa eine E-Mail-Adresse oder Telefonnummer).
  - `request-language`: Die Sprache, die für Anfragen gewählt werden sollte. In den meisten Fällen nicht anzugeben. Nur dann nötig, wenn das Unternehmen seine Dienste nur in einer bestimmten Sprache anbietet, die nicht mit der Landessprache der Länder/des Landes übereinstimmt, in denen/dem es seine Dienste anbietet. Ansonsten fallen wir nämlich eh auf die Webseitensprache der Nutzer_in zurück, das ist in den meisten Fällen korrekt.
  - `custom-access-template`: Gesondertes Template, das für Auskunftsanfragen an dieses Unternehmen genutzt werden sollte. Angabe des Dateinamens im `templates`-Ordner ohne Dateiendung.  
    Bsp.: [`"access-bundesjustizamt"`](https://www.datenanfragen.de/company/bundesjustizamt)
  - `custom-erasure-template`: Analog für Löschanfragen.
  - `custom-rectification-template`: Analog für Berichtigungsanfragen.
  - `needs-id-document`: Ist für die Anfrage das Anhängen eines Ausweisdokuments nötig? Nur als "ja" angeben, wenn das definitiv in allen Fällen so ist.  
    Bsp.: `true` oder `false`
  - `suggested-transport-medium`: Auf welchem Wege sollten Anfragen an das Unternehmen am besten gestellt werden? Standardwert: E-Mail (bitte ggf. trotzdem explizit angeben)  
    Bsp.: `"fax"` oder `"letter"` oder `"email"`
  - `comments`: Hinweise zu dem Unternehmen, die auch im Generator angezeigt werden.  
    Bsp.: [`[ "Achtung: Telefonnummer ist kostenpflichtig (3,99 EUR pro Anruf – nur aus dem deutschen Festnetz erreichbar)!" ]`](https://www.datenanfragen.de/company/1und1-webde)
<!-- * Ein/zwei Beispieleinträge anlegen. -->
* Weitere Hinweise und Tipps gibt es in der [README](https://github.com/datenanfragen/data/blob/master/README.md).

## Aufsichtsbehördendatenbank

* "Füttert" die [Liste von Aufsichtsbehörden](https://www.datenanfragen.de/supervisory-authority/) auf der Webseite.
* Wird aber auch verwendet, wenn Nutzer_in zu einer Anfrage eine Beschwerde schicken möchte.
  <!-- Das kurz demonstrieren. -->
* Folgen ähnlichem [Schema](https://github.com/datenanfragen/data/blob/master/schema-supervisory-authorities.json) wie die Unternehmen. Die JSON-Dateien hierfür liegen im Ordner [`supervisory-authorities`](https://github.com/datenanfragen/data/tree/master/supervisory-authorities).
* An den Inhalten ändert sich naturgemäß nicht so häufig etwas. Es wäre aber sicherlich doch sinnvoll, ab und an mal zu prüfen, ob noch alles korrekt ist…

## Liste empfohlener Unternehmen pro Land

* Auf unserer Startseite haben wir einen Wizard, der quasi als erster (praktischer) Kontaktpunkt mit der DSGVO gedacht ist. Idee dabei ist, an eine große Anzahl von Unternehmen möglichst einfach Auskunftsanfragen zu schicken, um so überhaupt erst einmal einen Überblick zu bekommen, was für Daten zu einem selbst verarbeitet werden. Ausgehend von diesen Informationen kann man dann bei Bedarf weitergehen und ggf. etwa Berichtigungs- und/oder Löschanfragen an einzelne Unternehmen schicken.
* Der Wizard führt hierbei durch eine Reihe von Kategorien, die der Nutzer_in helfen soll, sich an Unternehmen zu erinnern, mit denen sie "Kontakt" hatte. (-> Der Flow hiervon soll aber angepasst werden, vgl. Aufgabenfelder).
* Die Liste der ausgewählten Unternehmen ist aber von Anfang an vorausgefüllt mit eben den *empfohlenen Unternehmen*. Das sind Unternehmen von denen wir wissen/ausgehen, dass sie Daten zu einer großen Menge von Menschen in dem jeweiligen Land verarbeiten, ggf. auch ohne dass die Menschen das unbedingt mitkriegen. Klassische Beispiele sind hier die Schufa und der Beitragsservice, aber auch etwa Adresshändler.
* Technisch gesehen hat jedes unterstützte Land im Ordner [`suggested-companies`](https://github.com/datenanfragen/data/tree/master/suggested-companies) eine JSON-Datei mit einer Liste der *Slugs* der empfohlenen Unternehmen.
  <!-- Das demonstrieren. -->
* In der Zukunft würde ich mir wünschen, dass wir zusätzlich dazu noch zu jedem Unternehmen einen Grund angeben, warum es auf der Liste enthalten ist (ggf. auch aus einer Liste vorgegebener Gründe). Das ist aber momentan weder implementiert noch nennenswert geplant.

## Templates

* Die Templates dienen als Grundlage für die Schreiben, die der Generator generiert.
* Es handelt sich dabei um einfache Textdateien, die im [`templates`-Ordner](https://github.com/datenanfragen/data/tree/master/templates) liegen, sortiert nach Sprache.
* Um eine Sprache auf der Webseite zu unterstützen brauchen wir mindestens die folgenden Templates:
  - `access-default`: Auskunftsanfrage
  - `erasure-default`: Löschanfrage
  - `rectification-default`: Berichtigungsanfrage
  - `objection-default`: Werbewiderspruch
  - `admonition`: Mahnung bei nicht korrekt oder rechtzeitig beantworteter Anfrage
  - `complaint`: Beschwerde bei Aufsichtsbehörde
* Zusätzlich zu den `-default`-Varianten können auch spezielle Templates vorhanden sein, etwa spezifisch für ein Unternehmen (etwa [Bundesjustizamt](https://github.com/datenanfragen/data/blob/master/templates/de/access-bundesjustizamt.txt)) oder eine Unternehmensgruppe (etwa [Trackingunternehmen](https://github.com/datenanfragen/data/blob/master/templates/de/access-tracking.txt)).
* Darüber hinaus können theoretisch auch vollkommen andere Templates hinterlegt werden, die dann über die "Eigener Text"-Funktion im Generator genutzt werden könnten. Das wird aber aktuell noch nicht genutzt.
<!-- `de/access-default.txt` öffnen -->
* Innerhalb der Templates gibt es einige Formatzeichen, die genutzt werden können:
  - Text, der zwischen `<bold>` und `</bold>` steht, wird fett angezeigt. Text, der zwischen `<italic>` und `</italic>` steht, wird kursiv angezeigt.
  - Mithilfe der *Flags* können Textabschnitte eingefügt werden, die nur unter bestimmten Umständen im generierten Schreiben erscheinen. Der folgende Satz wird etwa nur angezeigt, wenn die `data_portability`-Flag wahr ist (das kann die Nutzer_in im Generator mit der Checkbox "Daten in maschinenlesbarem Format erhalten" einstellen):
    ```
    [data_portability>
    Ich bitte Sie, mir die betreffenden personenbezogenen Daten, die ich Ihnen zur Verfügung gestellt habe, im Sinne des Art. 20 Abs. 1 DSGVO in einem strukturierten, gängigen und maschinenlesbaren Format zu übermitteln.
    ]
    ```
  - Mithilfe von *Variablen* können Inhalte, die von der Nutzer_in abgefragt wurden, in das Schreiben integriert werden. So werden an der Stelle von `{id_data}` etwa die Identifikationsdaten der Nutzer_in eingefügt.
