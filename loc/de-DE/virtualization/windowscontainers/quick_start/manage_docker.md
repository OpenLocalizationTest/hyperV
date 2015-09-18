ms. ContentId: 347fa279-d588-4094-90ec-8c2fc241f5b6
Titel: Verwalten des Windows-Server-Container mit Docker

#Quick Start: Windows Server Container und Docker

In diesem Artikel gehen durch die Grundlagen der Verwaltung von Windows Server-Container mit Docker. Angesprochenen Themen umfassen Windows Server Container und Windows-Server-Container-Abbilder erstellen, Entfernen von Windows-Server-Container und Container-Bilder und schließlich Bereitstellen einer Anwendung in einem Windows-Server-Container. 

Haben Sie Fragen? Fragen sie im [Windows Containern Forum] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).

> ** Hinweis: ** mit PowerShell erstellt Windows-Container kann nicht aktuell mit Docker und Visum Versa verwaltet werden. Erstellen von Containern mit PowerShell finden Sie [Quick Start: Windows Server Container und PowerShell](./manage_powershell.md). <br /><br /> Wollen Sie mehr wissen [Lesen Sie die FAQ] (.. / about/faq.md#WhydoIhavetopickbetweenDockerandPowerShellforWindowsServerContainermanagement).

## Voraussetzungen
Durchführung dieser exemplarischen müssen die folgenden Elemente vorhanden sein.

- Windows Server 2016 TP3 oder später mit der Container-Funktion von Windows Server konfiguriert. 
- Dieses System müssen an ein Netzwerk angeschlossen und auf das Internet zugreifen.

Benötigen Sie die Container-Funktion konfigurieren, finden Sie in den folgenden Handbüchern: [Container Setup in Azure] (./azure_setup.md) oder [Container Setup in Hyper-V] (./container_setup.md). 

## Grundlegende Behältermanagement mit Docker

In diesem erste Beispiel werden die Grundlagen der erstellen und Entfernen von Windows-Server-Container und Windows-Server-Container-Bilder mit Docker spazieren.

Spaziergang durch Protokoll in Ihrem Host-System von Windows Server Container zunächst sehen Sie eine Windows-Eingabeaufforderung.

! [] (media/cmd.png)

Starten Sie eine PowerShell-Sitzung, durch Eingabe von "Powershell". Sie wissen, dass Sie in einer PowerShell-Sitzung sind, wenn die Eingabeaufforderung von wird ' C:\directory >', ' PS C:\directory >'.
```
C:\> powershell
Windows PowerShell
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\>
```
> Dieser Schnellstart wird auf Docker Befehle konzentriert, aber einige Schritte wie Verwaltung von Firewall-Regeln und das Kopieren von Dateien mit PowerShell-Befehle ausgeführt werden. 

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

Bevor Sie einen Windows-Server-Container mit Docker erstellen, benötigen Sie den Namen oder die ID des Bildes Windows Server Container Exsisitng.

Bis alle Bilder geladen auf dem Container-Host mithilfe des Befehls "Hafenarbeiter Bilder" zu sehen.

``` PowerShell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
windowsservercore   latest              9eca9231f4d4        30 hours ago        9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        30 hours ago        9.613 GB
```

Verwenden Sie nun 'Hafenarbeiter ausführen' einen neuen Windows Server Container erstellen. 

``` PowerShell
docker run -it --name dockerdemo windowsservercore cmd
```
Wenn der Befehl abgeschlossen ist werden Sie in einer Konsolensitzung auf dem Container arbeiten.

Arbeiten in einem Container ist nahezu identisch mit der Arbeit mit Windows auf einer virtuellen oder physischen Maschine installiert. Sie können Befehle wie 'Ipconfig' wieder die IP-Adresse des Containers, "Mkdir" erstellen Sie ein neues Verzeichnis oder "Powershell" zum Starten einer PowerShell-Sitzung ausführen. Gehen Sie voran und nehmen Sie eine Änderung an dem Container wie das Erstellen einer Datei oder eines Ordners. 

``` PowerShell
ipconfig > c:\ipconfig.txt
```

Sie können lesen, den Inhalt der Datei Sicherstellung den Befehl wurde erfolgreich ausgeführt. 

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-94a3e12ad262b3059e08edc4d48fca3c8390e38c3b219023d4a0a4951883e658-0):

   Connection-specific DNS Suffix  . : 
   Link-local IPv6 Address . . . . . : fe80::cc1f:742:4126:9530%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1
```

Nun, da der Container geändert wurde, führen Sie folgendermaßen vor, um die Konsole Sitzung setzen Sie Sie wieder in der Konsolensitzung des Container-Hosts zu stoppen.

``` PowerShell
exit
```

Schließlich um zu sehen, eine Liste von Containern für den Container Host Befehl 'Hafenarbeiter Ps – a'. 

``` PowerShell
docker ps -a

CONTAINER ID        IMAGE               COMMAND        CREATED             STATUS                     PORTS     NAMES
4f496dbb8048        windowsservercore   "cmd"          2 minutes ago       Exited (0) 2 minutes ago             dockerdemo
``` 

### Schritt 2 - Erstellen Sie ein neues Container-Bild

Ein Bild kann nun von dieser Container gemacht werden. 

Erstellen Sie ein neues Bild, führen Sie den folgenden. 

``` PowerShell
docker commit dockerdemo newcontainerimage
```

Um alle Bilder auf dem Host anzuzeigen, führen Sie 'Hafenarbeiter Bilder'. 

``` PowerShell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
newcontainerimage   latest              4f8ebcf0a334        2 minutes ago       9.613 GB
windowsservercore   latest              9eca9231f4d4        30 hours ago        9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        30 hours ago        9.613 GB
```

### Schritt 3 - Erstellen Sie neuen Container aus Bild

Nun, da Sie eine benutzerdefinierte Container-Bild haben, stellen Sie einen neuen Container mit dem Namen 'Newcontainer' aus 'Newcontainerimage' und öffnen Sie eine interaktive Shell-Sitzung mit dem Container.

``` PowerShell
docker run –it --name newcontainer newcontainerimage cmd
```

Schauen Sie sich das Laufwerk c:\ dieses neuen Containers und beachten Sie, dass die ipconfig.txt-Datei vorhanden ist.

Beenden Sie den neu erstellten Container mit der Konsolensitzung des Container-Gastgeber zurückgegeben.

``` PowerShell
exit
```

Diese Übung hat gezeigt, dass ein Bild aus einem modifizierten Container alle Änderungen enthält. Während hier im Beispiel wird eine einfache Dateiänderung war, würde dasselbe gelten, wenn man Software in den Container, z. B. einen Webserver zu installieren. 

### Schritt 4 - Container entfernen und Bilder

Um einen Container zu entfernen, nachdem es nicht mehr ist nötig den 'Hafenarbeiter Rm'-Befehl verwenden. 

``` PowerShell
docker rm newcontainer
```
Um Container-Bilder zu entfernen, wenn sie nicht mehr benötigte mithilfe des Befehls 'Hafenarbeiter Rmi'. 

Der folgende Befehl entfernt das Container-Bild mit dem Namen 'Newcontainerimage'.
``` PowerShell
docker rmi newcontainerimage

Untagged: newcontainerimage:latest
Deleted: 4f8ebcf0a334601e75070a92294d993b0f182abb6f4c88740c75b05093e6acff
```

## Host ein Web-Server in einem Container

Das nächste Beispiel zeigen einen praktischeren Anwendungsfall für Windows-Server-Container. 

### Schritt 1 - Download-Web-Server-Software

Vor dem Erstellen eines Container-Bild im Web benötigen Serversoftware heruntergeladen und auf dem Container-Host inszeniert werden. Wir werden die Nginx für Windows-Software für dieses Beispiel verwenden. ** Hinweis **, dass dieser Schritt erfordert die Container-Host mit dem Internet verbunden sein. 

Führen Sie den folgenden Befehl auf dem Container-Host die Verzeichnisstruktur zu erstellen, die in diesem Beispiel verwendet wird.

``` PowerShell
mkdir c:\build\nginx\source
```

Führen Sie diesen Befehl auf dem Container-Host herunterladen die Nginx-Software zu 'c:\nginx-1.9.3.zip'.

``` PowerShell
wget -uri 'http://nginx.org/download/nginx-1.9.3.zip' -OutFile "c:\nginx-1.9.3.zip"
```

Schließlich wird der folgende Befehl die Nginx-Software zum 'C:\build\nginx\source' entpacken. 

``` PowerShell
Expand-Archive -Path C:\nginx-1.9.3.zip -DestinationPath C:\build\nginx\source -Force
```

### Schritt 2 - Erstellen von Web-Server-Image
Im vorherigen Beispiel Sie manuell erstellt, aktualisiert und ein Container-Bild erfasst. In diesem Beispiel wird eine automatisierte Methode zum Erstellen von Container-Bilder mit einer Dockerfile demonstrieren. Dockerfiles enthalten Anweisungen, die Docker-Engine verwendet, zum Erstellen und Ändern eines Containers, und begehen dann den Container Container-Bild. 
Weitere Informationen zu Dockerfiles siehe [Dockerfile Reference] (https://docs.docker.com/reference/builder/).

Verwenden Sie den folgenden Befehl zum Erstellen einer leeren Dockerfile.

``` PowerShell
new-item -Type File c:\build\nginx\dockerfile
```
Öffnen Sie die Dockerfile mit dem Notepad.

```
notepad.exe c:\build\nginx\dockerfile
```

Kopieren Sie und fügen Sie den folgenden Text in den Editor, speichern Sie die Datei und schließen Editor.

``` PowerShell
FROM windowsservercore
LABEL Description="nginx For Windows" Vendor="nginx" Version="1.9.3"
ADD source /nginx
```

An dieser Stelle werden die Dockerfile in 'c:\build\nginx' und in 'c:\build\nginx\source' extrahiert Nginx-Software. 
Sie sind jetzt bereit für die Erstellung des Web Server-Container-Image auf der Grundlage der Anweisungen in der Dockerfile. 

``` PowerShell
docker build -t nginx_windows C:\build\nginx
```
Dieser Befehl weist den Hafenarbeiter-Motor die Dockerfile am 'C:\build\nginx' verwenden, um ein Bild mit dem Namen 'Nginx_windows' zu erstellen.

Die Ausgabe wird so aussehen:

! [] (media/docker1.png)

Wenn abgeschlossen, schauen Sie sich die Bilder auf dem Host mit dem Befehl 'Hafenarbeiter Bilder'. Es erscheint ein neues Bild mit dem Namen 'Nginx_windows'.
``` PowerShell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE

nginx_windows       latest              d792268338d0        5 seconds ago       9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        35 hours ago        9.613 GB
windowsservercore   latest              9eca9231f4d4        35 hours ago        9.613 GB
```

### 3. Schritt – Netzwerk für Container-Anwendung konfigurieren
Weil Sie eine Website innerhalb eines Containers hosten soll bezogene ein paar Vernetzung Konfigurationen vorgenommen werden müssen. Zuerst muss eine Firewallregel auf dem Container-Host erstellt werden, die Zugang zu der Website ermöglichen. In diesem Beispiel werden wir die Website über Port 80 zugreifen. Führen Sie das folgende Skript, um diese Firewallregel erstellen.  

``` powershell
if (!(Get-NetFirewallRule | where {$_.Name -eq "TCP80"})) {
    New-NetFirewallRule -Name "TCP80" -DisplayName "HTTP on TCP/80" -Protocol tcp -LocalPort 80 -Action Allow -Enabled True
}
```

Als nächstes Wenn Sie von Azure arbeiten und nicht bereits einen virtuellen Computer-Endpunkt erstellt haben musst du jetzt erstellen. Weitere Informationen auf Azure VM Endpunkten finden Sie in diesem Artikel: [eingerichtet-Azure-VM-Endpunkte] (https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/).

### Schritt 4 - Web-Server bereit Container bereitstellen

Stellen Sie einen Windows Server-Container auf führen Sie den folgenden Befehl 'Nginx_windows'-Container basiert. Dies erstellt einen neuen Container mit dem Namen 'Nginxcontainer' und starten eine Konsolensitzung auf dem Container.  

``` powershell
docker run -it --name nginxcontainer -p 80:80 nginx_windows cmd
```
Sobald dem Container arbeitet, kann der Nginx-Webserver gestartet werden und Webinhalte inszeniert. 

``` powershell
cd c:\nginx\nginx-1.9.3
```

Starten Sie den Webserver Nginx.
``` powershell
start nginx
```
### Schritt 5-Zugriff auf die Container gehostete Website

Mit dem Web-Server-Container erstellt können Sie nun die Anwendung gehostet im Container Kasse. Hierzu öffnen Sie einen Browser auf anderen Computer, und geben Sie 'http://containerhost-ipaddress'. Hier ist zu bemerken, dass Sie zu der IP-Adresse des Hosts Container und nicht der Container selbst Surfen im.  

Wenn alles richtig konfiguriert wurde, sehen Sie die Seite "Willkommen" Nginx.

! [] (media/nginx.png)

An dieser Stelle, zögern Sie nicht, die Website zu aktualisieren. 

```powershell
powershell wget -uri 'https://raw.githubusercontent.com/Microsoft/Virtualization-Documentation/master/doc-site/virtualization/windowscontainers/quick_start/SampleFiles/index.html' -OutFile "C:\nginx\nginx-1.9.3\html\index.html"
```

Nachdem die Website aktualisiert wurde, wechseln Sie zurück zu 'http://containerhost-ipaddress'.

! [] (media/hello.png)

> ** Hinweis: ** Wenn Sie wollen, ändern Sie die Docker Daemon-Einstellungen (z.B. sein, daß den Port zu ändern, es hört auf, zu einem Container eine Remoteverbindung herstellen), musst du die Datei "C:\ProgramData\docker\runDockerDaemon.cmd" in den Container zu bearbeiten und dann müssen Sie zum Neustarten des Dienstes mit PowerShell, ''' Neustartdienst Hafenarbeiter '''.

## Video-Anleitung

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Deploying-and-Managing-Windows-Server-Containers-with-Docker/player" width="800" height="450"  allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>

## Die nächsten Schritte
Nun, da Sie Container eingerichtet und eine Einführung in die Werkzeuge haben, gehen Sie Ihrer eigenen Containerbetrieb Anwendungen zu bauen.

Denken Sie daran, dies ist ein ** Vorschau ** es gibt Fehler und wir haben eine Menge Arbeit.  [Diese Seite] (.. / about/work_in_progress.md) enthält viele unserer bekannten Fragen.

Beachten Sie, dass es gibt einige bekannte Docker-Befehle, die [funktioniert nicht] (.. / about/work_in_progress.md#DockermanagementDockercommandsthatdontworkwithWindowsServerContainers) und einige, dass nur [teilweise Arbeit] (.. / about/work_in_progress.md#DockermanagementDockercommandsthatpartiallyworkwithWindowsServerContainers)

Wir sind auch die [Foren] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers) sehr aufmerksam.

Es gibt auch vorgefertigte Proben auf [GitHub] (https://github.com/Microsoft/Virtualization-Documentation/tree/master/windows-server-container-samples).

-----------------------------------
[Zurück zur Container-Startseite] (.. / containers_welcome.md) [bekannte Probleme bei der aktuellen Version] (.. / about/work_in_progress.md)