# Schritt 8: Experimentieren Sie mit Windows PowerShell

Nun, da Sie durch die Grundlagen der Bereitstellung von Hyper-V, virtuelle Maschinen erstellen und verwalten diese virtuellen Computer gegangen sind, lassen Sie uns, wie Sie viele dieser Aktivitäten mit PowerShell automatisieren können.

### Zurückgeben einer Liste der Hyper-V-Kommandos

1.	Klicken Sie auf die Windows-Schaltfläche Start, Typ ** PowerShell **.
2.	Führen Sie den folgenden Befehl, um eine durchsuchbare Liste der PowerShell-Befehle zur Verfügung, mit dem Hyper-V-PowerShell-Modul anzuzeigen.

 ```powershell
get-command –module hyper-v | out-gridview
```
  Sie erhalten etwa folgendermaßen:

  ! [] (media\command_grid.png)

3. Erfahren Sie verwenden mehr über einen bestimmten PowerShell-Befehl, "Get-Help". Zum Beispiel den folgenden Befehl ausführen, gibt Informationen über den Hyper-V-Befehl "Get-Vm" zurück.

  ```powershell
get-help get-vm
```
 Die Ausgabe zeigt, wie strukturieren den Befehl, was sind die erforderlichen und optionalen Parametern und der Aliase, die Sie verwenden können.

 ! [] (media\get_help.png)


### Zurückgeben einer Liste der virtuellen Maschinen

Verwenden Sie den Befehl "Get-Vm", eine Liste der virtuellen Computer zurückgeben.

1. Führen Sie den folgenden Befehl in die PowerShell:
 
 ```powershell
get-vm
```
 Dies zeigt in etwa wie folgt:

 ! [] (media\get_vm.png)

2. Rückkehren eine Liste nur eingeschaltet virtueller Maschinen fügen einen Filter auf den Befehl "Get-Vm". Mit den Befehl Where-Object kann ein Filter hinzugefügt werden. Weitere Informationen zum Filtern finden Sie unter [Using Where-Object] (https://technet.microsoft.com/en-us/library/ee177028.aspx)-Dokumentation.   

 ```powershell
 get-vm | where {$_.State –eq ‘Running’}
 ```
3.  Listen Sie alle virtuellen Computer in einem angetriebenen off-Zustand, den folgenden Befehl ausführen. 

 ```powershell
 get-vm | where {$_.State –eq ‘Off’}
 ```

### Starten und Herunterfahren der virtuellen Maschinen

1. Um einen bestimmten virtuellen Computer zu starten, führen Sie den folgenden Befehl mit Namen der virtuellen Maschine:

 ```powershell
 Start-vm –Name virtual machine name
 ```

2. Um alle derzeit ausgeschaltet von virtuellen Maschinen starten, erhalten Sie eine Liste mit diesen Maschinen und leiten Sie die Liste auf den Befehl 'Start-Vm':

  ```powershell
 get-vm | where {$_.State –eq ‘Off’} | start-vm
 ```
3. Führen Sie diese Schritte aus, um alle ausgeführten virtuellen Computer herunterzufahren:
 
  ```powershell
 get-vm | where {$_.State –eq ‘Running’} | stop-vm
 ```

### Erstellen Sie einen VM-checkpoint

Um einen Checkpoint mit PowerShell zu erstellen, wählen Sie die virtuelle Maschine mit dem Befehl "Get-Vm" und leiten Sie dies auf den Befehl 'Prüfpunkt-Vm'. Schließlich geben dem Checkpoint einen Namen mit '-Snapshotname'. 

 ```powershell
 get-vm -Name VM Name | checkpoint-vm -snapshotname name for snapshot
 ```
Hier ist beispielsweise ein Prüfpunkt mit dem Namen DEMOCP:
 
 ! [] (media\POSH_CP2.png)

### Erstellen einer neuen virtuellen Maschine

Das folgende Beispiel veranschaulicht das Erstellen Sie einer neuen virtuelle Maschine in der PowerShell Integrated Scripting Environment (ISE). 

1. Öffnen Sie die PowerShell ISE klicken Sie auf Start, geben Sie ** PowerShell ISE **.
2. Führen Sie den folgenden Code zum Erstellen einer virtuellen Maschine. Siehe [New-VM] (https://technet.microsoft.com/en-us/library/hh848537.aspx) Dokumentation ausführliche Informationen über den Befehl New-VM.

  ```powershell
 $VMName = "VMNAME"

 $VM = @{
     Name = $VMName 
     MemoryStartupBytes = 2147483648
     Generation = 2
     NewVHDPath = "C:\Virtual Machines\$VMName\$VMName.vhdx"
     NewVHDSizeBytes = 53687091200
     BootDevice = "VHD"
     Path = "C:\Virtual Machines\$VMName "
     SwitchName = (get-vmswitch).Name[0]
 }

 New-VM @VM
  ```

## Einpacken und Verweise

Dieses Dokument hat einige einfache Schritte, Explorer das Hyper-V-PowerShell-Modul sowie einige Beispielszenarien gezeigt. Weitere Informationen über die Hyper-V-PowerShell-Module finden Sie unter [Hyper-V-Cmdlets in Windows PowerShell-Referenz] (https://technet.microsoft.com/%5Clibrary/Hh848559.aspx).  
 