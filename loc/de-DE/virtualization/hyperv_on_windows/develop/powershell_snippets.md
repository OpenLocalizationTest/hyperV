# PowerShell-Snippets

PowerShell ist ein genial Skripting, Automatisierung und Management-Tool für Hyper-V.  Hier ist eine Toolbox zu erkunden einige der tollen Dinge tun kann!

Alle Hyper-V-Management erfordert ausführen als Administrator übernehmen also alle Skripts und Ausschnitte als Administrator werden, von einem Hyper-V-Administrator-Konto ausgeführt müssen.

Wenn Sie sich nicht sicher, ob Sie die richtigen Berechtigungen verfügen, geben Sie "Get-VM" und wenn es ohne Fehler ausgeführt wird, sind Sie bereit zu gehen.


## PowerShell-Direct-Werkzeuge
Alle Skripte und Ausschnitte in diesem Abschnitt wird auf die folgenden Grundlagen verlassen.

** Anforderungen **:  
*  PowerShell-Direct. 

** Gemeinsame Variablen **: '$VMName'--Dies ist ein String mit dem VMName.  Finden Sie eine Liste der verfügbaren VMs mit 'Get-VM' '$cred'--Anmeldeinformationen für das Betriebssystem des Gastes.  Kann gefüllt werden mit ' $cred = Get-Credential "  

### Prüfen Sie, ob der Gast gestartet wurde

Hyper-V-Manager geben nicht Sie Einblick in das Gastbetriebssystem, oft ist es schwierig zu wissen, ob der Gast OS gebootet hat.

Verwenden Sie diesen Befehl, um festzustellen, ob der Gast gestartet ist.

``` PowerShell
if((Invoke-Command -VMName $VMName -Credential $cred {"Test"}) -ne "Test"){Write-Host "Not Booted"} else {Write-Host "Booted"}
```  

** Ergebnis ** Drucke eine freundliche Meldung deklarieren den Zustand der das Betriebssystem des Gastes.


### Skript sperren, bis der Gast gestartet wurde

Die folgende Funktion wartet verwendet das gleiche Prinzip zu warten, bis die PowerShell gibt es in der Gast (d. h. das OS gebootet hat und die meisten Dienste ausgeführt werden) und danach wieder.

``` PowerShell
function waitForPSDirect([string]$VMName, $cred){
   Write-Output "[$($VMName)]:: Waiting for PowerShell Direct (using $($cred.username))"
   while ((Invoke-Command -VMName $VMName -Credential $cred {"Test"} -ea SilentlyContinue) -ne "Test") {Sleep -Seconds 1}}
```

** Ergebnis ** Drucke eine freundliche Meldung und sperren, bis der Anschluss an die VM erfolgreich ist.  
Erfolgreich im Hintergrund.

### Skript sperren, bis der Gast ein Netzwerk hat
Mit PowerShell-Direct ist es möglich, angeschlossen an eine PowerShell-Sitzung in einer virtuellen Maschine vor der virtuellen Maschine erhalten hat eine IP-Adresse erhalten.

``` PowerShell
# Wait for DHCP
while ((Get-NetIPAddress | ? AddressFamily -eq IPv4 | ? IPAddress -ne 127.0.0.1).SuffixOrigin -ne "Dhcp") {sleep -Milliseconds 10}
```

** Ergebnis **
Sperren, bis eine DHCP-Lease erhalten ist.  Da dieses Skript kein bestimmtes Subnetz oder IP-Adresse, auf der Suche nach ist es funktioniert egal welche Netzwerkkonfiguration verwenden Sie.  
Erfolgreich im Hintergrund.

## Verwalten von Anmeldeinformationen mit PowerShell
Hyper-V-Skripts erfordern häufig die Behandlung von Anmeldeinformationen für einen oder mehrere virtuelle Maschinen, Hyper-V-Host oder beides.

Es gibt mehrere Möglichkeiten, Sie können dies erreichen, beim Arbeiten mit PowerShell Direct oder Norm PowerShell-Remoting:

1. Die erste (und einfachste) Weg soll haben dieselben Anmeldeinformationen in der und der Gast oder lokale und remote-Host gültig sein.  
  Dies ist ganz einfach, wenn Sie sich mit Ihrem Microsoft-Konto - anmelden oder wenn Sie in einer Domänenumgebung.  
  In diesem Szenario führen Sie einfach 'Invoke-Command - VMName "test {Get-Process}" '.

2. Lassen Sie PowerShell-Eingabeaufforderung erhalten Sie zur Eingabe von Anmeldeinformationen, wenn Sie Ihre Anmeldeinformationen nicht übereinstimmen automatisch ein Administratoranmeldeaufforderung, so dass Sie die entsprechenden Anmeldeinformationen für die virtuelle Maschine zur Verfügung zu stellen.

3. Speichern von Anmeldeinformationen in einer Variablen für die Wiederverwendung.
  Einen einfachen Befehl wie folgt ausgeführt:  
  ``` PowerShell
  $localCred = Get-Credential
   ```
  Und dann etwas wie folgt ausführen:
  ``` PowerShell
  Invoke-Command -VMName "test" -Credential $localCred  {get-process} 
  ```
  Bedeutet, dass Sie nur einmal pro Skript/PowerShell-Sitzung für Ihre Anmeldeinformationen aufgefordert.

4. Codieren Sie Ihre Anmeldeinformationen in Skripts.  ** Nicht für echte Arbeitsauslastung oder System **
 > Warnung: _Do nicht in einem Produktionssystem.  Tun Sie dies nicht mit echten Passwörtern. _
  
  Sie können mit der hand Handwerk ein PSCredential-Objekt mit einigen Code wie folgt:  
  ``` PowerShell
  $localCred = New-Object -typename System.Management.Automation.PSCredential -argumentlist "Administrator", (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force) 
  ```
  Grob unsicher- aber für Testzwecke.  

