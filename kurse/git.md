# Git Kurs

## Was ist Git?

- Git ist ein Versionsverwaltungsprogramm (für Code)
  - verschiedene Versionen eines Projektes behalten
  - Änderungshistorie angucken
  - Versionen zusammenführen
  - den Arbeitsstand anderer in den eigenen Arbeitsstand integieren
- Programmiert für den Linux Kernel

## Was ist GitHub?

- Hosting Plattform für mit git verwaltete Projekte ("**Remote**")
- Kollaborationsplattform
  - Wiki
  - Issue tracker (Bugs, Verbesserungsvorschläge, Feature requests)
  - Continous Integration  (automatisches Bauen und Upload der Webseite, Fehlersuche etc.)
- Code ist in **Repositories** gegliedert. (Schreibweise: Username/Repository)
  - Datenanfragen.de hat eine Organisation (*datenanfragen*) und folgende (wichtigen) Repos:
    - *datenanfragen/website*   
      Enthält alles wichtige, was auf der Webseite passiert: Generator, Artikel etc.
    - *datenanfragen/data*  
      Enhält alle Daten und Verarbeitungsskripte für die Unternehmensdatenbank etc.
    - *datenanfragen/verein*  
      Enthält öffentliche Vereinsdokumente (Satzung, Datenschutzerklärung etc.)


## Setup

### Schritt 1: GitHub Account

1. GitHub Account erstellen  (mit E-Mail etc.)
2. Datenanfragen Organisation angucken (https://github.com/datenanfragen)
3. datenanfragen/website forken
  - **Fork** ist eine persönliche Kopie des Repos in ein eigenes Repo. Hier kann mensch dann Veränderungen vornehmen, ohne den aktuellen Stand direkt zu beeinflussen.
  
### Schritt 2: Git installieren

1. Konsole aufmachen
2. macOS: XCode Command Line Tools installieren  
  Ubuntu/Windows Subsystem for Linux: 
```bash
sudo apt install git
```
3. Testen mit `git --version`
4. Name und E-Mail festlegen (die gleichen wie bei GitHub verwenden)
```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com 
```
5. SSH-Key erstellen
```bash
ssh-keygen -o -a 100 -t ed25519 # Schlüssel erstellen
cat ~/.ssh/id_ed25519.pub # öffentlichen Schlüssel ausgeben
``` 
6. öffentlichen Schlüssel bei GitHub eintragen (Account Settings > SSH and GPG Keys > New SSH key)

### Schritt 3: Repository klonen

1. In einen passenden Ordner wechseln (`cd` (Change Directory) und `ls` (List) benutzen, ggf. mit `mkdir` einen neuen erstellen)
2. Das `git clone` Kommando von github kopieren (Grüner Button "Klonen oder Downloaden") und ausführen
3. Mit `ls` und `cd` exploren

## Wichtige Kommandos

### Bearbeitete Änderungen in die Versionsverwaltung übernehmen

```bash
git add Dateiname.endung # Datei in den Staging-Bereich bringen
git commit -m 'Commit message' # Änderungen in die Historie schreiben
```

Die **Commit Message** beschreibt knapp die Änderungen seit dem letzten **Commit**.

### Aktuellen Stand auf den Stand des Ursprungs angleichen

```bash
git pull upstream master
```

Hierbei kann es zu sog. **Merge Conflicts** kommen, wenn Änderungen in der eigenen Version nicht mit den Änderungen auf dem Ursprung übereinstimmen. Um das Problem zu lösen, versucht git die Dateien zusammenzuführen und markiert die kritischen Stellen:

```
<<<<<<< HEAD
Inhalt auf meinem Stand
=======
Inhalt auf dem Stand des Ursprungs
>>>>>>> upstream/master
```

Das muss dann einfach so bearbeitet und commitet werden, so dass die Datei wieder Sinn ergibt. Für Binärdateien funktioniert es nicht so einfach, hier muss eine Datei ausgewählt werden, die gewünscht ist:

```bash
git checkout --ours neues_bild.jpg
git checkout --theirs altes_bild.jpg
```

### Fertigen Arbeitsstand hochladen

```bash
git push origin master
```

Es werden nur Änderungen beachtet, die comittet wurden.

### Stand der Arbeitskopie anzeigen

```bash
git status
```

Gitb Aufschluss darüber, welche Dateien von git getrackt werden, ob Änderungen vorliegen, die noch comittet werden müssen, welche Änderungen gestaged wurden und welche nicht. Sollte vor einem Commit, Merge oder Pull ausgeführt werden, um sicherzugehen, dass keine wichtigen Änderungen verloren gehen.

### Pull Requests

 - "Bitte" den eigenen Stand in das Ursprungsrepo zu integrieren
 - Können von den **Maintainern** überprüft und angenommen werden
 - Wenn eine Ergänzung fertig ist, kann ein PR erstellt werden:
  1. Im geforkten Repo auf "Pull Request" klicken, unter dem "Clone or Download"-Button 
     ![Geforktes Repository](/res/screenshot-forked-repo.png)
  
  2. Die Änderungen überprüfen und dann auf "Create Pull Request" klicken
     ![Eine PR erstellen](/res/screenshot-create-pr.png)

  3. Im Pull Request werden dann die Änderungen diskutiert und Anmerkungen gemacht. Um sie einzubauen, einfach neue Commits ins geforkte Repo hochladen.
  4. Der PR wird dann angenommen und in den master-Branch gemerged.
  
### Issues

- Auf GitHub auf der Repository Seite zu finden
- Werden genutzt, um den Arbeitsstand zu verfolgen und dokumentieren:
  - Bug Reports (Was geht nicht, warum, wie lässt sich der Bug reproduzieren)
  - Feature requests (Ich hätte gerne dieses Feature, baut das bitte ein)
  - Dokumentation des aktuellen Arbeitsstands (Es fehlen noch diese ToDos bis zum neuen Feature)
  - Diskussion zu wichtigen Entscheidungen
  - Fragen zum Programm
- Mit Labels werden Issues nach Arten sortiert
- Issues können Leuten zugewiesen werden, die dann daran arbeiten
- Wir sammeln Diskussionen und Recherchen zu einen Thema im dazugehörigen Issue

## Beispiel-Arbeitsablauf: Artikel schreiben

1. Stand aktualisieren: `git pull upstream master`
2. Deutschen Artikel schreiben (`interesting-article.de.md`)
3. Datei stagen: `git add interesting-article.de.md`
4. Änderungen schreiben: `git commit -m 'New article about interesting topic'`
5. Englischen Artikel schreiben (`interesting-article.en.md`) und deutschen bearbeiten
6. Änderungen stagen: `git add interesting-article.en.md; git add interesting-article.de.md`
7. Comitten: `git commit -m 'English translation'`
8. Stand hochladen: `git push origin master`
9. PR erstellen

## Resources

- https://rogerdudler.github.io/git-guide/index.de.html
- https://git-scm.com/book/de/v2
- https://guides.github.com/introduction/git-handbook/
