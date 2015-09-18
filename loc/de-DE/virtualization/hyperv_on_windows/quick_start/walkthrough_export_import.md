# Schritt 7: Exportieren Sie und importieren Sie eine virtuelle Maschine 

Schnell können einen virtuellen Computer zu kopieren oder verschieben eine virtuellen Maschine mit dem Exportieren und Importieren von Funktionalität.

## Export der VM 

Exportieren einer virtuellen Maschine exportiert alle Stücke der VM, einschließlich den Checkpoints.

1. In Hyper-V-Manager mit der rechten Maustaste den virtuellen Computer, und wählen Sie ** Export **.

  ! [] (media/select_export1.png)
2. Klicken ** durchsuchen ** im Dialog box und navigieren Sie zu C:\Users\Public und klicken ** wählen Sie Ordner **. 

3. In der ** exportieren VM ** Dialogfeld, stellen Sie sicher der Pfad sieht gut und dann auf ** Export **.

  ! [] (media/click_export.png)
4. Während die VM exportiert wird, können Sie den Fortschritt im Abschnitt Status sehen:

  ! [] (media/export_progress.png) 

## Funktionierte der Export? 

Um sicherzustellen, dass die virtuelle Maschine exportiert wurde, mit einem Rechtsklick Ihrer ** Start ** Menü und wählen Sie ** Datei Explorer **.
1. Navigieren Sie zu C:\Users\Public\Windows Exemplarische Vorgehensweise VM.
2. Sehen Sie einen anderen Ordner namens Windows Walkthrough VM und in diesem Ordner sollte drei Ordner mit den Dateien für Ihre exportierten virtuellen Maschine:
 - Momentaufnahmen
 - Virtuelle Festplatten
 - Virtuelle Maschinen 
 
  ! [] (media/export_confirm.png)

## Die VM importieren 

Bevor wir die VM importieren, werden wir die ursprüngliche VM löschen. Mit der rechten Maustaste auf die VM und wählen ** Löschen **. 
1. In ** Hyper-V Manager **, in der ** Aktion ** im Menü klicken ** Import virtuellen Maschine **.
2. In der ** suchen Sie Ordner ** Abschnitt, klicken Sie auf Durchsuchen und navigieren Sie zu C:\Users\Public\Windows Exemplarische Vorgehensweise VM und klicken ** weiter **.
3. In der ** wählen Sie Virtual Machine Import ** Bildschirm klicken ** weiter **.
4. In der ** Import-Typ wählen Sie ** wählen Sie Abschnitt ** die virtuelle Maschine im Ort ** registrieren und dann auf ** Weiter **. 
6. In der ** wählen Sie Ziel ** Abschnitt, behalten Sie die Standardeinstellung, und klicken Sie auf ** Weiter **.
7. Im Speicherordner auswählen lassen den Standardpfad, und klicken Sie auf ** Weiter **.
8. Auf der Übersichtsseite sehen Sie eine Liste der Pfade, wo die neuen VM-Dateien gespeichert werden. Klicken ** fertig ** um den Import zu starten.


## Funktionierte der Import? 

Um sicherzustellen, dass der Import arbeitete, ein Doppelklick auf die VM in ** Hyper-V Manager ** und Launch VMConnect um die VM zu überprüfen. 

## Nächster Schritt: 
[Schritt 8: Experiment mit Windows Powershell] (walkthrough_powershell.md)