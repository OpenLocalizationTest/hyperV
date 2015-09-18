# Migrieren und Aktualisieren von virtuellen Maschinen 


Wenn Sie virtueller Maschinen auf Maschinenebene Windows 10, die ursprünglich mit Hyper-V in Windows 8.1 oder früher erstellt wurden verschieben, werden nicht Sie möglicherweise die neue virtuelle Maschine-Features verwenden, bis Sie die virtuelle Maschine Konfigurationsversion manuell aktualisieren. 

Um die Konfigurationsversion zu aktualisieren, den virtuellen Computer Herunterfahren Sie, und wählen Sie dann zum Upgrade Konfiguration des virtuellen Computers in Hyper-V Manager.  

 ```PowerShell
Update-VmVersion <vmname> | <vmobject>
```



## Wie überprüfe ich die Konfigurationsversion der virtuellen Maschinen auf Hyper-V ausgeführt wird? 

Um die Konfigurationsversion zu finden, öffnen Sie eine Windows PowerShell-Eingabeaufforderung, und führen Sie den folgenden Befehl:

** Get-VM * | Format-Table-Name, Version **

Der PowerShell-Befehl erzeugt die folgende Beispielausgabe:

```
Name		State		CPUUsage(%)	MemoryAssigned(M)	Uptime				Status					Version
    
Atlantis	Running			0		1024			 	00:04:20.5910000	Operating normally		5.0
    
SGC VM		Running			0		538 	 			00:02:44.8350000	Operating normally		6.2
```


## Was passiert, wenn ich nicht die Konfiguration der Version aktualisieren?

Wenn Sie virtuelle Computer, die Sie mit einer früheren Version von Hyper-V erstellt verfügen, einige Funktionen funktioniert möglicherweise nicht mit diesen virtuellen Maschinen bis Sie die VM-Version zu aktualisieren.

Minimale Version von VM-Konfiguration für Hyper-V-Neuerungen:

| ** Funktion Name ** | ** Mindestens VM Version ** ||
| :------------------------------------- | -----------------: ||
| Hinzufügen/Entfernen von Speicher warm |                6.0 ||
| Heiße Netzwerkadapter hinzufügen/entfernen |                5.0 ||
| Secure Boot für Linux-VMs |                6.0 ||
| Produktion-Checkpoints |                6.0 || 
| PowerShell-Direct |                6.2 ||
| Virtuelle Trusted Platform Module (vTPM) |                6.2 ||
| Virtuelle Maschine Gruppierung |                6.2 ||



## Virtuelle Maschine Konfigurationsversion ##

Beim Verschieben oder eine virtuelle Maschine auf einen Host mit Hyper-V auf Windows 10 von Windows 8.1-Host zu importieren, ist nicht die Konfigurationsdatei des virtuellen Computers automatisch aktualisiert. Dadurch kann die virtuelle Maschine auf einem Host mit Windows 8.1 zurück verschoben werden.  

Die VM-Konfiguration-Version stellt dar, welche Version von Hyper-V-Konfiguration des virtuellen Computers gespeicherten Zustand und snapshot-Dateien, die mit kompatibel ist. Virtuelle Maschinen mit Konfiguration der Version 5 sind kompatibel mit Windows 8.1 und Windows 8.1 und Windows 10 ausführen. 

Es ist nicht notwendig, um alle virtuellen Computer gleichzeitig zu aktualisieren. Sie können wählen, um bestimmte virtuelle Maschinen bei Bedarf zu aktualisieren.   


----------------
** Wichtig **

• Nach einem upgrade die virtuellen Maschine Konfigurationsversion Verschieben nicht möglich die virtuelle Maschine auf einen Host, die ausgeführt Windows 8.1 wird.

• Sie können die virtuelle Maschine Konfigurationsversion ab Version 6 auf Version 5 nicht herabsetzen.

• Sie müssen den virtuellen Computer für die Konfiguration des virtuellen Computers aktualisieren deaktivieren.

• Nach der Aktualisierung wird die virtuelle Maschine das Format der neuen Konfigurationsdatei verwendet. 

--------





## Was passiert, wenn ich ein der Version einer virtuellen Maschine Upgrade?
Wenn Sie manuell aktualisieren, die Konfigurationsversion einer virtuellen Maschine auf Version 6.x, ändern Sie die Dateistruktur, die zum Speichern der virtuellen Maschinen-Konfiguration und Checkpoint-Dateien verwendet wird. 

Aktualisierten virtuellen Maschinen verwendet ein neues Format für Konfiguration, zur Steigerung der Effizienz des Lesens und Schreibens von Daten zur Konfiguration der virtuellen Maschine vorgesehen ist.  

Die folgende Tabelle listet die Binärdatei Standorte und Erweiterungsinformationen für eine aktualisierte virtuelle Maschine.  

| ** VM-Konfiguration und Checkpoint-Dateien (Version 6.x)**|**Description**||
|:---------------|:----------------||
| ** Konfiguration der virtuellen Maschine ** | Konfigurationsinformationen werden in einem binären Dateiformat gespeichert, das die .vmcx-Erweiterung verwendet. ||
| ** VM Runtime Zustand ** | Zustandsdaten Runtime werden in ein binäres Dateiformat gespeichert, das die .vmrs-Erweiterung verwendet.  ||
| ** VM virtuelle Festplatte ** | Die virtuelle Festplatte-Dateien für den virtuellen Computer. Sie verwenden die Dateierweiterungen VHD oder .vhdx.   ||
| ** Automatische virtuelle Festplatte Dateien ** | Die differenzierende virtuelle Maschine Kontrollpunkte verwendeten Datenträgerdateien. Sie verwenden die .avhdx-Datei-Erweiterungen. ||
| ** Prüfpunkt Dateien ** | Prüfpunkte werden in mehreren Checkpoint-Dateien gespeichert. Jedem Checkpoint erstellt eine Konfigurationsdatei und Runtime-Statusdatei. Checkpoint-Dateien verwenden, die .vmrs und .vmcx Dateierweiterungen. Diese neuen Dateiformate werden auch für Produktion Checkpoints und Norm Prüfpunkte verwendet. 

Nachdem Sie die Konfiguration des virtuellen Computers aktualisiert Version zu Version 6.x, es ist nicht möglich, downgrade von Version 6.x auf Version 5. 

Die virtuelle Maschine muss deaktiviert werden, um die Konfiguration des virtuellen Computers zu aktualisieren.

Die folgende Tabelle listet die Datei Standardspeicherorte für neue oder aktualisierte virtuelle Maschinen.

|   ** Dateien des virtuellen Computers (Version 6.x)** | ** Beschreibung ** ||
|:-----|:-----||
| ** VM-Konfiguration-Datei ** | C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Maschinen ||
| ** VM Runtime Status Datei ** | C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Maschinen ||
| ** Checkpoint-Dateien (.vmrs, .vmcx) ** | C:\ProgramData\Microsoft\Windows\Snapshots ||
| ** Virtuelle Festplattendatei (.vhd/.vhdx)**| C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks ||
| ** Automatische virtuelle Festplatte-Dateien (.avhdx) ** | C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks ||




