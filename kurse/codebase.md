# Struktur von Datenanfragen.de

## Repositories

- *datenanfragen/website*  
  Kernrepository mit dem gesamten Code für die Webseite (Artikel, Generator, …)
- *datenanfragen/data*  
  Datenbank für Unternehmen, Templates und Aufsichtsbehörden, Deploy für die Suche
- *datenanfragen/company-json-generator*  
  Tool zur Erstellung von Einträgen in die Datenbank
- *datenanfragen/letter-generator*  
  Teil des Generators, der PDFs und Emails aus den Anfragedaten erstellt
- *datenanfragen/locate-contacts-addon*  
  Addon für Firefox, um das Überprüfen von Datenbankeinträgen zu erleichtern
- *baltpeter/yace*  
  Comment Engine, die Datenanfragen.de verwendet
- *zner0L/serverless-donations*  
  Setup für die Serverseite des Spendenwidgets
- *zner0L/postcss-fonticons*  
  Plugin, um mit Postcss Fonticons zu erstellen

## Infrastruktur

- Amazon Web Services (AWS)  
  - Suchserver
    - Amazon EC2 mit typesense
    - Deployment über GitHub mit python Skript
    - Wird \*hoffentlich\* bald deprecated
  - Spendenwidget Server
    - AWS Lamda
    - Relay für Anfragen an unsere Payment Provider
  - Object Storage
    - AWS S3 Object Storage
    - Für statische Dateien (Bilder, Downloads etc.)
    - Backups etc.
    
- Netlify
  - Static Site Hosting
  - Deploy über GitHub (siehe deploy.sh)
  
## Code

- Hauptsprachen sind hugo flavoured HTML und Javascript
- In JS benutzen wir für die Benutzer_innenoberfläche vor allem `preact`, ein React Derivat, das sehr viel kleiner ist
  - Die Komponenten definieren wir in der React-eigenen Sprache JSX (eine Mischung aus HTML und JS)
  - State Management machen wir von Hand
- Wir versuchen so viel wie möglich ohne externe Dependencies zu machen, um Build Time und Größe der Produkte zu sparen (klappt aber nur so mittel)

### Build

- Seite wird mit `hugo` generiert
  - Static Site Generator
  - nimmt **HTML** Templates und füllt sie mit **Markdown**-Inhalt
- Restlicher Build wird von `yarn` bzw. `webpack` gestemmt
  - CSS wird in **SCSS** definiert und mit `sass` und `postcss` gebaut
  - **JavaScript**/**JSX** wird mit `babel` übersetzt und mit `terser` komprimiert
- Die Datenbank wird in den content geklont (siehe deploy.sh)

### Ordnerstruktur

![Die Ordnerstruktur des website-Repositories](/res/screenshot-codebase-folders.png)

`src/` noch etwas genauer:

![Die Struktur des src/-Ordners](/res/screenshot-codebase-src-folder.png)
