ms. ContentId: 71a03c62-50fd-48dc-9296-4d285027a96a
Titel: Setup Windows Container in einer lokalen VM

# Vorbereiten von Windows Server Technical Preview für Windows-Server-Container

Um erstellen und Verwalten von Windows-Server-Container, muss die Technical Preview des Windows-2016-Umgebung bereit. 

> Andere erste Schritte Leitfäden:
  * Führen Sie Windows-Server-Container im [Azure] (./azure_setup.md).
  * Führen Sie Windows-Server-Container in [einer vorhandenen virtuellen Maschine] (./inplace_setup.md).
  * Setup von Windows Server Container [auf eine physische Windows Server Core-Installation] (./inplace_setup.md).

  ** Bitte lesen Sie vor der Installation des BETRIEBSSYSTEMABBILDS CONTAINER: ** die Lizenzbedingungen von Microsoft Windows Server Pre-Release-Software ("Lizenzbedingungen") gelten für Ihre Verwendung des Microsoft Windows-Container-Betriebssystemabbilds Supplement ("zusätzliche Software).  Durch das herunterladen und benutzen die ergänzende Software, stimmen Sie den Lizenzbedingungen und Sie dürfen es nicht verwenden, wenn Sie nicht die Lizenzbedingungen akzeptiert haben.   

* System unter Windows 10 / Windows Server Technical Preview 2 oder höher.
* Hyper-V-Rolle aktiviert ([siehe Anweisungen] (https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install#UsingPowerShell)).
* 20GB Speicherplatz für Container Host Bild, Abbild des Betriebssystems-Base und Setup-Skripts.
* Administratorberechtigungen auf dem Hyper-V-Host.

> Windows Server Container erfordern keine Hyper-V, aber die Dinge einfach halten dieses Handbuch setzt voraus, dass eine Hyper-V-Umgebung verwendet wird, um den Container für Windows-Server-Host ausgeführt.

## Einen neuer Container-Host auf einen neuen virtuellen Computer einrichten
Windows Server Container bestehen aus mehreren Komponenten wie die Windows-Server-Host-Container und Container Betriebssystemabbild Base. Wir haben ein Skript, das herunterladen und konfigurieren Sie diese Elemente für Sie zusammengestellt. 

Starten Sie eine PowerShell-Sitzung als Administrator. 

``` powershell
start-process powershell -Verb runAs
```

Verwenden Sie den folgenden Befehl, um das Konfigurationsskript herunterzuladen. Das Skript kann auch manuell aus dieser Lage - [Konfigurationsskript] (http://aka.ms/newcontainerhost) heruntergeladen werden.
 
``` PowerShell
wget -uri https://aka.ms/newcontainerhost -OutFile New-ContainerHost.ps1
```
   
Führen Sie folgenden Befehl zum Erstellen und konfigurieren den Host Container wo '<containerhost>' wird sein Name der virtuellen Maschine und '<password>' wird das Konto Administrator zugewiesene Kennwort sein.</password> </containerhost>

``` powershell
.\New-ContainerHost.ps1 –VmName <containerhost> -Password <password>
```
  
Wenn das Skript beginnt werden Sie lesen und akzeptieren der Lizenzbedingungen aufgefordert werden.

```
Before installing and using the Windows Server Technical Preview 3 with Containers virtual machine you must:
    1. Review the license terms by navigating to this link: http://aka.ms/WindowsServerTP3ContainerVHDEula
    2. Print and retain a copy of the license terms for your records.
By downloading and using the Windows Server Technical Preview 3 with Containers virtual machine you agree to such
license terms. Please confirm you have accepted and agree to the license terms.
[N] No  [Y] Yes  [?] Help (default is "N"): Y
```

Das Skript beginnt dann herunterladen und konfigurieren die Windows Server-Container-Komponenten. Dieser Prozeß dauert schon seit einiger Zeit aufgrund der großen Download.   

Sie können die folgende Meldung während der Fenster-Servercontainer Host Bereitstellung. 
```
This VM is not connected to the network. To connect it, run the following:
Get-VM | Get-VMNetworkAdapter | Connect-VMNetworkAdapter -Switchname <switchname>
```  
In diesem Fall überprüfen Sie die Eigenschaften des virtuellen Computers, und schließen Sie die virtuelle Maschine an einen virtuellen Switch. Sie können auch den folgenden PowerShell-Befehl ausführen wo '<switchname>' ist der Name der virtuellen Hyper-V-Schalter, der Sie den virtuellen Computer herstellen möchten.</switchname>

``` powershell 
Get-VM | Get-VMNetworkAdapter | Connect-VMNetworkAdapter -Switchname <switchname>
```

Wenn das Konfigurationsskript abgeschlossen wurde, starten Sie die virtuelle Maschine. 
  
<center>! [] (. / media/containerhost2.png)</center><br />
  
Schließlich melden Sie sich bei der virtuellen Maschine mit dem Kennwort während des Konfigurationsprozesses angegeben und stellen Sie sicher, dass die virtuelle Maschine eine gültige IP-Adresse hat.  

## Video-Anleitung

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Configure-Windows-Server-Containers-on-a-Local-System/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>


## Nächste Schritte - starten mithilfe von Containern

Jetzt haben Sie einen Windows-Server-2016 System läuft das Feature Windows Server-Container zu den folgenden Handbüchern zu beginnen, arbeiten mit Windows-Server-Container und Container für Windows-Server Bilder springen. 
 
[Quick-Start: Windows Server Container und Docker] (. / manage_docker.md) 

[Quick-Start: Windows Server Container und PowerShell] (. / manage_powershell.md) 

-------------------

[Zurück zur Container-Startseite] (.. / containers_welcome.md) [bekannte Probleme bei der aktuellen Version] (.. / about/work_in_progress.md)
