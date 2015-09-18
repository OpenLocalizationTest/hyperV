ms. ContentId: F0D47E70-0BA1-4A06-B2F3-0232C496709D
Titel: häufig gestellte Fragen

# Häufig gestellte Fragen
Datenstand: 1. Mai 2015

## Was ist ein Windows-Server-Container?

Windows Server-Container sind eine leichte Betriebssystem-Virtualisierung-Methode verwendet, um Anwendungen oder Dienste von anderen Diensten, die auf dem gleichen Container Host zu trennen.   

## Was ist der Unterschied zwischen Linux und Windows-Server-Container?

Linux und Windows-Server-Container sind ähnlich--beide implementieren ähnliche Technologien innerhalb ihrer Betriebssystem-Kernel und Kern. Der Unterschied kommt von der Plattform und Arbeitslasten, die innerhalb der Behälter ausgeführt.  
Wenn ein Kunde Windows Server Container verwendet, können sie mit vorhandenen Windows-Technologien wie .NET, ASP.NET und PowerShell integrieren.

## Was ist ein Hyper-V-Container?

Sie können als Windows Server Container innerhalb einer Hyper-V-Partition Ausführen eines Hyper-V-Containers vorstellen.

Hyper-V-Container bieten eine zusätzliche Bereitstellungsoption zwischen den Servercontainer hocheffiziente, High-Density-Windows und Hardware virtualisiert hoch isolierten Hyper-V Virtual Machine. Für Umgebungen, in denen Anwendungen aus verschiedenen Grenzen auf dem gleichen Host Vertrauen, sein zusätzliche Isolierung erforderlich. Hyper-V-Behälter bieten höhere Isolation mit einer optimierten Virtualisierung und Windows Server-Betriebssystems, die Container aus dem Host-Betriebssystem voneinander trennt. 


## Wann werden Hyper-V-Containern zur Verfügung?

Wir erwarten eine Vorschau von Hyper-V-Containern in diesem Kalenderjahr liefern.


## Werden Hyper-V-Containern auch Docker-Ökosystem?

Hyper-V-Container wird ja – das gleiche Maß an Integration und Management mit Docker als Windows-Server-Container stellen.  Das Ziel ist es, eine offene, einheitliche, Cross-Plattform-Erfahrung haben.  
Die Docker-Plattform wird auch erheblich vereinfachen und verbessern die Erfahrung des Arbeitens über unsere Container-Optionen. 

## Warum muss ich wählen zwischen Docker und PowerShell für Windows Server Container Management?

** Dies ist nicht gewünschte Verhalten noch unsere langfristige plan.* * PowerShell Containers-Verwaltungstools und Docker Container Management-Tools funktionieren nebeneinander in der Zukunft.

Nachdem dies gesagt wurde kann es schwierig sein, den gleichen Container verwalten mithilfe mehrerer Schnittstellen.

Nehmen Sie wir z. B. Erstellen eines Containers mit PowerShell und benennen das Bild mit einem Großbuchstaben.  Hafenarbeiter unterstützt keine Kappen, PowerShell tut.  
Während dieses spezifische Beispiel sehr überschaubar ist, welche bekommt viel härter sind Übergabe Zustandsänderungen (Racebedingungen und unterschiedliche Erwartungen), Feature set Unterschiede oder Versionen...

Unsere kurzfristige Entscheidung war, dass (in diesem Fall Docker und PowerShell) Verwaltungsschnittstellen, nur siehe Container, die sie geschaffen – Sie einen Container mit Docker erstellen und PowerShell nicht sehen, Sie es mit PowerShell erstellen und Docker sehen es nicht.


## Als Entwickler muss ich meine app für jede Art von Container neu zu schreiben?

Nein, sind Container-Windows-Abbilder über Windows-Server-Container und Hyper-V-Containern. Die Auswahl der Containertyp erfolgt beim Starten des Containers. Aus Sicht der Entwickler stehen Windows Server Container und Hyper-V-Container zwei Arten von der gleichen Sache. 

Ein Entwickler kann ein Container-Bild mit einem Windows-Server-Container erstellen und bereitstellen als Hyper-V-Container oder umgekehrt ohne Änderungen als das entsprechende Runtime-Flag angeben.

Windows Server-Container werden höhere Dichte und Leistung (z.B. anbieten geringere Drehbeschleunigung oben Zeit, schneller Laufzeit-Performance im Vergleich zu geschachtelten Konfigurationen) Wenn die Geschwindigkeit Schlüssel befindet. Hyper-V-Behälter bieten größere Isolation, um sicherzustellen, dass Code in einem Container ausgeführt nicht gefährden oder beeinträchtigen das Host-Betriebssystem oder anderen Behältern auf dem gleichen Host ausgeführt. 


## Sind Hyper-V/Windows-Server-Container ein Add-on, oder, dass sie in Windows-Server integriert werden?

Die Container-Funktionen werden in Windows Server 2016 integriert werden.   


## Was sind die Voraussetzungen für Windows Server-Container und Hyper-V-Container?

Fenster Server Container und Hyper-V-Behälter erfordern Windows Server 2016. 

## Werden Nano-Server basierten Container werden unterstützt?

Für die Veröffentlichung von TP3 sind Nein sie nicht. 

## Kann ich Windows Server Container auf ESXi oder einem anderen nicht Hyper-V Hypervisor ausführen?
Ja, Windows-Server-Container auf jeder TP3 Server Core-Installation ausführen.  Folgen Sie den Anweisungen zum [in-Place-Container-Feature aktivieren] (.. / quick_start/inplace_setup.md).

 
## Ist Microsoft in den offenen Container Initiative (OCI) teilnehmen?
Um zu gewährleisten, dass das Packaging-Format bleibt universal, organisierte Docker vor kurzem die öffnen Container Initiative (OCI), mit dem Ziel, sicherzustellen, dass Container Verpackung bleibt ein offenes und Stiftung geführten Format mit Microsoft als eines der Gründungsmitglieder.

## Ist Microsoft wirklich Partnerschaft mit Docker?
Ja.  
Unsere Partnerschaft mit Docker ermöglicht Entwicklern das Erstellen, verwalten und Bereitstellen von Windows Server und Linux Container mit denselben Docker Tool.   

Docker ist zweierlei, der open-Source Projekte und Docker das Unternehmen. Wir betrachten diese Partnerschaft, beide einzuschließen. Docker ist erfolgreich, teilweise wegen der lebendigen Ökosystem, das rund um die Docker-Container-Technologie aufgebaut.   

Weitere Informationen finden Sie unter [neue Windows Server-Container und Azure Unterstützung für Docker] (http://azure.microsoft.com/blog/2014/10/15/new-windows-server-containers-and-azure-support-for-docker/?WT.mc_id=Blog_ServerCloud_Announce_TTD) Blog-Post.

-------------------
[Zurück zur Container-Startseite] (.. / containers_welcome.md)