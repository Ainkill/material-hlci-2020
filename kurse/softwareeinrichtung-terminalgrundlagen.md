# Einrichtung der Software und Terminalgrundlagen

Die folgenden Erklärungen nehmen an, dass eines der folgenden Systeme benutzt wird:

* Windows 10 mit installiertem WSL (Ubuntu 18.04)
* Ubuntu, Debian oder ein anderes Debian-Derivat in einer aktuellen Version
* macOS mit installiertem [Homebrew](https://brew.sh/)

Es können grundsätzlich auch andere Systeme genutzt werden, dann weichen die genauen Schritte aber ggf. etwas ab.

## Terminalgrundlagen

### Motivation: Warum nutzen wir das Terminal?

* Oftmals "mächtiger" als grafische Oberflächen (GUIs), Zugriff auf umfangreichere Befehle
* Insbesondere im Programmierbereich gibt es Vieles nur als Kommandozeilensoftware.
* Einfacher zu beschreiben: Es kann einfach ein Befehl (oder eine Reihe von Befehlen) angegeben werden statt aufwendige Klicksequenzen und Positionen von Buttons zu beschreiben, die sich im schlimmsten Fall mit dem nächsten Update ändern werden.
* Es besteht die Möglichkeit, völlig unabhängige Programme miteinander zu verbinden, was in GUIs nicht möglich ist.
* Dadurch ist es dann auch einfach, häufig wiederkehrende Prozesse zu automatisieren. Wenn jemand etwa Änderungen an unserem Code oder unseren Daten hochlädt, werden diese vollkommen automatisch kompiliert ("zusammengeführt"), getestet und auf die Webseite hochgeladen, ohne dass wir irgendetwas tun müssen.
* Häufig versteht man bei der Nutzung des Terminal besser, was eigentlich tatsächlich passiert.
* Mit ein bisschen Erfahrung ist die Bedienung über Terminals häufig schneller bis deutlich schneller als die über GUIs.

### Das Terminal öffnen

Je nach System gibt es leicht unterschiedliche Wege, das Terminal zu öffnen.

* **unter Windows**: Weil wir uns entschieden haben, Ubuntu 18.04 in unserem WSL zu installieren, geben wir einfach in der Suche `ubuntu` ein und starten das Programm *Ubuntu 18.04*.
* **unter macOS**: Mit *Command* + *Leertaste* Spotlight öffnen und `terminal` eingeben. Dann das Programm *Terminal* starten.
* **unter Linux**: Kann sich je nach System unterscheiden. Meist heißt das Programm auch *Terminal* und die Suche lässt sich mit der *Super (Windows)*-Taste öffnen.

### Wichtige Befehle

Das Terminal wartet nun auf die Eingabe von Befehlen. Wir wollen einige grundlegende Befehle einführen. Aus Zeitgründen werden wir nicht auf komplexere Befehle und das "Kombinieren" von Befehlen eingehen. Bei Interesse gibt es da aber zahlreiche Erklärungen im Internet zu.

* Die Befehle werden immer im Kontext eines Verzeichnisses ausgeführt. Bei ersten Start befinden wir uns im Homeverzeichnis (Benutzerverzeichnis, hier liegen bspw. auch die Dokumente- und Downloadordner; unter Linux und WSL: `/home/[username]`, unter macOS: `/Users/[username]`; kann auch mit `~` abgekürzt werden).  
* Das aktuelle Verzeichnis wird in der Regel in der Befehlszeile angezeigt, kann sonst aber auch jederzeit mit dem Befehl `pwd` (steht für 'print working directory') ausgegeben werden.
* Mit `ls` (steht für 'list') werden die Dateien und Ordner im aktuellen Verzeichnis ausgegeben.
* Mit `cd [Pfad]` (steht für 'change directory') kann das Verzeichnis gewechselt werden. `cd` (ohne Pfadangabe) führt zurück ins Homeverzeichnis.
* Mit `mkdir [Ordnername]` (steht für 'make directory') kann ein neuer Ordner angelegt werden.
* Mit `cp [Ursprungsdatei] [Zieldatei]` (steht für 'copy') können Dateien kopiert, mit `mv [Ursprungsdatei] [Zieldatei]` (steht für 'move') verschoben (oder umbenannt) werden. Achtung: Eventuell bereits vorhandene Dateien am Ort `[Zieldatei]` werden ohne Rückfrage überschrieben!
* Mit `rm [Dateiname]` (steht für 'remove') können Dateien gelöscht werden. Soll ein Ordner gelöscht werden, muss stattdessen `rm -r [Ordnername]` verwendet werden. Achtung: Es wird nicht nach einer Bestätigung gefragt, die Dateien/Ordner werden sofort gelöscht.
* Um eine Textdatei schnell im Terminal auszugeben, wird `cat [Dateiname]` verwendet.
* Manche Befehle müssen als *root* ("Administrator") ausgeführt werden, dazu wird dem entsprechenden Befehl ein `sudo` vorgestellt.

### Ein paar Tipps

* Mit den Pfeiltasten nach oben und unten ist es möglich, durch die bereits benutzten Befehle zu scrollen. Das ist nützlich, wenn man einen langen Befehl häufiger ausführen möchte.
* Mit der *Tab*-Taste lassen u.a. Befehle und Pfade automatisch vervollständigen. Das spart viel Tipparbeit.
* Als professioneller Linuxnutzer bin ich verpflichtet auf die interne Dokumentation hinzuweisen, die sich für quasi alle Befehle mit `man [Befehl]` (steht für 'manual') aufrufen lässt. Diese sogenannten *man pages* enthalten alle Informationen, die man zu einem bestimmten Befehl wissen können wollte. Darunter aber eben auch viele Sachen, die man nicht unbedingt wissen muss. Daher ist es für Anfänger_innen häufig doch einfacher und sinnvoller die bevorzugte Suchmaschine zu bemühen.  

## Setup

### Installation von Node, Yarn und Hugo

**unter Windows (WSL) und Linux**:

Folgende Befehle in der Ubuntu Bash ausführen (vgl. [1](https://github.com/nodesource/distributions/blob/master/README.md#installation-instructions), [2](https://classic.yarnpkg.com/en/docs/install/#debian-stable), [3](https://gohugo.io/getting-started/installing#binary-cross-platform)):

```sh
# Evtl. ist curl schon installiert, dann schlägt dieser Befehl fehl. Das ist in Ordnung.
sudo apt install -y curl

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

sudo apt update

# Dieser Befehl schlägt u. U. mit der Meldung fehl, dass das Paket nicht installiert sei. Das ist in Ordnung.
sudo apt remove cmdtest

# Ggf. erscheint die Frage "Restart services during package upgrades without asking?" Dann "<Yes>" auswählen.
sudo apt install -y build-essential nodejs yarn

wget https://github.com/gohugoio/hugo/releases/download/v0.65.3/hugo_extended_0.65.3_Linux-64bit.deb
sudo dpkg -i hugo_extended_0.65.3_Linux-64bit.deb
rm hugo_extended_0.65.3_Linux-64bit.deb
```

**unter macOS**:

Folgenden Befehl im Terminal ausführen:

```sh
brew install node yarn hugo
```

**für alle Systeme:**

Zum Testen, ob die Installationen erfolgreich waren, die folgenden Befehle ausführen:

```sh
node --version
yarn --version
hugo version
```

### Installation von Visual Studio Code

**unter Linux:**

```sh
sudo snap install code --classic
```

**unter macOS:**

```sh
brew cask install visual-studio-code
```

**unter Windows:**

[hier](https://code.visualstudio.com/download) herunterladen und den Installer ausführen

Nach dem ersten Start erscheint unten rechts die Aufforderung "The 'Remote - WSL' extension is recommended…". Hier auf "Install" klicken.

Im Menü links befindet sich befindet sich unten das Icon *Remote Explorer* (Computer mit einem Kreis davor). Darauf klicken. Es sollte nun eine Liste mit der Überschrift "WSL TARGETS" und unserer "Ubuntu-18.04"-Installation erscheinen. Daneben auf das kleine Icon mit dem Plus klicken.  
Es öffnet sich ein neues VS Code-Fenster. Unten rechts sieht man, dass einige zusätzliche Komponenten installiert werden. Das abwarten.  
Ggf. erscheint ein "Windows Security Alert": "Windows Defender Firewall has blocked some features of this application". Hier muss "Allow access" ausgewählt werden.

Die Verbindung ist erfolgreich hergestellt, sobald unten links "WSL: Ubuntu-18.04" auf grünem Untergrund steht. Das erste VS Code-Fenster kann nun geschlossen werden.

### Einstellungen für VS Code

Im Menü links auf das *Extensions*-Icon (gevierteiltes Quadrat, bei dem ein Teil versetzt ist) klicken und über die Suche die folgenden Erweiterungen installieren:

* [Better TOML](https://marketplace.visualstudio.com/items?itemName=bungcip.better-toml)
* [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
* [eslint-disable-snippets](https://marketplace.visualstudio.com/items?itemName=drKnoxy.eslint-disable-snippets)
* [Hugo Language and Syntax Support](https://marketplace.visualstudio.com/items?itemName=budparr.language-hugo-vscode)
* [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Nach der Installation aller Erweiterungen auf den blauen *Relaod Required*-Button klicken.

*Ctrl* + *Shift* + *P* drücken und `settings` eingeben. Dann *Preferences: Open Settings (JSON)* auswählen. Dort den folgenden Inhalt hereinkopieren und speichern:

```js
{
    "workbench.editor.highlightModifiedTabs": true,
    "files.trimFinalNewlines": true,
    "files.insertFinalNewline": true,
    "files.trimTrailingWhitespace": true,
    "editor.wordWrap": "on",
    "editor.formatOnPaste": true,
    "editor.renderWhitespace": "boundary",
    "editor.formatOnSave": true,
    "editor.insertSpaces": true,
    "editor.rulers": [120],

    "prettier.printWidth": 120,
    "prettier.singleQuote": true,
    "prettier.jsxBracketSameLine": true,
    "prettier.tabWidth": 4,
    "prettier.disableLanguages": ["html", "vue", "md"],

    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[markdown]": {
        "files.trimTrailingWhitespace": false,
        "editor.formatOnSave": false
    },
    "[json]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[yaml]":{
        "editor.tabSize": 2,
        "editor.formatOnSave": false
    },
    "html.format.enable": false
}
```

### Einrichten der Repositories

* Zunächst mit `cd` ins Home-Verzeichnis gehen.
* Dort mit `mkdir datenanfragen` den Ordner `datenanfragen` anlegen.
* Mit `cd datenanfragen` in diesen Ordner wechseln.

#### `website`

* Den eigenen Fork des `website`-Repositories clonen: `git clone git@github.com:[username]/website.git`
* Mit `cd website` in dieses neue Verzeichnis wechseln.
* Mit `ls` können wir uns den Inhalt des Ordners anschauen, um zu prüfen, ob das geklappt hat.
* Dann `yarn && ./deploy.sh` ausführen, um alle Abhängigkeiten herunterzuladen.
* Um nun an der Webseite zu arbeiten, braucht es zwei Fenster:
  - Im ersten `yarn dev` ausführen. Dadurch werden alle Änderungen an den JavaScript-Dateien automatisch im Hintergrund kompiliert.
  - Im zweiten `hugo server` ausführen. Dadurch werden u.a. Änderungen an den Inhalten automatisch übernommen.
* Im Browser jetzt einer der Sprachversionen aufrufen:
  - deutsch: [`localhost:1313`](http://localhost:1313)
  - englisch: [`localhost:1314`](http://localhost:1314)
  - französisch: [`localhost:1315`](http://localhost:1315)
  
#### `data`

* Zurück ins `datenanfragen`-Verzeichnis gehen: `cd ~/datenanfragen`
* Den eigenen Fork des `data`-Repositories clonen: `git clone git@github.com:[username]/data.git`
* Mit `cd data` in dieses neue Verzeichnis wechseln.
* Dann `yarn` ausführen, um die notwendigen Abhängigkeiten zum Testen der Einträge herunterzuladen.
* Um die vorhandenen Einträge auf Fehler zu prüfen, einfach `yarn test` ausführen.
* Dieser Test wird auch automatisch ausgeführt, wenn ein Commit angelegt werden soll. Liegen Fehler vor, kann der Commit nicht ausgeführt werden.
