# Verwendung von Prüfpunkten virtuelle Computer in einen früheren Zustand wiederherstellen

Prüfpunkte bieten eine schnelle und einfache Möglichkeit, den virtuellen Computer in einen früheren Zustand wiederherzustellen. 


## Aktivieren oder Deaktivieren von Prüfpunkten

1.	In ** Hyper-V Manager **, klicken Sie mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie auf ** Einstellungen **.
2.	In der ** Management ** wählen Sie Abschnitt ** Checkpoints **.
3.	Damit können Kontrollpunkte dieser virtuellen Maschine abgenommen werden, stellen Sie sicher, dass Checkpoints aktivieren ausgewählt ist--ist dies das Standardverhalten.  
Um die Prüfpunkte zu deaktivieren, deaktivieren Sie die ** Kontrollkästchen aktivieren Checkpoints **.
4.	Klicken ** übernehmen ** um Ihre Änderungen zu übernehmen. Wenn Sie fertig sind, klicken Sie ** OK **, um das Dialogfeld zu schließen.


## Wählen Sie Standard oder Produktion Prüfpunkte

Es gibt zwei Arten von Checkpoints:
*  ** Produktion Prüfpunkte **--als eine Form der Sicherung vor allem auf Servern in Produktionsumgebungen verwendet.
*  ** Standard Prüfpunkte **--in Entwicklungs- oder Testumgebungen verwendet, um Rollback zu ermöglichen, wenn eine Änderung fehlschlägt. 

Beide Arten von Checkpoints wiederherstellen eine virtuelle Maschine auf einen früheren Zustand.

Produktion-Kontrollpunkte erstellt ein anwendungskonsistente-Checkpoint einer virtuellen Maschine.   

Norm Prüfpunkte (früher bekannt als Snapshots) erfassen den genaue Speicherstatus Ihrer virtuellen Maschine.  Das bedeutet, dass die virtuelle Maschine wird mit wiederherstellen ** genau ** den gleichen Zustand, in dem der Prüfpunkt wurde zur genauen Anwendungszustand abgerissen.  
Norm-Kontrollpunkte können Informationen über Client-Verbindungen, Transaktionen und den externen Netzwerk-Status enthalten. Diese Informationen möglicherweise nicht gültig, wenn der Prüfpunkt angewendet wird. 

Das Vorhandensein einer Norm-Checkpoint für eine virtuelle Maschine kann die Datenträgerleistung des virtuellen Computers auswirken. 


Anwenden eines Checkpoints Produktion umfasst Offlinestatus das Gast-Betriebssystem gebootet.  

Die folgende Tabelle zeigt wann Produktion Prüfpunkte oder Norm Kontrollstellen, je nach Zustand des virtuellen Computers zu verwenden.

|   ** Virtuelle Maschine Zustand ** | ** Produktion Checkpoint ** |  ** Standard-Checkpoint ** |
|:-----|:-----|:-----|
| ** Mit Integration Services ** | Ja | Ja |
| ** Läuft ohne Integration Services ** | Nein | Ja | 
| ** Offline - keine gespeicherten Zustand ** | Ja | Ja |
| ** Offline - mit gespeicherten Zustand ** | Nein | Ja |
| ** Angehalten ** | No| Ja |

Um den Unterschied zwischen Standard- und Produktion Checkpoints zu sehen, Schau dir die [Prüfpunkte Anleitung] (.. / quick_start/walkthrough_checkpoints.md).

## Legen Sie einen Prüfpunkt Standardtyp

1.	In ** Hyper-V Manager **, klicken Sie mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie auf ** Einstellungen **.
2.	In der ** Management ** wählen Sie Abschnitt ** Checkpoints **.
3.	Wählen Sie entweder Produktion Prüfpunkte oder Norm Prüfpunkte. 
Wenn Sie Produktion Prüfpunkte wählen, können Sie auch angeben, ob der Host einen Norm Prüfpunkt ergreifen sollten, wenn ein Prüfpunkt Produktion nicht gefasst werden kann. 
4.	Wenn Sie möchten den Speicherort zu ändern, in dem die Konfigurationsdateien für den Prüfpunkt gespeichert werden, ändern Sie den Pfad in der ** Checkpoint Datei Lage ** Abschnitt.
5.	Klicken ** übernehmen ** um Ihre Änderungen zu übernehmen. Wenn Sie fertig sind, klicken Sie ** OK **, um das Dialogfeld zu schließen.

Das Standardverhalten in Windows 10 für neue virtuelle Computer ist Produktion Kontrollpunkte mit Fallback auf Norm Prüfpunkte erstellt werden.


## Erstellen eines Checkpoints
Um einen Checkpoint zu erstellen
1.	In ** Hyper-V Manager **, ** virtuelle Maschinen **, wählen Sie die virtuelle Maschine.
2.	Klicken Sie mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie dann auf ** Checkpoint **.
3.	Wenn der Prozess abgeschlossen ist, erscheint der Prüfpunkt unter ** Checkpoints ** in der ** Hyper-V Manager **. 


## Anwenden eines Checkpoints
Wenn Sie Ihren virtuellen Computer zu einem früheren-Zeitpunkt wiederherstellen möchten, können Sie ein vorhandenes Checkpoint anwenden.

1.	In ** Hyper-V Manager **, ** virtuelle Maschinen **, wählen Sie die virtuelle Maschine.
2.	Im Abschnitt Checkpoints Maustaste dem Checkpoint, die Sie verwenden möchten und klicken Sie auf ** übernehmen **.
3.	Es erscheint ein Dialogfenster mit den folgenden Optionen: 

```	
**Create Checkpoint and Apply**: Creates a new checkpoint of the virtual machine before it applies the earlier checkpoint. 

**Apply**: Applies only the checkpoint that you have chosen. You cannot undo this action.

**Cancel**: Closes the dialog box without doing anything.
```

##Delete ein Prüfpunkt

Um einen Checkpoint sauber zu löschen: 

1.	In ** Hyper-V Manager **, wählen Sie die virtuelle Maschine.
2.	In der ** Checkpoints ** Abschnitt mit der rechten Maustaste des Prüfpunkts, die Sie löschen möchten, und klicken Sie auf Löschen. Sie können auch einen Checkpoint und alle nachfolgenden Checkpoints löschen. Dazu mit der rechten Maustaste des frühesten Prüfpunkts, die Sie löschen, und klicken Sie dann auf möchten *** löschen Checkpoint ** Unterstruktur **.
3.	Sie möglicherweise aufgefordert, sicherzustellen, dass den Prüfpunkt löschen möchten. Bestätigen, dass es der richtige Checkpoint, und klicken Sie auf ** Löschen **. 
4.	Die Dateien .avhdx und .vhdx Zusammenführen werden, und wenn Sie fertig sind, wird die .avhdx-Datei aus dem Dateisystem gelöscht werden. 

> ** Tipp: ** können Sie Windows Powershell mit einen Prüfpunkt löschen die ** entfernen-VMSnapshot ** Cmdlet. 
 
 Prüfpunkte werden als .avhdx-Dateien in demselben Speicherort wie die .vhdx-Dateien für den virtuellen Computer gespeichert. 
 

## Ändern wo Prüfpunkt Einstellungen und Speichern des Zustands Dateien werden gespeichert
Wenn die virtuelle Maschine keine Checkpoints verfügt, können Sie ändern, in dem die Prüfpunkt-Konfiguration und gespeicherten Zustand Dateien gespeichert werden.

1.	In ** Hyper-V Manager **, klicken Sie mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie auf ** Einstellungen **.
	
2.	In der ** Management ** wählen Sie Abschnitt ** Checkpoints ** oder ** Checkpoint Datei Lage **.
	
4.	In ** Checkpoint Datei Lage **, geben Sie den Pfad zu dem Ordner, wo Sie die Dateien speichern möchten.
	
5.	Klicken ** übernehmen ** um Ihre Änderungen zu übernehmen. Wenn Sie fertig sind, klicken Sie ** OK **, um das Dialogfeld zu schließen.

Der standardmäßige Speicherort zum Speichern der Konfiguration Prüfpunktdateien ist: % systemroot%\ProgramData\Microsoft\Windows\Hyper-V\Snapshots.


<!-- This belongs in dev docs

Dieser Ordner enthält die. VMRS Datei mit der Common Language Runtime und gespeicherte Zustandsdaten und ein. VMCX-Konfigurationsdatei, die dem Checkpoint GUID als Dateiname verwendet.
-->

## Umbenennen eines Checkpoints

1.	In ** Hyper-V Manager **, wählen Sie die virtuelle Maschine.
2.	Maustaste auf dem Checkpoint, und wählen Sie dann ** ** Umbenennen.
3.	Geben Sie den neuen Namen für den Prüfpunkt. 
4.	Klicken ** ENTER ** Wenn Sie fertig sind.

Standardmäßig ist der Name von einem Checkpoint der Name der virtuellen Maschine kombiniert mit Datum und Uhrzeit, die der Prüfpunkt getroffen wurde.  

```
virtual_machine_name (MM/DD/YYY –hh:mm:ss AM\PM)
```

Namen sind auf 100 Zeichen oder weniger beschränkt, und der Name darf nicht leer sein. 


