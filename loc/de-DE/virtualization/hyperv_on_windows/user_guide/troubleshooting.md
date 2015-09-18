# Problembehandlung beim Hyper-V auf Windows 10

## Ich aktualisierte Windows 10 und jetzt ich bekomme keine Verbindung zu meiner Downlevel-Host (Windows 8.1 oder Server 2012 R2)
Windows 10 zog Hyper-V-Manager zu WinRM für die Remoteverwaltung. 

Weitere Informationen finden Sie unter [Managing Remote Hyper-V Hosts](remote_host_management.md)

## Ich änderte den Prüfpunkt-Typ, aber es nimmt immer noch die falsche Art von checkpoint
Wenn Sie dem Checkpoint von VMConnect einnehmen und Ändern des Prüfpunkt-Typs in Hyper-V-Manager der Prüfpunkt getroffen werden Sie gleich welcher Art Prüfpunkt angegeben wurde, als VMConnect eröffnet wurde.

VMConnect zu schließen und wieder öffnen zu machen, die richtige Art der Prüfpunkt zu nehmen.

## Wenn ich versuche, eine virtuelle Festplatte auf einem Flashlaufwerk erstellen, wird eine Fehlermeldung angezeigt.
Hyper-V unterstützt FAT/FAT32-formatierten Laufwerken nicht, da diese Dateisysteme keine Zugriffssteuerungslisten (ACLs bieten) und keine Dateien größer als 4GB unterstützen. ExFAT formatiert Disketten nur begrenzte ACL-Funktionen und werden daher ebenfalls nicht unterstützt aus Sicherheitsgründen.
Die Fehlermeldung in PowerShell angezeigt wird "das System versagte beim Erstellen ' \[path, VHD\]': der angeforderte Vorgang konnte nicht abgeschlossen werden, aufgrund einer Datei Systemeinschränkung (0x80070299)."

Verwenden einer NTFS formatierten Laufwerk statt. 

## Wenn ich versuche zu installieren erhalte ich diese Fehlermeldung: "Hyper-V kann nicht installiert werden: der Prozessor unterstützt keine zweite Ebene Adressübersetzung (Stab)."
Hyper-V erfordert SLAT, um virtuelle Maschinen ausführen. 

Wenn Sie nur die Verwaltungstools installieren möchten, deaktivieren Sie ** Hyper-V Plattform ** in ** Programme und Features ** > ** Windows-Funktionen ein- oder ausschalten **.
