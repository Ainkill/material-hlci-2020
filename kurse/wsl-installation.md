# Installation von WSL (Windows Subsystem for Linux)

**Hinweis**: Die folgende Anleitung funktioniert nur unter Windows 10. Bitte darauf achten, dass möglichst alle Updates eingespielt sind, da WSL noch relativ neu ist und regelmäßig verbessert wird.

PowerShell als Admin starten: Windows-Taste drücken, `powershell` eingeben, Rechtsklick auf *Windows PowerShell*, dann *Run as administrator* klicken.

Folgenden Befehl eingeben und mit *Enter* bestätigen:  
`Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`

Es erscheint nach ein paar Minuten die Frage: *Do you want to restart the computer to complete this operation now?* Hier `Y` eingeben und *Enter* drücken.

Der Rechner startet neu. Wieder anmelden und PowerShell erneut als Admin starten.

Folgenden Befehl eingeben und mit *Enter* bestätigen:  
`Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1804 -OutFile Ubuntu.appx -UseBasicParsing`

Warten, bis der Befehl fertig ist (der blaue Hinweis *Writing web request* verschwindet und man wird zur Eingabe eines neuen Befehls aufgefordert).

Folgenden Befehl eingeben und mit *Enter* bestätigen:  
`Add-AppxPackage .\Ubuntu.appx`

Warten, bis der Befehl fertig ist.

Zum Sparen von Speicherplatz kann das Installationspaket nun gelöscht werden. Dazu den folgenden Befehl eingeben und mit *Enter* bestätigen:  
`rm .\Ubuntu.appx`

Das PowerShell-Fenster kann nun geschlossen werden.

Windows-Taste drücken und `ubuntu` suchen. Es sollte *Ubuntu 18.04* erscheinen. Das anklicken. Es erscheint ein Fenster mit dem Text *Installing, this may take a few minutes...*.

Nach einiger Zeit erscheint die Aufforderung: *Enter new UNIX username*. Hier einen beliebigen Benutzernamen eingeben und den merken (kann der gleiche sein wie bei Windows, muss aber nicht). Mit *Enter* bestätigen. Es erscheint die Frage: *Enter new UNIX password*. Hier ein beliebiges Passwort eingeben und merken. Mit *Enter* bestätigen. Es erscheint die Frage: *Retype new UNIX password*. Hier das gleiche Passwort erneut eingeben und mit *Enter* bestätigen.

Es sollte nun eine Zeile erscheinen, die so ähnlich aussieht (aber mit anderem Benutzer- und Computernamen):  
`benni@DESKTOP-A9B7UD5:~$`

Hier zum Testen Folgendes eingeben:  
`lsb_release -a`

Es sollte folgende Ausgabe erscheinen:  
```
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.1 LTS
Release:        18.04
Codename:       bionic
```

Die Installation ist nun abgeschlossen.
