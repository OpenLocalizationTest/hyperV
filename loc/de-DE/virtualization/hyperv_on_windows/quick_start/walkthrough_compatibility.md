# Schritt 1: Stellen Sie sicher, dass Ihre Maschine Hyper-V ausgeführt werden können

Nur Windows 10 Pro und Windows 10 Enterprise unterstützt Hyper-V.

> Wenn Sie Windows 10 Home--ausführen können Sie in der Aktivierungs-Seite befindet sich in den Sicherheitseinstellungen auf Win 10 Pro aktualisieren. 

Hyper-V ist nicht verfügbar in Windows 10 Mobile / Windows 10 Mobile Enterprise

Hyper-V erfordert mindestens 4 GB RAM, aber Sie brauchen mehr, wenn Sie mehrere virtuelle Computer gleichzeitig ausführen möchten.

Ab Windows 10, erfordert Hyper-V einen 64-Bit-Prozessor mit Second Level Address Translation (Stab).

## Überprüfen Sie die Hardware-Kompatibilität

Um Kompatibilität zu überprüfen, öffnen Sie PowerShell oder eine Windows-Eingabeaufforderung (cmd.exe) und Typ:'systeminfo.exe'. 

Alle Elemente unter ** Hyper-V Anforderungen ** müssen den Wert wenn ** ja **.

![](media\systeminfo.png)

Relevanten Bereichen:
*  'OS Name'--muss Windows 8 oder höher und Beruf oder Enterprise.
*  "Hyper-V-Anforderungen"--all dies muß wahr (Wert "Yes"), aber einige können im BIOS eingestellt werden.
	*  'VM Monitor Modus Erweiterungen'--Eigenschaft der Hardware. 
	*  'Virtualisierung in Firmware aktiviert'--sein im BIOS aktiviert
	*  'Second Level Address Translation'--Eigenschaft der Hardware. 
	*  "Data Execution Prevention verfügbar"--kann im BIOS aktiviert sein
	
Wenn Hyper-V bereits aktiviert ist, liest der Abschnitt über die Hyper-V-Anforderungen:  
```
Hyper-V Requirements: A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```

## Nächster Schritt: 
[Schritt 2: Installieren von Hyper-V] (walkthrough_install.md)