ms. ContentId: 526e4f1a-2936-4c61-b3be-d41b4cf9d10f
Titel: über Windows-Server-Container

#Windows Server-Container

Anwendungen Kraftstoffpumpe Innovation in der Wolke und das mobile Zeitalter. 

Sehen Sie eine kurze Übersicht: [Windows-basierten Container: moderne app Entwicklung mit Enterprise-Klasse Control] (https://youtu.be/Ryx3o0rD5lY).

Sind ##What Container?

Sie sind eine isolierte, Ressource kontrollierte und portable Betriebsumgebung.

Grundsätzlich ist ein Container ein isolierten Ort, wo eine Anwendung ohne Auswirkungen auf den Rest des Systems und ohne das System auf die Anwendung ausführen können. 

Wenn Sie innerhalb eines Containers wäre, würde es aussehen wie Sie in einem frisch installierten physischen Computer oder einer virtuellen Maschine waren sehr. Und zu [Docker] (https://www.docker.com/), ein Windows-Server-Container auf die gleiche Weise wie jede andere Container verwaltet werden können.

## Container-Grundlagen

Wenn Sie mit Containern arbeiten anfangen beachten Sie viele Ähnlichkeiten zwischen einem Container und einer virtuellen Maschine. Ein Container wird ein Betriebssystem ausgeführt, hat ein Dateisystem und kann über ein Netzwerk zugegriffen werden, so als ob es ein physikalisches oder virtuelles Computersystem war. Das heißt, die Technologie und die Konzepte hinter dem Container sind sehr verschieden von der virtuellen Maschinen.  
[Dieser Blog-Post] (http://azure.microsoft.com/blog/2015/08/17/containers-docker-windows-and-trends/) von Mark Russinovich erklärt Behälter gut.

Die folgende Schlüsselkonzepte werden hilfreich sein, wenn Sie erstellen beginnen und arbeiten mit Windows-Server-Container. 

** Container Host: ** physischen oder virtuellen Computer-System mit der Windows Server-Container-Funktion konfiguriert. 

** Container Bild: ** wie Änderungen auf eine Container-Datei-System oder die Registrierung, gemacht werden, wie z. B. mit Softwareinstallation sie im Sandkasten erfasst werden.  In vielen Fällen, die möglicherweise möchten Sie diesen Zustand zu erfassen, so dass neue Container erstellt werden können, erben, die diese Änderungen. Das ist, was ist ein Bild-sobald der Container hat Sie gestoppt können entweder verwerfen, dass Sandbox oder können Sie es in ein neues Container-Bild umwandeln. Zum Beispiel stellen wir uns, dass Sie einen Container aus dem Windows Server Core OS-Image bereitgestellt haben. Dann installieren Sie MySQL in diesem Container. Erstellen ein neues Bild aus diesem Container würden als einsetzbare Version des Containers fungieren. 

** Sandbox: ** Container gestartet wurden, schreiben alle Aktionen wie Datei-Modifikationen, Registrierungsänderungen oder Software-Installationen zu dieser 'Sandkasten'-Ebene erfasst werden.  
 
** Container OS Image: ** Container werden aus Bildern bereitgestellt. Das Container-OS-Bild ist die erste Schicht in potenziell vielen Bildebenen, die einen Container bilden. Dieses Bild stellt die Betriebssystem-Umgebung. 

** Container Repository: ** jedes Mal ein Container-Bild erzeugt das Container-Bild und seine Abhängigkeiten sind in einem lokalen Repository gespeichert. Diese Bilder können auf dem Container-Host viele Male wiederverwendet werden. 

** Container-Management-Technologie: ** Windows Server Container kann mithilfe von PowerShell und Docker verwaltet werden. 

<center>! [] (media/containerfund.png)</center>

## Behälter für Entwickler

Von einem Entwickler Desktop zu einer Prüfmaschine auf einen Satz von Produktionsmaschinen, ein Docker Image erstellt werden kann, die identisch in jeder Umgebung in Sekunden bereitstellen.   

Wenn Sie eine app Terminal, werden nur die app und die Komponenten erforderlich, um die app in ein "Bild" zusammengefasst. Container werden dann aus diesem Image erstellt, wie Sie sie benötigen. Sie können auch ein Bild als Basis verwenden, um ein anderes Bild zu erstellen, Image-Erstellung noch schneller machen.  Mehrere Container können dasselbe Bild, teilen, d.h. Behälter sehr schnell starten und weniger Ressourcen zu verwenden. 

Da der Container alles es braucht hat, um die Anwendung auszuführen, sind Sie sehr portabel und läuft auf jedem Rechner, auf dem Windows Server 2016 ausgeführt wird. Sie können erstellen und Container lokal zu testen und dann bereitstellen dieses gleichen Container-Images auf Ihr Unternehmen private Wolke, öffentliche Cloud oder Dienstleister. 

Mit Containern können Entwickler eine Anwendung in einer beliebigen Sprache erstellen.   

Container hilft Entwicklern zum Erstellen und versenden höherwertigen Anwendungen schneller.

## Behälter für IT-Professionals ##

Container können IT-Experten bieten standardisierte Umgebungen für ihre Entwicklung, QS und Produktion-Teams. Sie müssen nicht mehr über komplizierte Installations- und Konfigurationsschritte sorgen. 

Container helfen Admins eine Infrastruktur zu schaffen, die ist einfacher zu aktualisieren und zu pflegen.

## Video-Überblick

<iframe 
src="https://channel9.msdn.com/Blogs/containers/Containers-101-with-Microsoft-and-Docker/player" width="960" height="540" allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>


##Try-Windows-Server-Container

[Erste Schritte mit Windows Server-Container in Windows Azure] (.. / quick_start/azure_setup.md) [erste Schritte mit Windows Server Container lokal] (.. / quick_start/container_setup.md)

-------------------
[Zurück zur Container-Startseite] (.. / containers_welcome.md)
