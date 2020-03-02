# PGP Kurs

## Was ist PGP?

- "Pretty Good Privacy"
- asymmetrischer Verschlüsselungsalgorithmus mit zwei Schlüssel:
  - public Key
    - öffentlich
    - wird an alle Kommunikationpartner_innen weitergegeben
    - verschlüsselt Nachrichten und verifiziert Signaturen
    - Analogie: Vorhängeschloss
  - private Key
    - muss unter Verschluss gehalten werden
    - entschlüsselt Nachrichten, erstellt Signaturen
    - Analogie: Schlüssel zum Vorhängeschloss
- Beachten: Schutz gegen PITM-Attacks durch Verifizieren der Fingerprints (eindeutige Kurzformen der Public Keys) -> Vertrauen in die Schlüssel aufbauen

## Einrichten

1. Thunderbird installieren/öffnen
2. Enigmail & GnuPG installieren
3. Enigmail einrichten, Schlüssel generieren (https://enigmail.net/index.php/en/user-manual/quick-start)
4. Schlüssel vom Vorstandskey signieren lassen

**Hinweis**: Für die Rechtsberatung verwenden wir einen Key für alle Berater_innen gemeinsam

## Mails versenden

1. *Schlüssel austauschen*  
  1. Schlüssel von anderen bekommen (von der Webseite runterladen (HTTPS!), aus dem Mailanhang (unsicher), persönlich, von Keyservern)
  2. Fingerprint abgleichen! (Persönlich, oder über einen zweiten trusted Channel)
    ![Schlüsselverwaltung in Enigmail](/res/screenshot-enigmail-key-management.png)
  3. Alternativ: Signatur des Schlüssels prüfen
2. *Email formulieren*
3. *Verschlüsselung und Signatur auswählen*  
![Verschlüsselung und Signatur auswählen](/res/screenshot-enigmail-options.png)
4. Abschicken

## Resources

- https://enigmail.net/index.php/en/user-manual/signature-and-encryption
