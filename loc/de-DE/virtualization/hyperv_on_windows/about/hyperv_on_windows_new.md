# Einführung in Hyper-V unter Windows 10

Ob Sie ein Softwareentwickler, eine ITPro oder ein Techenthusiast sind, müssen viele von Ihnen mehrere Betriebssysteme, gelegentlich auf vielen verschiedenen Computern ausführen.  

Dies ist ein neuer Satz.

hehehe

Hier ist ein Diagramm:

! [Bild] (media/ProductionCheckpoints_new.png)

## Verwendungsmöglichkeiten für Virtualisierung
Virtualisierung ermöglicht es jedem leicht mehrere Testumgebungen bestehend aus viele Betriebssysteme, Software-Konfigurationen und Hardwarekonfigurationen zu pflegen.     

Hyper-V kann in vielerlei Hinsicht zum Beispiel verwendet werden:
- Eine Testumgebung, bestehend aus mehreren virtuellen Maschinen kann auf einem einzigen Desktop oder Laptop-Computer erstellt werden. 

- Hyper-V können auf ihrem Computer Entwickler die Software auf mehreren Betriebssystemen testen. 

- Hyper-V können Sie um virtuelle Maschinen aus einer Hyper-V-Bereitstellung zu beheben.  

- Virtuellen Netzwerke verwenden, erstellen Sie eine Multi-machine Umgebung für Test, Entwicklung, Demonstration, die Auswirkungen auf das Produktionsnetzwerk sicher ist.

- Enthusiasten können sie experimentieren mit anderen Betriebssystemen. 

- Hyper-V können auf einem Laptop Sie für den Nachweis von älterer Versionen von Windows oder nicht-Windows-Betriebssystemen. 


## System-Anforderungen

Hyper-V erfordert ein 64-Bit-System, Second Level Address Translation (Stab) verfügt. SLAT ist ein Feature in der aktuellen Generation von 64-Bit-Prozessoren von Intel & AMD vorhanden. Sie benötigen auch eine 64-Bit-Version von Windows 8 oder höher und mindestens 4 GB RAM. 

Hyper-V dynamische Speicher ermöglicht Speicher benötigt von der VM zugewiesen und de dynamisch zugeteilt werden (Angabe eines Minimum und Maximum) und ungenutzten Speicher zwischen VMs zu teilen. 3 oder 4 VMs können auf eine Maschine mit 4 GB RAM ausgeführt, aber Sie benötigen mehr RAM für 5 oder mehr VMs. 

## Betriebssysteme, die in einer virtuellen Maschine ausgeführt werden können ##

Der Begriff "Gast" bezieht sich auf eine virtuelle Maschine und "Host" bezieht sich auf den Computer mit der virtuellen Maschine. Hyper-V unter Windows unterstützt viele verschiedene Gast-Betriebssysteme, einschließlich der verschiedenen Versionen von Linux, FreeBSD und Windows. Informationen darüber, welche Betriebssysteme als Gäste in Hyper-V unter Windows unterstützt werden, finden Sie unter [unterstützt Windows Guest Operating Systems](supported_guest_os.md) und [Linux und FreeBSD virtuellen Maschinen auf Hyper-V] (https://technet.microsoft.com/library/dn531030.aspx). 


## Unterschiede zwischen Hyper-V auf Windows und Hyper-V unter Windows Server
Es gibt einige Funktionen, die anders in Hyper-V unter Windows funktionieren als Hyper-V unter Windows Server ausgeführt. 

- Das Speicher-Management-Modell unterscheidet sich für Hyper-V unter Windows. Hyper-V-Speicher erfolgt auf einem Server mit der Annahme, die ausschließlich der virtuellen Maschinen auf dem Server ausgeführt werden. In Hyper-V unter Windows ist Speicher verwaltet, mit der Maßgabe, dass die meisten Client-Rechner laufende Software zusätzlich zu laufenden virtuellen Maschinen sind. 

- SR-IOV auf einem 64-Bit-Gast funktioniert normal, aber 32-Bit nicht und wird nicht unterstützt.


### Windows Server-Features nicht Avilable in Windows Hyper-V
Es gibt einige Features, die in Hyper-V auf Server enthalten, die in Hyper-V unter Windows nicht enthalten sind. 

- Die Remote FX-Fähigkeit, GPUs zu virtualisieren 

- Live-Migration virtueller Maschinen von einem Host zu einem anderen

- Hyper-V Replica

- Virtuelle Fibre-Channel

- SR-IOV-Vernetzung

- Gemeinsam genutzt. VHDX


> ** Achtung **: virtuelle Maschinen auf Hyper-V ausgeführt wird können nicht automatisch verarbeiten Verschieben von einem drahtgebundenen auf eine drahtlose Verbindung. 

## Einschränkungen
Mit Virtualisierung Einschränkungen haben. Funktionen oder Anwendungen, die bestimmte Hardware abhängen funktioniert nicht gut in einer VM. Z. B. Spiele oder Programme, die Verarbeitung mit GPUs benötigen (ohne Softwarefallbacks) funktioniert möglicherweise nicht gut. Auch Anwendungen, die unter Berufung auf Sub 10ms Timer, wie Latenz-Sensitive hochpräzise Anwendungen wie live-Musik mischen, apps, etc.. Fragen, die in einer virtuellen Maschine ausgeführt hätte. Die Wurzel OS läuft auch auf dem Hyper-V Virtualisierungsschicht, aber es ist spezielle, auf die sie direkten Zugriff auf die Hardware. 

Zur Erinnerung musst du eine gültige Lizenz für alle Betriebssysteme können in den VMs-Test verwendeten.

## Nächster Schritt: 
[Exemplarische Vorgehensweise Hyper-V auf Windows 10] (.. \quick_start\walkthrough.MD) 

Check out [What's New](whats_new.md) in Hyper-V auf Windows 10.

