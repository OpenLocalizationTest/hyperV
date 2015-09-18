<!--Reviewed by liwer 7/8/15 -->
# Export and Import virtual machines
You can use the export and import functionality to quickly duplicate virtual machines or to move them from one host to another.
You don't need to export a virtual machine to be able to import it. You can simply copy a virtual machine and its associated files to the new host, and then use the **Import Virtual Machine** wizard to specify the location of the files. This registers the virtual machine with Hyper-V and makes it available to be used.

## Virtuelle Maschinen exportieren
Eine einfache Möglichkeit, virtuelle Maschinen zu importierende vorzubereiten ist die ** exportieren VM **-Assistenten.

1. Hyper-V-Manager, wählen Sie eine oder mehrere virtuelle Maschinen, mit der rechten Maustaste auf Ihre Auswahl und wählen Sie ** Export **.
2. Klicken ** durchsuchen ** im Dialog und wählen Sie wo Sie möchten, setzen Sie die exportierte VM(s) und klicken Sie dann auf ** Wählen Sie Ordner **.
3. In der ** exportieren VM ** Dialogfeld, klicken Sie ** Export **.

Informationen zur Verwendung von Windows PowerShell, um virtuelle Maschinen zu exportieren finden Sie unter [Export-VM] (https://technet.microsoft.com/library/hh848491.aspx)

## Importieren von virtuellen Maschinen
1. In ** Hyper-V Manager **, in der ** Aktion ** im Menü klicken ** Import virtuellen Maschine **.
2. Klicken Sie im Abschnitt Ordner suchen auf Durchsuchen, und navigieren Sie zu dem die VM-Dateien befinden. <!--zu prüfen, ob dies gelöst ist - dieses verhalten ist ein Bug aus meiner sicht--> Bitte beachten Sie, dass mithilfe des Assistenten können Sie eine VM zu einem Zeitpunkt importieren und musst die VM-Ordner anstelle von den allgemeinen Exportordner auswählen. Klicken ** weiter ** wenn fertig.
3. Wählen Sie den virtuellen Computer zu importieren, und klicken Sie dann auf ** Weiter **.
4. Im Abschnitt wählen Sie Import-Typ können Sie den virtuellen Computer zu importieren:
  -  ** Register ** - nutzt die vorhandene eindeutige ID des virtuellen Computers und registriert sie vor Ort. 
  - ** ** Restore - eindeutige ID der ursprünglichen virtuellen Maschine verwendet und auch kopiert die Dateien der virtuellen Maschine auf den standardmäßigen Speicherort für den Host angegeben.
  - ** Kopie ** - erstellt eine neue eindeutige Kennung für die virtuelle Maschine und auch kopiert die Dateien der virtuellen Maschine auf den standardmäßigen Speicherort für den Host angegeben.

5. Klicken Sie nach Auswahl die VM importieren, ** weiter **.
6. Im Abschnitt wählen Sie Ziel können Sie wählen, wo Sie die Dateien für den virtuellen Computer gespeichert oder lassen sie in ihrem aktuellen Speicherort. Wenn Sie fertig sind, klicken Sie ** ** weiter.
7. Im Speicherordner auswählen können Sie einen anderen Ort zu speichern Sie die Datei .vhdx oder lassen Sie sie auswählen, wo sie sind. Wenn Sie fertig sind, klicken Sie ** ** weiter.
8. Wenn Sie die VM importieren abgeschlossen haben, sehen Sie die Seite "Zusammenfassung", beschreibt, in dem die neuen VM-Dateien befinden.

Der VM Import-Assistent führt Sie auch durch die Schritte der Adressierung Inkompatibilitäten beim Importieren der virtuelle Computer auf den neuen Host — so kann dieser Assistent mit Konfiguration helfen, die physische Hardware, wie z. B. Arbeitsspeicher, virtuelle Switches und virtuelle Prozessoren zugeordnet ist.

Um einen virtuellen Computer zu importieren, führt der Assistent die folgenden:
1. Erstellt eine Kopie der Konfigurationsdatei des virtuellen Computers. 
2. Überprüft die Hardware. 
3. Erstellt eine Liste von Fehlern. 
4. Zeigt die relevanten Seiten einer Kategorie zu einem Zeitpunkt. 
5. Entfernt die Kopie der Konfigurationsdatei. 

Neben dem Assistenten umfasst das Hyper-V-Modul für Windows PowerShell Cmdlets für den Import von virtuellen Maschinen. Weitere Informationen finden Sie unter [Import-VM] (https://technet.microsoft.com/library/hh848495.aspx).