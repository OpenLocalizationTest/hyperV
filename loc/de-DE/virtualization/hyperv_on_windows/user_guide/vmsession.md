# Verwalten von Windows PowerShell direkten #
PowerShell-Direct können Sie die Remoteverwaltung eines Windows 10 oder virtuelle Maschine Windows Server Technical Preview von einem Windows 10 oder Windows Server technische Vorschau Hyper-V-Host. PowerShell-Direct ermöglicht PowerShell Management innerhalb eines Virtual machine unabhängig von der Netzwerkkonfiguration oder remote-Management-Einstellungen auf entweder die Hyper-V-Host oder der virtuellen Maschine. 

Es gibt zwei Möglichkeiten zum Ausführen von PowerShell-Direct:  
* Erstellen Sie und beenden Sie eine Sitzung des PowerShell-Direct mit PSSession cmdlets
* Run-Skript oder mit dem Cmdlet Invoke-Command Befehl

Wenn Sie ältere virtuelle Maschinen verwalten, verwenden Verbindung mit virtuellen Computern (VMConnect) oder [konfigurieren ein virtuelles Netzwerks für die virtuelle Maschine] (http://technet.microsoft.com/library/cc816585.aspx). 

## Erstellen Sie und beenden Sie eine Sitzung des PowerShell-Direct mit PSSession cmdlets
1. Öffnen Sie Windows PowerShell auf dem Hyper-V-Host als Verwalter.

3. Führen Sie eine der folgenden Befehle zum Erstellen einer Sitzung mithilfe der Name der virtuellen Maschine oder GUID:  
``` PowerShell
Enter-PSSession -VMName VMName
Enter-PSSession -VMGUID VMGUID
```

4. Führen Sie was Befehle, die Sie benötigen. 
5. Wenn Sie fertig sind, führen Sie den folgenden Befehl zum Schließen der Sitzung:  
``` PowerShell
Exit-PSSession 
``` 

> Hinweis: Wenn Sie die Sitzung sind nicht anschließen, stellen Sie sicher Sie verwenden Anmeldeinformationen für den virtuellen Computer, die Sie an--nicht den Hyper-V-Host herstellen.

Weitere Informationen zu diesen Cmdlets siehe [Enter-PSSession] (http://technet.microsoft.com/library/hh849707.aspx) und [Exit-PSSession] (http://technet.microsoft.com/library/hh849743.aspx). 

## Run-Skript oder mit dem Cmdlet Invoke-Command Befehl

Das Cmdlet [Invoke-Command] (http://technet.microsoft.com/library/hh849719.aspx) können Sie einen vordefinierten Satz von Befehlen auf dem virtuellen Computer ausgeführt. 

 ``` PowerShell
 Invoke-Command -VMName PSTest -FilePath C:\script\foo.ps1 
 ```

Um einen Einzelbefehl auszuführen, verwenden Sie die **-ScriptBlock ** Parameter:

 ``` PowerShell
 Invoke-Command -VMName PSTest -ScriptBlock { cmdlet } 
 ```

## Was ist erforderlich, um PowerShell direkt verwenden?
Eine direkte PowerShell-Sitzung auf einem virtuellen Computer zu erstellen,
* Die virtuelle Maschine muss lokal auf dem Host ausgeführt werden und gebootet. 
* Sie müssen in den Hostcomputer als Hyper-V-Administrator angemeldet sein.
* Sie müssen gültige Benutzeranmeldeinformationen für die virtuelle Maschine angeben.
* Das Host-Betriebssystem muss Windows 10 Windows Server Technical Preview oder eine höhere Version ausgeführt.  
* Der virtuelle Computer muss Windows 10 Windows Server Technical Preview oder eine höhere Version ausgeführt.  

Sie können mithilfe des Cmdlets [Get-VM] (http://technet.microsoft.com/library/hh848479.aspx), zu überprüfen, ob die Anmeldeinformationen, die Sie verwenden die Hyper-V-Administratorrolle haben und zu sehen, die VMs werden lokal auf dem Host ausgeführt und gebootet.

## Was können Sie mit PowerShell-Direct?

Siehe [PowerShell Direct Ausschnitte] (.. / develop/powershell_snippets.md) für zahlreiche Beispiele zur Verwendung von PowerShell anweisen in Ihrer Umgebung als auch als Tipps und tricks für Hyper-V-Skripten mit PowerShell.


