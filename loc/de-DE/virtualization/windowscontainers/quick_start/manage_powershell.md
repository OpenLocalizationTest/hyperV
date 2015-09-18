ms. ContentId: d0a07897-5fd2-41a5-856d-dc8b499c6783
Titel: Windows-Server-Container mit PowerShell verwalten

# Schnellstart: Windows Server Container und PowerShell

In diesem Artikel gehen durch die Grundlagen der Verwaltung von Windows-Server-Container mit PowerShell. Angesprochenen Themen umfassen Windows Server Container und Windows-Server-Container-Abbilder erstellen, Entfernen von Windows-Server-Container und Container-Bilder und schließlich Bereitstellen einer Anwendung in einem Windows-Server-Container. 

Haben Sie Fragen? Fragen sie im [Windows Containern Forum] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).

> ** Hinweis: ** Windows Server Container mit PowerShell erstellt können nicht aktuell mit Docker und Visum Versa verwaltet werden. Stattdessen erstellen von Containern mit Docker finden Sie [Quick Start: Windows Server Container und Docker](./manage_docker.md). <br /><br /> Wollen Sie mehr wissen [Lesen Sie die FAQ] (.. / about/faq.md#WhydoIhavetopickbetweenDockerandPowerShellforWindowsServerContainermanagement).

## Voraussetzungen
Durchführung dieser exemplarischen müssen die folgenden Elemente vorhanden sein.

- Windows Server 2016 TP3 oder später mit der Container-Funktion in Windows Server konfiguriert. 
- Dieses System müssen an ein Netzwerk angeschlossen und auf das Internet zugreifen.

Benötigen Sie die Container-Funktion konfigurieren, finden Sie in den folgenden Handbüchern: [Container Setup in Azure] (./azure_setup.md) oder [Container Setup in Hyper-V] (./container_setup.md). 

## Grundlegende Behältermanagement mit PowerShell

In diesem erste Beispiel gehen durch die Grundlagen der erstellen und Entfernen von Windows-Server-Container und Windows-Server-Container-Bilder mit PowerShell.

Spaziergang durch Protokoll in Ihrem Host-System von Windows Server Container zunächst sehen Sie eine Windows-Eingabeaufforderung.

! [] (media/cmd.png)

Starten Sie eine PowerShell-Sitzung, durch Eingabe von "Powershell". Sie wissen, dass Sie in einer PowerShell-Sitzung sind, wenn die Eingabeaufforderung von wird ' C:\directory >', ' PS C:\directory >'.

```
C:\> powershell
Windows PowerShell
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\>
```

Verwenden Sie "Get-Command", um die verfügbaren Befehle im Container-Modul finden Sie unter

```
PS C:\> Get-Command -Module containers

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Function        Install-ContainerOSImage                           1.0.0.0    Containers
Function        Uninstall-ContainerOSImage                         1.0.0.0    Containers
Cmdlet          Add-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Connect-ContainerNetworkAdapter                    1.0.0.0    Containers
Cmdlet          Disconnect-ContainerNetworkAdapter                 1.0.0.0    Containers
Cmdlet          Export-ContainerImage                              1.0.0.0    Containers
Cmdlet          Get-Container                                      1.0.0.0    Containers
Cmdlet          Get-ContainerHost                                  1.0.0.0    Containers
Cmdlet          Get-ContainerImage                                 1.0.0.0    Containers
Cmdlet          Get-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Import-ContainerImage                              1.0.0.0    Containers
Cmdlet          Move-ContainerImageRepository                      1.0.0.0    Containers
Cmdlet          New-Container                                      1.0.0.0    Containers
Cmdlet          New-ContainerImage                                 1.0.0.0    Containers
Cmdlet          Remove-Container                                   1.0.0.0    Containers
Cmdlet          Remove-ContainerImage                              1.0.0.0    Containers
Cmdlet          Remove-ContainerNetworkAdapter                     1.0.0.0    Containers
Cmdlet          Set-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Start-Container                                    1.0.0.0    Containers
Cmdlet          Stop-Container                                     1.0.0.0    Containers
Cmdlet          Test-ContainerImage                                1.0.0.0    Containers
```


Anschließend stellen Sie sicher, dass Ihr System eine gültige IP-Adresse mit 'dem Befehl Ipconfig' hat und beachten Sie diese Adresse für die spätere Verwendung.

```
ipconfig

Ethernet adapter Ethernet 3:

   Connection-specific DNS Suffix  . :
   IPv6 Address. . . . . . . . . . . : 2601:600:8f01:84eb::e
   IPv6 Address. . . . . . . . . . . : 2601:600:8f01:84eb:a8c1:a3e:96b7:ffcb
   Link-local IPv6 Address . . . . . : fe80::a8c1:a3e:96b7:ffcb%5
   IPv4 Address. . . . . . . . . . . : 192.168.1.25
```

Wenn Sie von einer Azure-VM anstelle von 'Ipconfig' arbeiten musst du die öffentliche IP-Adresse der Azure Virtual Machine zu erhalten.

! [] (media/newazure9.png)

### Schritt 1 - erstellen Sie einen neuen Container

Bevor Sie einen Windows Server Container erstellen benötigen Sie den Namen eines Container-Bildes und den Namen eines virtuellen Switches, die in den neuen Container befestigt wird.

Verwenden Sie den Befehl "Get-ContainerImage", um eine Liste der Bilder, Container geladen auf dem Host zurückzugeben. 
``` PowerShell
Get-ContainerImage

Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
WindowsServerCore CN=Microsoft 10.0.10514.0 True
```

Verwenden Sie den Befehl "Get-VMSwitch", um eine Liste der verfügbaren Schalter auf dem Host zurückzugeben. 

``` PowerShell
Get-VMSwitch

Name           SwitchType NetAdapterInterfaceDescription
----           ---------- ------------------------------
Virtual Switch NAT
```

Führen Sie den folgenden Befehl zum Erstellen eines Containers. Beim Ausführen von "New-Container" Sie benennen, werden der Container das Container-Bild angeben, und wählen Sie Netzwerk-Switch, mit dem Container zu verwenden. Beachten Sie in diesem Beispiel, dass die Ausgabe in eine Variable $container befindet.  

``` PowerShell
$container = New-Container -Name "MyContainer" -ContainerImageName WindowsServerCore -SwitchName "Virtual Switch"
```

Finden eine Liste von Containern auf dem Host und überprüfen, ob der Container erstellt wurde, verwenden Sie den Befehl "Get-Container". 

``` PowerShell
Get-Container

Name        State Uptime   ParentImageName
----        ----- ------   ---------------
MyContainer Off   00:00:00 WindowsServerCore
```

Um den Container zu starten, verwenden Sie 'Start-Container' Proivding der Name des Containers.

``` PowerShell
Start-Container -Name "MyContainer"
```

Sie können mit Containern mithilfe von PowerShell-Remoting-Befehle wie "Invoke-Command" oder "Enter-PSSession" interagieren. Das folgende Beispiel erstellt eine remote PowerShell-Sitzung in den Container mit dem "Enter-PSSession"-Befehl. Dieser Befehl braucht die Container-Id, um die remote-Sitzung zu erstellen. Die Container-Id wurde in der '$container' Variablen gespeichert, wenn der Container erstellt wurde. 

Beachten Sie, dass sobald die remote-Sitzung erstellt wurde der Eingabeaufforderung ändern, um die ersten 11 Zeichen des Container-Id '[2446380e-629]' erweitert.

``` PowerShell
Enter-PSSession -ContainerId $container.ContainerId -RunAsAdministrator

[2446380e-629]: PS C:\Windows\system32>
```

Ein Container kann sehr viel wie eine physische oder virtuelle Maschine verwaltet werden. Befehl wie 'Ipconfig' die IP-Adresse des Containers, "Mkdir" zum Erstellen eines Verzeichnisses im Container und PowerShell-Befehle wie "Get-ChildItem" alle Arbeit zurück. Gehen Sie voran und nehmen Sie eine Änderung an dem Container wie das Erstellen einer Datei oder eines Ordners. 

``` PowerShell
ipconfig > c:\ipconfig.txt
```

Sie können lesen, den Inhalt der Datei Sicherstellung den Befehl wurde erfolgreich ausgeführt. 

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-E0D87408-325B-4818-ADB2-2EC7A2005739-0):

   Connection-specific DNS Suffix  . : corp.microsoft.com
   Link-local IPv6 Address . . . . . : fe80::400e:1e0e:591c:beef%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1
```

Nun, da der Container geändert wurde, Beenden der remote PowerShell-Sitzungs.

``` PowerShell
exit
```

Stoppen Sie den Container mit dem Containernamen auf den Befehl "Stop-Container". 

``` PowerShell
Stop-Container -Name "MyContainer"
```

### Schritt 2 - Erstellen Sie ein neues Container-Bild

Ein Bild kann nun von dieser Container gemacht werden. 

Erstellen Sie ein neues Bild mit dem Namen Befehl 'Newimage' den "New-ContainerImage". 

``` PowerShell
$newimage = New-ContainerImage -ContainerName MyContainer -Publisher Demo -Name newimage -Version 1.0
```

Verwenden Sie "Get-ContainerImage", um eine Liste der Bilder, Container zurückzugeben. 

``` PowerShell
Get-ContainerImage

Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
newimage          CN=Demo      1.0.0.0      False
WindowsServerCore CN=Microsoft 10.0.10254.0 True
```

### Schritt 3 - Erstellen Sie neuen Container aus Bild

Nun, da Sie eine kundenspezifische Containers-Bild erstellt haben, gehen Sie voran und Bereitstellen Sie einen neuen Container aus diesem Image.

Erstellen Sie einen Container mit dem Namen 'Newcontainer' aus dem Container-Bild mit dem Namen 'Newimage', Ausgabe das Ergebnis einer Variablen namens '$newcontainer'.

``` PowerShell
$newcontainer = New-Container -Name "newcontainer" -ContainerImageName newimage -SwitchName "Virtual Switch"
```

Starten Sie den neuen Container.
``` PowerShell
Start-Container $newcontainer
```

Erstellen Sie eine remote PowerShell-Sitzung mit dem Container.
``` PowerShell
Enter-PSSession -ContainerId $newcontainer.ContainerId -RunAsAdministrator
```

Beachten Sie schließlich, dass diese neue Container die weiter oben in dieser Übung erstellte ipconfig.txt-Datei enthält.

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-E0D87408-325B-4818-ADB2-2EC7A2005739-0):

   Connection-specific DNS Suffix  . : corp.microsoft.com
   Link-local IPv6 Address . . . . . : fe80::400e:1e0e:591c:beef%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1
```

 Sobald Sie fertig sind mit diesem Container arbeiten, die remote PowerShell-Sitzung zu beenden.

``` PowerShell
exit
```

Diese Übung hat gezeigt, dass ein Bild aus einem modifizierten Container alle Änderungen enthält. Während hier im Beispiel wird eine einfache Dateiänderung war, würde dasselbe gelten, wenn man Software in den Container, z. B. einen Webserver zu installieren. 

### Schritt 4 - Remove-Container und Container-Bilder

Alle laufenden Container, führen Sie folgenden Befehl stoppen. 

``` PowerShell
Get-Container | Stop-Container
```
Führen Sie folgendermaßen vor, um alle Container entfernen.

``` PowerShell
Get-Container | Remove-Container -Force
```
Führen Sie Folgendes aus, um die Container-Bild mit dem Namen 'Newimage' entfernen.

``` PowerShell
Get-ContainerImage -Name newimage | Remove-ContainerImage -Force
```

## Host ein Web-Server in einem Container

Das nächste Beispiel zeigen einen praktischeren Anwendungsfall für Windows-Server-Container. 

### Schritt 1-Container aus der Windows Server Core OS-Image erstellen

Um ein Web-Server-Container-Image zu erstellen, müssen Sie zuerst bereitstellen und einen Container aus dem Windows Server Core OS-Image zu starten.
``` PowerShell
$container = New-Container -Name webbase -ContainerImageName WindowsServerCore -SwitchName "Virtual Switch"
 ```

Starten Sie den Container.
``` PowerShell
Start-Container $container
```

Wenn der Container ist, erstellen Sie eine remote PowerShell-Sitzung mit dem Container.
``` PowerShell
Enter-PSSession -ContainerId $container.ContainerId -RunAsAdministrator
```

### Schritt 2 - Web-Server-Software installieren

Der nächste Schritt ist, die Webserver-Software zu installieren. In diesem Beispiel wird Nginx für Windows verwenden. Verwenden Sie die folgenden Befehle zum automatischen herunterladen und Extrahieren der Nginx-Software zum c:\nginx-1.9.3. ** Hinweis **, dass dieser Schritt erfordert die Container-Host mit dem Internet verbunden sein. 

Nginx-Software herunterladen.
``` PowerShell
wget -uri 'http://nginx.org/download/nginx-1.9.3.zip' -OutFile "c:\nginx-1.9.3.zip"
```

Extrahieren Sie die Nginx-Software.
``` PowerShell
Expand-Archive -Path C:\nginx-1.9.3.zip -DestinationPath c:\ -Force
```
Dies ist alles, die was der Nginx Installation abgeschlossen sein muss.

Die remote PowerShell-Sitzung zu beenden.
``` PowerShell
exit
```

Stoppen Sie den Container mithilfe des folgenden Befehls. 
``` PowerShell
Stop-Container $container
```
### Schritt 3 - Image vom Web Servercontainer erstellen

Mit dem Container geändert, um die Nginx Webserver-Software enthalten können Sie nun ein Bild von diesem Container erstellen. 
``` PowerShell
$webserverimage = New-ContainerImage -Container $container -Publisher Demo -Name nginxwindows -Version 1.0
```
Wenn abgeschlossen, der Befehl 'Get-ContainerImage' überprüfen, ob das Bild erstellt wurde.

``` PowerShell
Get-ContainerImage

Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
nginxwindows      CN=Demo      1.0.0.0      False
WindowsServerCore CN=Microsoft 10.0.10254.0 True
```

### Schritt 4 - Web-Server bereit Container bereitstellen

Um einen Windows-Server-Container auf das 'Nginxwindows' Bild basiert bereitzustellen, verwenden Sie den Befehl "New-Container" PowerShell.

``` PowerShell
$webservercontainer = New-Container -Name webserver1 -ContainerImageName nginxwindows -SwitchName "Virtual Switch"
```

Starten Sie den Container.
``` PowerShell
Start-Container $webservercontainer
```

Erstellen Sie eine remote PowerShell-Sitzung mit den neuen Container.
``` PowerShell
Enter-PSSession -ContainerId $webservercontainer.ContainerId -RunAsAdministrator
```

Sobald dem Container arbeitet, kann der Nginx-Webserver gestartet werden und Webinhalte inszeniert. 
``` PowerShell
cd c:\nginx-1.9.3\
```

Starten Sie den Webserver Nginx.
``` PowerShell
start nginx
```

Und diese PS-Sitzung zu beenden. 
``` PowerShell
exit
```

### Schritt 5 - Container-Netzwerk konfigurieren

Abhängig von der Konfiguration des Containers Host und Netzwerk erhalten ein Container entweder eine IP-Adresse von einem DHCP-Server oder den Container-Host selbst mit Netzwerkadressübersetzung (NAT). Geführte Wanderung durch ist NAT verwenden konfiguriert In dieser Konfiguration wird ein Port aus dem Container einen Port auf dem Container-Host zugeordnet. Die in den Container gehostete Anwendung erfolgt dann über die IP-Adresse / Name des Hosts, Container. Zum Beispiel wenn Port 80 aus dem Container Port 55534 auf dem Container-Host zugeordnet wurde, eine typische http-Anforderung an die Anwendung aussehen würde dieses Http://contianerhost:55534.  

Wir müssen diese Portzuordnung zu schaffen, für diese Übungseinheit. Dazu müssen wir wissen, die IP-Adresse der Container und interne (Anwendung) und externe (Container Host) Ports, die konfiguriert wird. In diesem Beispiel wollen wir halten es einfach und ordnen Port 80 aus dem Container an Port 80 des Hosts. Mit dem Befehl 'Add-NetNatStaticMapping' der ' – InternalIPAddress 'werden die IP-Adresse des Containers der für diese exemplarische Vorgehensweise ' 172.16.0.2 sein sollte'.

``` PowerShell
Add-NetNatStaticMapping -NatName "ContainerNat" -Protocol TCP -ExternalIPAddress 0.0.0.0 -InternalIPAddress 172.16.0.2 -InternalPort 80 -ExternalPort 80
```
Wenn die Portzuordnung erstellt wurde, müssen Sie auch eine eingehende Firewall-Regel für den konfigurierten Port konfigurieren. Dazu für Port 80, den folgenden Befehl ausführen.  

``` PowerShell
if (!(Get-NetFirewallRule | where {$_.Name -eq "TCP80"})) {
    New-NetFirewallRule -Name "TCP80" -DisplayName "HTTP on TCP/80" -Protocol tcp -LocalPort 80 -Action Allow -Enabled True
}
```

Als nächstes Wenn Sie von Azure arbeiten und nicht bereits einen virtuellen Computer-Endpunkt erstellt haben musst du jetzt erstellen. Weitere Informationen auf Azure VM Endpunkten finden Sie in diesem Artikel: [eingerichtet-Azure-VM-Endpunkte] (https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/).

### Schritt 6-Zugriff auf die Container gehostete Website
Mit dem Web-Server-Container erstellt können Sie nun die Anwendung gehostet im Container Kasse. Hierzu öffnen Sie einen Browser auf anderen Computer, und geben Sie 'http://containerhost-ipaddress'. Hier ist zu bemerken, dass Sie zu der IP-Adresse des Hosts Container und nicht der Container selbst Surfen im.  

Wenn alles richtig konfiguriert wurde, sehen Sie die Seite "Willkommen" Nginx.

! [] (media/nginx.png)

An dieser Stelle, zögern Sie nicht, die Website zu aktualisieren. In Ihre eigene Beispiel-Website kopieren Sie, oder verwenden Sie eine einfache "Hello World"-Beispiel-Website erstellt wurde, für diese Demo. 

Sie müssen zunächst die Remotesitzung PS mit dem Container neu zu erstellen.
``` PowerShell
Enter-PSSession -ContainerId $webservercontainer.ContainerId -RunAsAdministrator
```
Führen Sie dann den folgenden Befehl zum download und ersetzen die Datei "index.html".

``` powershell
wget -uri 'https://raw.githubusercontent.com/Microsoft/Virtualization-Documentation/master/doc-site/virtualization/windowscontainers/quick_start/SampleFiles/index.html' -OutFile "C:\nginx-1.9.3\html\index.html"
```
   
Nachdem die Website aktualisiert wurde, wechseln Sie zurück zu 'http://containerhost-ipaddress'.

! [] (media/hello.png)

## Video-Anleitung

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Deploying-and-Managing-Windows-Server-Containers-with-PowerShell/player" width="800" height="450"  allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>


## Die nächsten Schritte
Nun, da Sie Container eingerichtet und eine Einführung in die Werkzeuge haben, gehen Sie Ihrer eigenen Containerbetrieb Anwendungen zu bauen.

Hier ist eine vollständigere [PowerShell Reference] (.. / reference/powershell_overview.md).

Denken Sie daran, dies ist ein ** Vorschau ** es gibt Fehler und wir haben eine Menge Arbeit.  [Diese Seite] (.. / about/work_in_progress.md) enthält viele unserer bekannten Fragen.

Wir sind auch die [Foren] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers) sehr aufmerksam.

Es gibt auch vorgefertigte Proben auf [GitHub] (https://github.com/Microsoft/Virtualization-Documentation/tree/master/windows-server-container-samples).

-----------------------------------
[Zurück zur Container-Startseite] (.. / containers_welcome.md) [bekannte Probleme bei der aktuellen Version] (.. / about/work_in_progress.md)
