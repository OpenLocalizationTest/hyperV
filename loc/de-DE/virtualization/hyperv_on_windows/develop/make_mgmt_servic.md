# Machen Sie einen neuen Management-service #
Dieses Dokument stellt VM-Diensten, das auf Hyper-V-Steckdosen und wie man mit ihnen beginnen.

! [](.. / media/1.png)

## Was ist ein VM-Service?
VM sind Dienste, die die Hyper-V-Hosts und virtuelle Maschinen auf dem Host zu erstrecken.

Hyper-V jetzt (Windows 10 and Server 2016 +) bietet eine nicht-Netz-Verbindung, die Sie Dienstleistungen umfassen die Host/virtuelle Maschine-Grenze unter Beibehaltung der grundsätzlichen Anforderungen der Hyper-V um Mieter/Hoster Isolation, Kontrolle, erstellen kann und diagnostizierbar.

Hyper-V bietet weiterhin einen Basissatz von in-Box-Service (Integrationsservices) für Grundlagen (z. B. Zeit Sync) und für allgemeine Anfragen, die wir erhalten, aber jetzt kann jeder schreiben und einen VM-Dienst bereitstellen, wie gebraucht.

PowerShell-Direct ist ein in-Box-Beispiel eines VM-Dienstes.

## Was ist eine Hyper-V-Steckdose?
Hyper-V-Steckdosen sind wie TCP Sockets mit keine Abhängigkeit von Vernetzung. 

## System-Anforderungen

** Unterstützte Host OS **
*	Windows 10
*	Windows Server technische Vorschau 3
*	Zukünftige Versionen (Server-2016 +)

** Unterstützte Gast OS **
*	Windows 10
*	Windows Server technische Vorschau 3
*	Zukünftige Versionen (Server-2016 +)
*	Linux

## Möglichkeiten und Grenzen
Kernelmodus oder im Benutzermodus Datenstrom nur keine Block-Speicher also nicht das beste für Backup/Video  

## Erste Schritte

Dieses Handbuch setzt voraus, dass Sie mit Socket-Programmierung in C/C++ vertraut bist.

### Schritt 1: Registrieren Sie Ihren Dienst auf dem Hyper-V-host
Um einen benutzerdefinierten Dienst integriert mit Hyper-V zu verwenden, muss der neue Dienst mit dem Hyper-V-Host-Registrierung registriert werden.

Mit der Registrierung des Diensts in der Registrierung erhalten Sie:
*  WMI-Management für aktivieren, deaktivieren und Auflisten der verfügbaren Dienste
*  Auf der Liste der Dienste mit virtuellen Maschinen direkt kommunizieren darf.

** Registrierungspfad und Informationen **  

``` 
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Virtualization\VirtualDevices\6C09BB55-D683-4DA0-8931-C9BF705F6480\GuestCommunicationServices\
```
Position in der Registrierung sehen Sie mehrere GUIDS. 

Informationen in der Registrierung pro Dienst:
* 'Service GUID'   
    * 'ElementName (REG_SZ)'--das ist Anzeigename des Dienstes

Um Ihren eigenen Service zu registrieren, erstellen Sie einen neuen Registrierungsschlüssel, die mit Ihren eigenen GUID und angezeigter Name.

Der Registrierungseintrag wird so aussehen:
```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Virtualization\GuestCommunicationServices\
    999E53D4-3D5C-4C3E-8779-BED06EC056E1\
	    ElementName	REG_SZ	VM Session Service
    YourGUID\
	    ElementName	REG_SZ	Your Service Friendly Name
```

> ** Tipp: ** um eine GUID in PowerShell zu generieren und in die Zwischenablage zu kopieren, führen:  
``` PowerShell
[System.Guid]::NewGuid().ToString() | clip.exe
```

<!-- How do customers know this worked -->

### Schritt 2 - Erstellen Sie einen einfachen hostseitige-Dienst



### Schritt 3 - Erstellen Sie einen einfachen Gast-Seite service

## Weitere Informationen zu AF_HYPERV
Da Hyper-V-Buchsen nicht Netzwerkstack, TCP/IP, DNS, abhängen usw.. der Socket-Endpunkt benötigt eine nicht-IP, nicht Hostname, Datenformat, das noch die Verbindung beschreibt.  Anstelle einer IP oder Hostname AF_HYPERV Endpunkte angewiesen auf zwei GUIDS:  
* VM-ID – Dies ist die eindeutige ID pro VM zugeordnet. 
```PowerShell
(Get-VM -Name vmname).Id
```
* Service ID-GUID, unter denen der Dienst in der Hyper-V-Host-Registrierung registriert ist.  Finden Sie unter [registrieren eine neue Service](#GettingStarted).

Für Verbindungen von einem Dienst auf dem Host mit dem Dienst auf einer VM: VMID und Service-ID
Für Verbindungen von einem Dienst auf einer VM zum Dienst auf dem Host: Zero-GUID und Service-ID

## Unterstützten Socket-Befehle

Socket()
BIND()
Connect()
Send()
'Listen()'-Aufruf
Wird accept()


 
