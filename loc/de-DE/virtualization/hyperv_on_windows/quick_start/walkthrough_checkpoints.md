# Schritt 6: Experiment mit checkpoints 

Kontrollpunkte sind ein hilfreiches Werkzeug, wenn Sie den aktuellen Status einer virtuellen Maschine zu speichern, bevor Sie eine Änderung wie Anwenden eines Updates, Software installieren oder Ändern einer Einstellung möchten.   

Es gibt zwei Arten von Checkpoints: ** Produktion Prüfpunkte **: hauptsächlich auf Servern in Produktionsumgebungen eingesetzt.  
** Standard-Kontrollpunkte **: bei der Entwicklung verwendet oder Testumgebungen 

Produktion-Kontrollpunkte sind Standard für Hyper-V auf Windows 10.


## Den Prüfpunkt-Typ ändern
Wir fangen durch Ausprobieren den älteren Stil von Checkpoints, ** standard-Kontrollpunkte **. 

1. Mit einem Rechtsklick **, und wählen Sie Windows-VM "Walkthrough" ** ** Einstellungen **.
2. In der ** Management ** wählen Sie Abschnitt ** Checkpoints **.
3. Wählen Sie ** Standard Prüfpunkte **. 

  ! [] (media/standard1.png)
4.	Klicken ** OK **, um das Dialogfeld zu schließen.

## Offen Notepad Prüfpunkte zu testen 
Um zu sehen, was passiert mit jeder Art von Prüfpunkt, werden wir eine Anwendung in der VM ausführen. 
1. Mit einem Rechtsklick **, und wählen Sie Windows-VM "Walkthrough" ** ** Connect **.
2. In der virtuellen Maschine öffnen ** Notepad ** durch Anklicken der ** Start ** Menü klicken und eingeben ** Notepad ** und wählen Sie es aus den Ergebnissen. 
3. Geben Sie im Editor ** Dies ist ein Test der checkpoints.* * die Datei sollte so aussehen:
  
  ! [] (media/standard_notepad.png)
4. Speichern Sie die Datei als ** test.txt**, aber nicht schließen Sie den Editor. 

## Erstellen Sie einen standard-checkpoint 
1. Um den Prüfpunkt zu erstellen, klicken Sie auf die! [] (media/checkpoint_button.png) ** Checkpoint ** Taste in der Menüleiste. 
2. Geben Sie im Dialogfeld Name Prüfpunkt ** Standard **. 

  ! [] (media/save_standard.png) 
3. Wenn der Prozess abgeschlossen ist, erscheint der Prüfpunkt unter ** Checkpoints ** in der ** Hyper-V Manager **.

  ! [] (media/standard_complete.png) 

## Erstellen eines Checkpoints Produktion 
Jetzt müssen wir ändern, ändern Sie den Typ des Prüfpunkts, die wir wollen zurück zu nehmen ** Produktion Prüfpunkte ** vor der Einnahme eines zweiten Checkpoints.

1.	Mit der rechten Maustaste den virtuellen Computer, und klicken Sie auf ** Einstellungen **.
2.	In der ** Management ** wählen Sie Abschnitt ** Checkpoints **.
3.	Wählen Sie ** Produktion Prüfpunkte **.
4.  Deaktivieren Sie die Option Herbst-zurück. 

  ! [] (media/production.png)
5.	Klicken ** OK **, um das Dialogfeld zu schließen.
6.	Der rechten Maustaste auf den virtuellen Computer erneut, und wählen Sie ** ** verbinden.
7.	Geben Sie im Editor in der VM eine weitere Zeile ** Dies ist ein Test der Produktion Prüfpunkt ** und speichern Sie die Datei erneut.
8.	Klicken Sie auf die! [] (media/checkpoint_button.png) ** Checkpoint ** Taste in der Menüleiste.
9.	Wenn gefragt, nennen Sie es ** Produktion ** und klicken Sie dann auf ** Ja **.

  ! [] (media/production_CheckpointName.png) 
10. VMConnect zu schließen. 
11. In Hyper-V-Manager wird Ihre Liste von Checkpoints nun so aussehen:

  ! [] (media/production_complete.png)



## Anwenden der Norm checkpoint 

1.	In ** Hyper-V Manager **, in der ** Checkpoints ** Abschnitt der rechten Maustaste auf diejenige mit dem Titel ** Standard ** und klicken ** übernehmen **.
2.	Klicken Sie im Popup-Dialog ** Prüfpunkt erstellen und anwenden **. 

  ! [] (media/apply_standard.png)
34. Wenn das fertig, Ihre Liste von Checkpoints jetzt wird etwa wie folgt aussehen:

  ! [] (media/standard_applied.png)
4. Wenn dies abgeschlossen ist, mit der rechten Maustaste den virtuellen Computer und dann auf ** Connect ** zum Herstellen einer Verbindung mit der VM. 
5. Beim Anschließen an die VM die VM sollte laufen, mit Notepad geöffnet, aber die Linie über Produktion Prüfpunkte werden fehlende:

  ! [] (media/standard_applied_notepad.png)
6. VMConnect zu schließen, aber die VM laufen lassen.


## Anwenden der Produktion-checkpoint 
Nun gehen Sie wir zurück zu Hyper-V Manager und wenden Sie Checkpoint Produktion an und sehen Sie, wie unsere VM danach aussieht.

1.	Klicken Sie im Abschnitt Checkpoints derjenige mit dem Titel ** Produktion Checkpoint ** und klicken ** übernehmen **.
2.	Wählen Sie im Popup-Dialog ** Prüfpunkt erstellen und anwenden **. 
3. Wenn dies abgeschlossen ist, mit der rechten Maustaste den virtuellen Computer und dann auf ** Connect ** die VM zu starten. 
4. Sie werden bemerken, dass die VM nicht ausgeführt wird. Klicken Sie auf die! [] (media/start.png)-Start-Button in der Menüleiste auf die VM gestartet.
5. Öffnen Sie in Editor öffnen test.txt. 

  ! [] (media/production_notepad.png)
	

## Umbenennen eines Checkpoints ##
1. Maustaste auf dem letzten Checkpoint in der Struktur, und klicken Sie auf Umbenennen.
2. Nennen Sie dem Checkpoint ** löschen Sie mich **.

  ! [] (media/delete_me.png)

## Löschen eines Checkpoints 
Vorherige Schritt hat wahrscheinlich Sie gegeben einen Hinweis, was wir als nächstes tun werde. 

1. Mit einem Rechtsklick der Prüfpunkt mit dem Namen ** löschen Sie mich ** und klicken Sie auf ** Löschen Prüfpunkt **. 

  ! [] (media/delete_checkpoint.png)
2. Klicken Sie im Dialogfeld Warnung ** löschen **. 

  ! [] (media/delete_warn.png)
3. Nach dem Checkpoint gelöscht wird, sollte die Liste wie folgt aussehen:

  ! [] (media/after_delete.png)


## Nächster Schritt: 
[Schritt 7: Export und Import eines virtuellen Computers] (walkthrough_export_import.md)


