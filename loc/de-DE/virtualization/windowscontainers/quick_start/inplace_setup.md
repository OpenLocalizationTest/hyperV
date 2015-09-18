ms. ContentId: 44b138bb-962f-4474-a0c4-284646a872e2
Titel: Setup Windows Container im Ort

# Vorbereitung einer physischen Maschine oder eine vorhandene virtuelle Maschine für Windows-Server-Container


Um erstellen und Verwalten von Windows-Server-Container, muss die Technical Preview des Windows-2016-Umgebung bereit.  

> Andere erste Schritte Leitfäden:
  * Führen Sie Windows-Server-Container im [Azure] (./azure_setup.md).
  * Führen Sie Windows-Server-Container in [einer neuen Hyper-V VM] (./container_setup.md).

  ** Bitte lesen Sie vor der Installation des BETRIEBSSYSTEMABBILDS CONTAINER: ** die Lizenzbedingungen von Microsoft Windows Server Pre-Release-Software ("Lizenzbedingungen") gelten für Ihre Verwendung des Microsoft Windows-Container-Betriebssystemabbilds Supplement ("zusätzliche Software).  Durch das herunterladen und benutzen die ergänzende Software, stimmen Sie den Lizenzbedingungen und Sie dürfen es nicht verwenden, wenn Sie nicht die Lizenzbedingungen akzeptiert haben.   

** System (oder VM) Anforderungen: **
* System Windows Server Technical Preview 3 Server Core ausgeführt.
* 10GB Speicherplatz für Base Betriebssystemabbild und Setup-Skripten.
* Administratorberechtigungen auf dem Computer oder VM.

## Einrichtung eine vorhandene virtuelle Maschine oder Bare Metal Host für Container
Windows Server Container erfordern das Container-OS-Basis-Bild. Wir haben ein Skript, das herunter und installieren Sie diese für Sie zusammengestellt. 

Starten Sie eine PowerShell-Sitzung als Administrator. 

``` powershell
powershell.exe
```

Stellen Sie sicher, dass der Titel der Fenster "Administrator: Windows PowerShell" ist. 

``` powershell
start-process powershell -Verb runas
```

Verwenden Sie den folgenden Befehl, um das Setup-Skript herunterladen. Das Skript kann auch manuell aus dieser Lage - [Konfigurationsskript] (http://aka.ms/setupcontainers) heruntergeladen werden.
 
``` PowerShell
wget -uri https://aka.ms/setupcontainers -OutFile C:\ContainerSetup.ps1
```
   
 Nachdem der Download abgeschlossen ist, führen Sie das Skript.
``` PowerShell
C:\ContainerSetup.ps1
```

Das Skript beginnt dann herunterladen und konfigurieren die Windows Server-Container-Komponenten. Dieser Prozeß dauert schon seit einiger Zeit aufgrund der großen Download. Die Maschine kann während des Prozesses neu gestartet.  

 Mit diesen Elementen abgeschlossen sollte dein System für Windows-Server-Container bereit sein. 


## Nächste Schritte - starten mithilfe von Containern

Nun, da die Ausführung von Windows-Server-Container, springen Sie zu den folgenden Anleitungen zum Arbeiten mit Windows Server-Container und Container für Windows-Server-Bildern beginnen. 
 
[Quick-Start: Windows Server Container und Docker] (. / manage_docker.md) 

[Quick-Start: Windows Server Container und PowerShell] (. / manage_powershell.md) 

-------------------

[Zurück zur Container-Startseite] (.. / containers_welcome.md) [bekannte Probleme bei der aktuellen Version] (.. / about/work_in_progress.md)