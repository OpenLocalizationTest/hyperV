ms. ContentId: 1ab7bfe1-da35-4ff1-916f-936fedf536a0
Titel: Setup Windows Container in Azure

# Vorbereitung von Microsoft Azure für Windows-Server-Container

Vor dem Erstellen und Verwalten von Windows-Server-Containern in Azure musst du ein Technical Preview des Windows-2016-Abbild bereitstellen, die mit das Feature Windows Server-Container vorkonfiguriert wurde. 

> Andere erste Schritte Leitfäden:
  * Führen Sie Windows-Server-Container in [eine neue Hyper-V Virtual Machine] (./container_setup.md).
  * Führen Sie Windows-Server-Container in [einer vorhandenen virtuellen Maschine] (./inplace_setup.md)
  * Setup von Windows Server Container [auf eine physische Windows Server Core-Installation] (./inplace_setup.md)

## Starten Sie mit azurblauen Portal
Wenn Sie ein himmelblau-Konto haben, überspringen Sie direkt um [ein Container-Host-VM](#CreateacontainerhostVM) zu erstellen.

1. Gehen Sie zu [azure.com] (https://azure.com), und befolgen Sie die Schritte für eine [Azure Testversion] (https://azure.microsoft.com/en-us/pricing/free-trial/).
2. Melden Sie sich mit Ihrem Microsoft-Konto.
3. Wenn Ihr Konto zu gehen bereit ist, melden Sie sich [Azure Management Portal] (https://portal.azure.com).

## Erstellen Sie einen Container-Host VM

Klicken Sie auf folgenden Link, um den Erstellungsprozess von VM-[neue Windows Server Container Host in Azure] starten (https://portal.azure.com/#gallery/Microsoft.WindowsServer2016TechnicalPreviewwithContainers). 

Sie können auch für das Bild in der Azure-Galerie suchen.

Klicken Sie auf die Schaltfläche 'erstellen'.

! [] (. / media/newazure1.png)

Geben Sie den virtuellen Computer einen Namen, wählen Sie einen Benutzernamen und ein Passwort.

! [] (media/newazure2.png)

Wählen Sie Optional Configuration > Endpunkte > und geben Sie einen HTTP-Endpunkt mit dem privaten und öffentlichen Port 80, wie unten zu sehen. 

! [] (. / media/newazure3.png)

Wählen Sie die Schaltfläche 'erstellen' um den virtuellen Computer Bereitstellung zu starten.

! [] (media/newazure2.png)

Wenn die VM-Bereitstellung abgeschlossen ist, wählen Sie die Schaltfläche verbinden eine RDP-Sitzung mit dem Windows-Server-Container-Host zu starten.

! [] (media/newazure6.png)

Melden Sie sich mit dem Benutzernamen und Kennwort angegeben, während der Assistent zur Erstellung von VM VM. 

! [] (media/newazure7.png) 

## Video-Anleitung

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Configure-Windows-Server-Containers-in-Microsoft-Azure/player" width="800" height="450"  allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>


## Nächste Schritte - starten mithilfe von Containern

Jetzt haben Sie einen Windows-Server-2016 System läuft das Feature Windows Server-Container zu den folgenden Handbüchern zu beginnen, arbeiten mit Windows-Server-Container und Container für Windows-Server Bilder springen. 

[Quick-Start: Windows Server Container und Docker] (. / manage_docker.md)  
[Quick-Start: Windows Server Container und PowerShell] (. / manage_powershell.md) 

-------------------
[Zurück zur Container-Startseite] (.. / containers_welcome.md) [bekannte Probleme bei der aktuellen Version] (.. / about/work_in_progress.md)