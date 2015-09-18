ms. ContentId: 5bbac9eb-c31e-40db-97b1-f33ea59ac3a3
Titel: In Arbeit

# In Arbeit

Wenn Sie nicht, Ihr Problem angesprochen sehen oder Fragen haben, kannst du sie im [Forum] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).

-----------------------

## Allgemeine Funktionalität

### Windows-Container-Abbild muss genau mit dem Container Host übereinstimmen.
Ein Windows-Server-Container erfordert ein Betriebssystemabbild, die den Container-Host in Hinsicht zu bauen und patch-Level entspricht. 

Wenn Sie Updates gegen Windows Container Host OS installieren, die Sie den Container Basis aktualisieren müssen, aktualisiert Abbild des Betriebssystems zu den passenden haben.
<!-- Can we give examples of behavior or errors?  Makes it more searchable -->

** Work Around: ** herunterladen und installieren ein Abgleich der OS Version und Patch-Ebene des Hosts Container Container-Basisabbild.


### Sporadisch Befehle fehl--versuchen Sie es erneut
Bei unseren Tests müssen Befehle gelegentlich mehrmals ausgeführt werden.  Das gleiche Prinzip gilt für andere Aktionen.  
Beispielsweise wenn Sie eine neue Datei erstellen, und es erscheint nicht, versuchen Sie die Datei zu berühren.  

Wenn Sie haben, dies zu tun, lassen Sie uns wissen über [Foren] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).

** Arbeit herum: ** Build-Skripte, so dass sie Befehle mehrmals versuchen.   

### Alle nicht-C: / in neue Behälter werden die Laufwerke automatisch zugeordnet.
Alle nicht-C: / verfügbare Laufwerke an den Container-Host werden automatisch in neue ausgeführten Windows Server Container zugeordnet.

Zu diesem Zeitpunkt besteht keine Möglichkeit auf selektiv anzeigen Ordner in einen Container wie ein vorläufiger Workaround Laufwerke werden automatisch zugeordnet.

** Work Around: ** Wir arbeiten dran. 


### Windows Server-Container sind sehr langsam
Wenn Ihr Container zum Starten länger als 30 Sekunden dauert, kann es viele doppelte Virenscans durchführen.

Viele Anti-Malware-Lösungen wie Windows Defender, vielleicht unnötig Scannen Dateien mit-in Container Bilder einschließlich aller der OS-Programme und Dateien in das Container-OS-Bild.  Dies geschieht, wann immer ein neuer Container erstellt und aus Sicht der Anti-Malware aller "Container Dateien" sehen aus wie neue Dateien, die zuvor nicht gescannt wurden.  Also Prozesse innerhalb des Containers versuchen, diese Dateien zu lesen einscannen die Anti-Malware-Komponenten zuerst bevor Zugriff auf die Dateien.  In Wirklichkeit wurden diese Dateien bereits gescannt, wenn das Container-Bild importiert oder auf den Server gezogen wurde.  

--------------------------

## Vernetzung

### Netzwerk Abteilzahl pro container
In dieser Version unterstützen wir ein Netzwerk-Fach pro Container. Dies bedeutet, dass wenn Sie einen Container mit mehreren Netzwerkkarten haben, Sie den gleichen Netzwerk-Port für die einzelnen Adapter (z.B. nicht zugreifen können 

** Work Around: ** Wenn mehrere Endpunkte von einem Container verfügbar gemacht werden müssen, verwenden Sie NAT Port-Mapping.

### Windows-Container sind nicht immer IPs
Wenn Sie die Windows Server-Container mit VM-Switches DHCP herstellen, ist es möglich für den Container-Host eine IP-Wwhile zu erhalten, die die Container nicht zu tun.

Die Behälter erhalten eine 169.254. ***. *** APIPA-IP-Adresse.

** Arbeit herum: **
Dies ist ein Nebeneffekt der Austausch des Kernels. 

MAC-Address-spoofing auf dem Container-Host zu aktivieren.

Dies kann erreicht werden mit PowerShell
```
Get-VMNetworkAdapter -VMName "[YourVMNameHere]"  | Set-VMNetworkAdapter -MacAddressSpoofing On
```

### Erstellen von Dateifreigaben, funktioniert nicht in einem Container

Derzeit ist es nicht möglich, erstellen eine Dateifreigabe innerhalb eines Containers. Beim Ausführen von 'net Share' sehen Sie einen Fehler wie folgt:

```
The Server service is not started.

Is it OK to start it? (Y/N) [Y]: y
The Server service is starting.
The Server service could not be started.

A service specific error occurred: 2182.

More help is available by typing NET HELPMSG 3547.
```

** Arbeit herum: **
Wenn Sie, kopieren Sie die Dateien in einen Container möchten können anders Runde Sie durch Ausführen von 'net Use' innerhalb des Containers.  
```
net use S: \\your\sources\here /User:shareuser [yourpassword]
```

--------------------------

## Anwendungskompatibilität

Es gibt so Mnay Fragen darüber, welche Anwendungen funktionieren und nicht in Windows Server Container arbeiten, wir beschlossen, Anwendung Kompatibilität Informationen in [einen eigenen Artikel] zu brechen (.. / reference/app_compat.md).

Einige der am häufigsten auftretenden Probleme liegen hier auch.

### WinRM startet nicht in einem Windows-Server-Container
WinRM beginnt, löst einen Fehler aus und wieder stoppt. 

** Arbeit herum: **
Verwenden Sie WMI, [RDP](#RemoteDesktopAccessOfContainers) oder geben Sie-PSSession - ContainerID

### Nicht installieren ASP.NET 4.5 oder ASP.NET 3.5 mit IIS in einem Container mithilfe von DISM 
Installieren von IIS-ASPNET45 in einem Container funktioniert nicht in einem Windows Server-Container. 

``` PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ASPNET45
```

Dies schlägt fehl, da ASP.NET 4.5 nicht in einem Container ausgeführt wird.

** Work Around: ** Installieren Sie stattdessen die Webserverrolle um IIS verwenden.  

``` PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName Web-Server
```

Finden Sie im [Anwendung Kompatibilität Artikel] (.. / reference/app_compat.md) für weitere Informationen über welche Anwendungen containerisierte werden können.

--------------------------


## Hafenarbeiter Verwaltung

### Hafenarbeiter Kunden standardmäßig ungesichert
In dieser Vorversion ist Hafenarbeiter Kommunikation öffentlich, wenn Sie wissen, wo Sie suchen.

### Hafenarbeiter-Befehle nicht mit Windows Server-Container funktionieren

Befehle, die fehlschlagen bekanntermaßen:

| ** Docker Befehl ** | ** Wo es läuft ** | ** Fehler ** | ** Hinweise ** |
|:-----|:-----|:-----|:-----|
| ** Hafenarbeiter Commit ** | Bild | Docker Container beendet und nicht korrekte Fehlermeldung anzeigen | Eine gestoppte Container-Werke zu begehen. Für die Ausführung von Containern: Wir arbeiten dran :) |
| ** Hafenarbeiter Diff ** | Dämon | Fehler: Windows-Graphdriver unterstützt keine Changes() ||
| ** Hafenarbeiter töten ** | Container | Fehler: Ungültiges Signal: KILL-Fehler: Fehler beim Container töten: [] ||
| ** Hafenarbeiter laden ** | Bild | Im Hintergrund fehl | Kein Fehler, aber das Bild ist nicht entweder laden |
| ** Hafenarbeiter anhalten ** | Container | Fehler: Windows-Container kann nicht angehalten werden.  Möglicherweise nicht unterstützt ||
| ** Hafenarbeiter Anschluss ** | Container |  | Wird kein Port aufgelistet bekommen auch wir sind in der Lage zu RDP.
| ** Hafenarbeiter ziehen ** | Dämon | Fehler: System kann den Pfad nicht finden. Wir können Container mit diesem Image ausgeführt werden. | Bild wird hinzugefügt bekommen kann nicht verwendet werden.  Wir arbeiten dran :) |
| ** Hafenarbeiter Neustart ** | Container | Fehler: Ein Herunterfahren des Systems ist im Gange. |  |
| ** Hafenarbeiter Neustarten ** | Container |  | Kann nicht testen weil anhalten noch nicht funktioniert. 

Wenn überhaupt, die nicht auf dieser Liste fehlschlägt (oder wenn ein Befehl fehlschlägt, anders als erwartet), lassen Sie uns wissen über [Foren] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).



### Hafenarbeiter-Befehle, die teilweise mit Windows Server-Container

Befehle mit teilweise Funktionalität:

| ** Docker Befehl ** | ** Läuft auf... ** | ** Parameter ** | ** Hinweise ** |
|:-----|:-----|:-----|:-----|
| ** Hafenarbeiter anfügen ** | Container | --keine-Stdin = False | Der Befehl nicht beenden, wenn STRG-P und STRG-Q gedrückt wird |
| | | --Sig-Proxy = True | funktioniert |
| ** Hafenarbeiter Build ** | Bilder | -f,--Datei | Fehler: Nicht in der Lage, Kontext vorzubereiten: keine Synlinks erhalten |
| | | --Kraft-Rm = False | funktioniert |
| | | --keine-Cache = False | funktioniert |
| | | -Q,--ruhig = False ||
| | | --Rm = True | Works|
| | | -t,--Tag = "" | funktioniert |
| ** Hafenarbeiter Anmeldung ** | Dämon | -e, -p, -u | sporratic Verhalten | 
| ** Hafenarbeiter drücken ** | Dämon || Immer gelegentliche Störungen "Repository beendet nicht". |
| ** Hafenarbeiter Rm ** | Container | -f | Fehler: Ein Herunterfahren des Systems ist im Gange. 

Wenn alles, was auf dieser Liste ist nicht fehlschlägt, wenn ein Befehl fehlschlägt, anders als erwartet, oder wenn Sie eine Arbeit herum finden, lassen Sie uns wissen über [Foren] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).


### Befehle zum interaktiven Docker-Sitzung einfügen ist begrenzt auf 50 Zeichen
Wenn Sie eine Befehlszeile in einer interaktiven Sitzung Docker kopieren, ist es derzeit auf 50 Zeichen beschränkt. 

Dies ist nicht beabsichtigt, wir arbeiten an der Aufhebung der Beschränkung.

### net Use gibt Systemfehler 1223 anstatt für Benutzername oder Kennwort aufzufordern
Problemumgehung: Geben Sie sowohl, der Benutzername und das Kennwort, beim Ausführen von net verwenden. 
```
net use S: \\your\sources\here /User:shareuser [yourpassword]
``` 

### HCS-Shim-Fehler beim Erstellen von neuen Container-images
Wenn Sie Fehlermeldungen wie folgt auftreten:
```
hcsshim::ExportLayer - Win32 API call returned error r1=2147942523 err=The filename, directory name, or volume label syntax is incorrect. layerId=606a2c430fccd1091b9ad2f930bae009956856cf4e6c66062b188aac48aa2e34 flavour=1 folder=C:\ProgramData\docker\windowsfilter\606a2c430fccd1091b9ad2f930bae009956856cf4e6c66062b188aac48aa2e34-1868857733
```

Sie sind ein Problem angesprochen durch die Zero Day-Patch für Windows Server 2016 TP3 treffen. 

Wenn Sie andere Fehler Hcsshim schlagen, lassen Sie uns wissen über [Foren] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).


## Zugriff auf Windows-Server-Container mit Remotedesktop 
Windows Server-Container kann es geschafft/mit interagiert über eine RDP-Sitzung sein.

Folgende Schritte sind erforderlich, Herstellen einer Remoteverbindung mit einem Windows-Server-Container über RDP. Es wird angenommen, dass der Container mit dem Netzwerk über einen NAT-Switch verbunden ist. 

** Im Container Sie herstellen möchten **

Die folgenden Schritte erfordern, Verwaltung der Container mit Docker oder, bei Verwendung von PowerShell ist die Angabe von der '-RunAsAdministrator' beim Herstellen einer Verbindung mit des Containers zu wechseln. 

1. Der Container-IP-Adresse beziehen

  ```
  ipconfig
  ```
  
  Gibt es etwas ähnliches wie das
  
  ```
  Windows IP Configuration

  Ethernet adapter vEthernet (Virtual Switch-f758a5a9519e1956cc3bef06eb03e5728d3fb61cf6d310246185587be490210a-0):

  Connection-specific DNS Suffix  . :
  Link-local IPv6 Address . . . . . : fe80::91cd:fb4c:4ea5:51df%17
  IPv4 Address. . . . . . . . . . . : 172.16.0.2
  Subnet Mask . . . . . . . . . . . : 255.240.0.0
  Default Gateway . . . . . . . . . : 172.16.0.1
  ```
  
  Bitte beachten Sie die IPv4-Adresse in der Regel in der Format-172.16.x.x

2. Legen Sie das Kennwort für das vordefinierte Administrator-Benutzer für den Container

  ```
  net user administrator [yourpassword]
  ```

3. Für den Container den Builtin-Administrator-Benutzer aktivieren

  ```
  net user administrator /active:yes
  ```

** Auf dem Host Container **

Seit Windows Server die Windows-Firewall mit erweiterter Sicherheit standardmäßig aktiviert hat, wir müssen einige Ports für die Kommunikation in Reihenfolge für RDP funktioniert geöffnet. 

Die folgenden Schritte erfordern eine PowerShell als Administrator auf dem Container-Host gestartet.

1. Erlauben Sie es, die Standard RDP-Port durch die erweiterte Windows-Firewall

  ```
  New-NetFirewallRule -Name "RDP" -DisplayName "Remote Desktop Protocol" -Protocol TCP -LocalPort @(3389) -Action Allow
  ```

2. Ermöglichen Sie einen zusätzlichen Anschluss für RDP-Verbindung auf den Container

  ```
  New-NetFirewallRule -Name "ContainerRDP" -DisplayName "RDP Port for connecting to Container" -Protocol TCP -LocalPort @(3390) -Action Allow
  ```
  
  Dieser Schritt eröffnet Port 3390 auf dem Container-Host. Es wird verwendet um eine RDP-Sitzung auf den Container zu öffnen.  

3. Fügen Sie eine Portzuordnung für die vorhandenen NAT

  In diesem Schritt benötigen Sie die IP-Adresse aus Schritt 1 innerhalb des Containers

  ```
  Add-NetNatStaticMapping -NatName ContainerNAT -Protocol TCP -ExternalPort 3390 -ExternalIPAddress 0.0.0.0 -InternalPort 3389 -InternalIPAddress [your container IP]
  ```
  
  Hier stellen Sie sicher, dass Kommunikation mit den Container-Host die Port 3390 in kommt umgeleitet werden, auf Port 3389 für den Container laufen auf die IP-Adresse, die Sie angeben.

** Schließen Sie an den Container über RDP **

Schließlich können Sie auf den Container mit RDP verbinden. Um führe die bitte den folgenden Befehl auf einem System die Remote Desktop Client (z. B. installiert hat  

```
mstsc /v:[ContainerHostIP]:3390 /prompt
```

Geben Sie bitte 'Administrator' als den Benutzernamen und das Kennwort, das Sie als Passwort gewählt haben.

Die Remotedesktopverbindung wird Sie Fragen, ob das System trotz Zertifikatfehler herstellen soll.   

** Hinweis: ** die Container-RDP-Sitzung zu beenden, ohne Abmeldung des Containers aus herunterfahren verhindern kann. 

--------------------------

## PowerShell-Verwaltung

### Geben Sie-PSSession hat Containerid Argument, nicht New-PSSession

Dies ist korrekt. 


Zögern Sie nicht zu Stimme-Feature-Anfragen im [Forum] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers). 

--------------------------
[Zurück zur Container-Startseite] (.. / containers_welcome.md)