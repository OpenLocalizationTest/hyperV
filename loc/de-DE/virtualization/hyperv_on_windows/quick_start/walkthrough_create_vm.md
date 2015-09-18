# Schritt 4: Erstellen einer virtuellen Windows-Maschine aus einer .iso-Datei 

Für diesen Schritt haben Sie bereits eine .iso-Datei für eine unterstützte 64-Bit-Betriebssystem können, das Sie. Wenn nicht, können die .iso für [Windows 8.1 Enterprise] (http://www.microsoft.com/en-us/evalcenter/evaluate-windows-8-1-enterprise) herunterladen und wählen Sie die 64-Bit-Edition. 

1. Klicken Sie im Hyper-V-Manager auf die ** Aktion ** Menü > ** neu ** > ** VM **. 
2. Stellen Sie im virtuellen Computer-Assistenten die folgenden Auswahlmöglichkeiten:

    <table>
    <tr><th>Page</th><th>Entry</th></tr>
    <tr><td>Name:</td><td>Type in <b>Windows Walkthrough VM</b></td></tr>
    <tr><td>Generation:</td><td><b>Generation 2</b></td></tr>
    <tr><td>Startup Memory:</td><td><b>1024</b> and leave dynamic memory selected</td></tr>
	<tr><td>Configure Networking:</td><td><b>External</b> (this is the virtual switch you created in Step 3)</td></tr>
    <tr><td>Connect virtual hard disk:</td><td><b>Create a virtual hard disk</b> (keep the other default values) </td></tr>
    <tr><td>Installation Options:</td><td><b>Install an operating system from a bootable CD/DVD-ROM</b>. Under <b>Media</b>, select <b>Image file (iso)</b> and then click <b>Browse</b> to point to the .iso file.</td></tr>
    </table>
  
3. Wenn alles gut aussieht, klicken Sie auf ** Fertig **. 

> ** Hinweis: ** Wenn Sie nur 32-Bit-Version von Windows haben, musst du Generation 1 in wählen die ** Generation ** Abschnitt des Assistenten. 

## Nächster Schritt: 
[Schritt 5: Verbinden Sie mit dem virtuellen Computer und schließen Sie die Installation] (walkthrough_vmconnect.md)

