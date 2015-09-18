# Was ist neu in Hyper-V auf Windows 10

In diesem Thema erläutert die neue und geänderte Funktionen in Hyper-V auf Windows 10 ®.

## Windows PowerShell-Direct

Es gibt jetzt eine einfache und zuverlässige Art des Host-Betriebssystems Windows PowerShell-Befehlen in einer virtuellen Maschine ausführen. Es gibt keine Netzwerk- oder Firewall-Anforderungen oder spezielle Konfiguration. 
Es funktioniert unabhängig von Ihrer remote-Management-Konfiguration. 

Um eine direkte PowerShell-Sitzung zu erstellen, verwenden Sie einen der folgenden Befehle:

``` PowerShell
Enter-PSSession -VMName VMName
Invoke-Command -VMName VMName -ScriptBlock { commands }
```

Heute vertrauen die Hyper-V-Administratoren auf zwei Kategorien von Werkzeugen für die Verbindung mit einer virtuellen Maschine auf ihre Hyper-V-Host:
- Remote-Management-Tools wie PowerShell oder Remote Desktop
- Verbindung mit Hyper-V virtuellen Computern (VM verbinden)

Beide Technologien funktionieren gut, aber jeweils vor-und Nachteile die Hyper-V-Bereitstellung wächst. VMConnect ist zuverlässig, aber es kann schwierig sein zu automatisieren.  

Windows PowerShell Direct bietet eine leistungsstarke scripting und Automatisierung mit der Einfachheit von VMConnect. Da Windows PowerShell direkt zwischen dem Host und den virtuellen Computer ausgeführt wird, gibt es keine Notwendigkeit für eine Netzwerkverbindung oder Remoteverwaltung aktivieren. 

#### Anforderungen
- Sie müssen verbunden sein, auf einen Windows 10 oder Windows Server Technical Preview-Host mit virtuellen Computern, die Windows 10 oder Windows Server Technical Preview als Gäste ausgeführt.
- Du musst angemeldet sein, sich mit Hyper-V-Administrator-Anmeldeinformationen auf dem Host.
- Sie benötigen Benutzeranmeldeinformationen für die virtuelle Maschine.
- Laufenden und gestarteten müssen den virtuellen Computer, die, dem Sie herstellen möchten.


## Heiß hinzufügen und Entfernen von für Netzwerkadapter und Speicher

Sie können jetzt hinzufügen oder Entfernen eines Netzwerkadapters, während der virtuelle Computer, ohne Ausfallzeiten ausgeführt wird.  

Sie können auch die Größe des Speichers, einer virtuellen Maschine zugewiesen, während es ausgeführt wird, auch wenn Sie Dynamic Memory aktiviert habe nicht anpassen. 

## Produktion-Kontrollpunkte

Produktion-Kontrollpunkte können Sie leicht "Zeitpunkt" Bilder einer virtuellen Maschine zu erstellen, die später in einer Weise wiederhergestellt werden können, die vollständig für alle Produktion Workloads unterstützt wird. Dies wird erreicht mit backup-Technologie innerhalb der Gast dem Checkpoint, anstelle von gespeicherten Zustand-Technologie erstellen. Produktion Kontrollpunkte wird das Volume Snapshot Service (VSS) in Windows virtuellen Maschinen verwendet. Linux Virtual Machines spülen ihre Dateipuffer System um eine Datei konsistent Systemprüfpunkt erstellen.  


> ** Wichtig: ** Standard für neue virtuelle Maschinen Produktion Kontrollpunkte mit Fallback auf Norm Prüfpunkte erstellt werden. 
 

## Hyper-V-Manager-Verbesserungen

- ** Alternative Anmeldeinformationen Support ** – jetzt können Sie einen anderen Satz von Anmeldeinformationen im Hyper-V-Manager beim Anschließen an ein anderes Windows 10 Technical Preview-Remotehost.  

- ** Früherer Verwaltung ** - jetzt Hyper-V-Manager können Sie um mehrere Versionen von Hyper-V zu verwalten. 

- ** Aktualisierte Management Protokoll ** - Hyper-V Manager wurde aktualisiert, um Kommunikation mit remote Hyper-V-Hosts mithilfe des WS-MAN-Protokolls, die CredSSP, Kerberos oder NTLM-Authentifizierung ermöglicht. Bei Verwendung von CredSSP zum Herstellen einer Verbindung mit eines Remotehosts Hyper-V ermöglicht es Ihnen, eine live-Migration ohne erste ermöglichen eingeschränkte Delegierung in Active Directory durchzuführen. WS-MAN-basierte Infrastruktur vereinfacht auch die Konfiguration notwendig, einen Host für die Remoteverwaltung aktivieren. 


## Standby-Modus arbeiten verbunden 

Wenn Hyper-V auf einem Computer, das Modell macht immer On/Always verbunden (AOAC) verwendet aktiviert ist, ist der Energiezustand verbunden Standby jetzt verfügbar.

Windows 8 und 8.1 verursachte Hyper-V Computer, die das immer On/Always verbunden (AOAC) macht-Modell (auch bekannt als InstantON) verwendet, um nie zu schlafen. Sehen Sie diese () [Artikel KB]
https://support.Microsoft.com/en-US/KB/2973536) für eine vollständige Umschreibung.


## Sichere Linux-boot 

Weitere Linux-Betriebssysteme, Ausführung auf Generation 2 virtuellen Maschinen, können jetzt mit aktivierter Option sicheren Boot Booten.  14,04 und später Ubuntu und SUSE Linux Enterprise Server 12, sind für sicheren Boot auf Hosts aktiviert, die die Technical Preview ausgeführt. Bevor Sie die virtuelle Maschine zum ersten Mal starten, müssen Sie angeben, dass die virtuelle Maschine die UEFI-Zertifizierungsstelle Microsoft verwenden soll. 

    Set-VMFirmware vmname -SecureBootTemplate MicrosoftUEFICertificateAuthority

Weitere Informationen über die Ausführung von Linux virtuellen Maschinen auf Hyper-V finden Sie unter [Linux und FreeBSD virtuellen Maschinen auf Hyper-V] (http://technet.microsoft.com/library/dn531030.aspx).
 
 
## Virtuelle Maschine Konfigurationsversion 

Beim Verschieben oder eine virtuelle Maschine auf einen Host mit Hyper-V auf Windows 10 von Windows 8.1-Host zu importieren, ist nicht die Konfigurationsdatei des virtuellen Computers automatisch aktualisiert. Dadurch kann die virtuelle Maschine auf einem Host mit Windows 8.1 zurück verschoben werden.  

Die VM-Konfiguration-Version stellt dar, welche Version von Hyper-V-Konfiguration des virtuellen Computers gespeicherten Zustand und snapshot-Dateien, die mit kompatibel ist. Virtuelle Maschinen mit Konfiguration der Version 5 sind kompatibel mit Windows 8.1 und Windows 8.1 und Windows 10 ausführen. 

#### Wie überprüfe ich die Konfigurationsversion der virtuellen Maschinen auf Hyper-V ausgeführt wird? 

Führen Sie den folgenden Befehl aus einer erhöhten Eingabeaufforderung:

``` PowerShell
Get-VM * | Format-Table Name, Version
```

#### Wie aktualisiere ich die Konfigurationsversion einer virtuellen Maschine?  

Führen Sie aus einer Eingabeaufforderung von Windows PowerShell einen der folgenden Befehle aus:

``` PowerShell
Update-VmConfigurationVersion <vmname>
```

Oder

``` PowerShell
Update-VmConfigurationVersion <vmobject>
```


** Wichtig: **
- Nach einem upgrade die virtuellen Maschine Konfigurationsversion Verschieben nicht möglich die virtuelle Maschine auf einen Host, die ausgeführt Windows 8.1 wird.
- Sie können die virtuelle Maschine Konfigurationsversion ab Version 6 auf Version 5 nicht herabsetzen.
- Sie müssen den virtuellen Computer für die Konfiguration des virtuellen Computers aktualisieren deaktivieren.
- Nach der Aktualisierung wird die virtuelle Maschine das Format der neuen Konfigurationsdatei verwendet. 


## Neue virtuelle Maschine Konfigurations-Dateiformat

Virtuelle Maschinen haben jetzt ein neues Dateiformat für die Konfiguration zur Steigerung der Effizienz des Lesens und Schreibens von Daten zur Konfiguration der virtuellen Maschine vorgesehen ist. Es ist auch entworfen, um das Potenzial für die Beschädigung von Daten zu reduzieren, wenn ein Speicher-Fehler vorliegt.  


> ** Wichtig: ** die. VMCX Datei ist ein binäres Format. 



## Integrationsdienste geliefert über Windows Update

Aktuelles zu Integrationsservices für Windows-Gäste sind jetzt über Windows Update verteilt.

Integrationskomponenten (auch genannt Integrationsdienste) sind der Gruppe der synthetischen Treiber ermöglichen eine virtuelle Maschine mit dem Host-Betriebssystem zu kommunizieren.  Sie kontrollieren die Dienste von Zeit Sync bis hin zu Gast-Datei kopieren. 

In der Vergangenheit kamen alle Versionen von Hyper-V mit neuen Integrationskomponenten. Aktualisieren den Hyper-V-Host benötigt, aktualisieren die Integrationskomponenten in der virtuellen Maschinen als auch.  Die neue Integrationskomponenten wurden aufgenommen mit dem Hyper-V-Host, dann wurden sie in den virtuellen Maschinen mit vmguest.iso installiert.  Dieser Prozess benötigt einen Neustart der virtuellen Maschine und konnte nicht mit anderen Windows-Updates zusammengefasst werden.  Da der Hyper-V-Administrator bieten Ihnen vmguest.iso und der virtuellen Computer-Administrator installieren mussten musste, benötigt Integration-Komponentenupdate, der Hyper-V-Administrator haben die Administratoranmeldeinformationen in den virtuellen Maschinen--was nicht immer der Fall.　

Maschinell bearbeitet in Windows 10 und künftig alle Integration, die Komponenten an virtuellen geliefert werden zusammen mit anderen wichtigen Updates über Windows Update.　

Gibt es Updates heute für ausgeführten virtuellen Computer zur Verfügung:
*  Windows Server 2012
*  Windows Server 2008 R2
*  Windows 8
*  Windows 7

Der virtuellen Maschine muss mit Windows Update oder WSUS-Server verbunden werden. 

Lesen Sie mehr über wie wir Anwendbarkeit bestimmen, finden Sie in diesem [Blogbeitrag] (http://blogs.technet.com/b/virtualization/archive/2014/11/24/integration-components-how-we-determine-windows-update-applicability.aspx).


Siehe [Dieses Blog] (http://blogs.msdn.com/b/virtual_pc_guy/archive/2014/11/12/updating-integration-components-over-windows-update.aspx) Beitrag für eine ausführliche Anleitung zum Installieren von Integrationsservices.


> ** Wichtig: ** das ISO-Abbild Datei vmguest.iso ist nicht mehr erforderlich, für die Aktualisierung von Integrationskomponenten. 




## Nächsten Schritt
[Zu Fuß durch Hyper-V unter Windows 10] (.. \quick_start\walkthrough.MD) 