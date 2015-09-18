ms. ContentId: 4981828d-1a08-4d8c-a99d-874a926a153f
Titel: PowerShell Docker-Vergleich

# PowerShell Docker Vergleich zum Verwalten von Windows-Server-Container

Es gibt viele Möglichkeiten zum Verwalten von Windows-Server-Container mit in-Box Windows-Tools (PowerShell, in dieser Vorschau) und Open-Source-Management-Tools wie Docker.  
Führer, gliedern beide einzeln erhältlich hier:
* [Verwalten Sie Windows-Server-Container mit Docker] (.. / quick_start/manage_docker.md)
* [Verwalten Sie Windows-Server-Container mit PowerShell] (.. / quick_start/manage_powershell.md) 

Diese Seite ist eine genauere Tiefenreferenz Vergleich Docker Werkzeuge und PowerShell-Management-Tools.

## PowerShell für Container im Vergleich zu Hyper-V VMs
Sie können erstellen, ausführen und Interaktion mit Windows-Server-Container mit PowerShell-Cmdlets. 

Wenn Sie Hyper-V-PowerShell verwendet haben, sollte das Design der Cmdlets Sie ziemlich vertraut sein. Viel des Workflows ist ähnlich, wie Sie eine virtuelle Maschine mit dem Hyper-V-Modul schaffen würde. Sie haben anstelle von 'New-VM', 'Get-VM', 'Start-VM', 'Stop-VM', 'New-Container', 'Get-Container', 'Start-Container', 'Stop-Container'. 

## Wie verträgt sich die PowerShell-Verwaltung zu Docker? 
Die Container-PowerShell-Cmdlets verfügbar machen, eine API, die nicht ganz dasselbe wie die Docker ist; Grundsätzlich sind die Cmdlets eine präzisere in Betrieb. 

| Hafenarbeiter Befehl |	PowerShell-Cmdlet |
|----|----|
| 'Hafenarbeiter Ps - a' | "Get-Container" |
| 'Hafenarbeiter Bilder' | 'Get-ContainerImage' |
| 'Hafenarbeiter Rm' | 'Entfernen-Container' |
| 'Hafenarbeiter Rmi' | 'Entfernen-ContainerImage' |
| "Hafenarbeiter erstellen" | Neue-Container |
| 'Hafenarbeiter Commit <container id="">' | ' New-ContainerImage-Container <container>' |
| 'Hafenarbeiter Ladung <tarball>' | 'Import-ContainerImage <AppX package="">' |
| 'Hafenarbeiter speichern' |	'Export-ContainerImage' |
| "Hafenarbeiter Start" |	"Start-Container" |
| 'Stop Hafenarbeiter' |	"Stop-Container" |</AppX></tarball></container></container>

Die PowerShell-Cmdlets sind keine genaue vollkommene Parität, und es gibt eine ganze Reihe von Befehlen, die wir nicht als Ersatz für PowerShell zur Verfügung stellen * (insbesondere 'Hafenarbeiter Build' und 'Hafenarbeiter cp'). Aber was dich heraus springen könnte ist, dass es kein einzelnes Einzeilen-Ersatz für 'Hafenarbeiter ausführen'.

\ * Vorbehalten.

### Aber ich brauche Hafenarbeiter laufen! Was ist los?  
Machen wir ein paar Dinge hier zu einer etwas bekannteren Interaktionsmodell für Benutzer bereitstellen, die ihren Weg zu PowerShell bereits kennen. 

1.	Der Lebenszyklus eines Containers in der PowerShell-Modell ist etwas anders. Im Container PowerShell-Modul setzen wir die präzisere Operationen der 'New-Container' (die einen neuen Container, der angehalten wird erstellt) und "Start-Container".
  
  Zwischen erstellen und starten den Container, können Sie auch den Container Einstellungen konfigurieren; für TP3 ist die nur andere Konfiguration, die wir planen, setzen die Fähigkeit die Netzwerkverbindung für den Container festlegen. 

2.	Derzeit keinen Befehl für die Ausführung innerhalb des Containers auf Start übergeben werden. Jedoch noch kann man eine interaktive PowerShell-Sitzung zu einem laufenden Container mit 'Enter-PSSession - ContainerId <ID of="" a="" running="" container="">', und Sie können Ausführen eines Befehls innerhalb eines laufenden Container mit "Invoke-Command - ContainerId <container id="">- ScriptBlock {Code innerhalb des Containers ausgeführt}' oder ' Invoke-Command - ContainerId <container id="">- FilePath <path to="" script="">'.  
Beide diese Befehle ermöglichen das optionale '-RunAsAdministrator' Flag für hohe Privilège Aktionen.</path> </container> </container> </ID>  


## Vorbehalte und bekannte Probleme
1.  Gerade jetzt, die Container-Cmdlets haben keine Kenntnisse über Container oder Bilder erstellt durch Docker und Docker nicht weiß nichts über Container und Bilder über die PowerShell erstellt. 

2.  Wir haben einiges an Arbeit, die wir tun, um die Endbenutzererfahrung--bessere Fehlermeldungen, bessere Berichterstattung, ungültiges Ereignis Zeichenfolgen und So weiter verbessern möchten. 

## Eine schnelle runthrough
Hier ist ein Spaziergang durch einige gemeinsame Workflows.

Dies setzt voraus, Sie haben ein Betriebssystemabbild Container mit dem Namen "ServerDatacenterCore" installiert und erstellt einen virtuellen Switch mit dem Namen "Virtual Switch" (mit New-VMSwitch).

``` PowerShell
### 1. Enumerating images
# At this point, you can enumerate the images on the system:
Get-ContainerImage

# Get-ContainerImage also accepts filters.
# For example, this will return all container images whose Name starts with S (case-insensitive):
Get-ContainerImage -Name S*

# You can save the results of this to a variable.
# (If you're not familiar with PowerShell, the "$" denotes a variable.)
$baseImage = Get-ContainerImage -Name ServerDatacenterCore
$baseImage

### 2. Creating and enumerating containers
# Now, we can create a new container using this image:
New-Container -Name "MyContainer" -ContainerImage $baseImage -SwitchName "Virtual Switch"

# Now we can enumerate all containers.
Get-Container

# Similarly, we can save this container to a variable:
$container1 = Get-Container -Name "MyContainer"

### 3. Starting containers, interacting with running containers, and stopping containers
# Now let's go ahead and start the container.
Start-Container -Name "MyContainer"

# (We could've also started this container using "Start-Container -Container $container1".)

# With the container now running, let's go ahead and enter an interactive PowerShell session:
Enter-PSSession -ContainerId $container1.Id

# This should eventually bring up a PowerShell prompt from inside the container.
# You can try all the things that you did in the interactive cmd prompt given by "docker run -it".
# For now, just to prove we've been here, we can create a new file:
cd \
mkdir Test
cd Test
echo "hello world" > hello.txt
exit

# Now we should be back in the outside world. Even though we've exited the PowerShell session,
# the container itself is still running, as you can see by printing out the container again:
$container1

# Before we can commit this container to a new image, we need to stop the container.
# Let's do that now.
Stop-Container -Container $container1

### 4. Creating a new container image
# And now let's commit it to a new image.
$image1 = New-ContainerImage -Container $container1 -Publisher Test -Name Image1 -Version 1.0

# Enumerate all the images again, for sanity's sake:
Get-ContainerImage

# Rinse and repeat! Make another container based on the new image.
$container2 = New-Container -Name "MySecondContainer" -ContainerImage $image1 -SwitchName "Virtual Switch"

# (If you like, you can start the second container and verify that the new file
# "\Test\hello.txt" is there as expected.)

### 5. Removing a container
# The first container we created is now stopped. Let's get rid of it:
Remove-Container -Container $container1

# And confirm that it's gone:
Get-Container

### 6. Exporting, removing, and importing images
# For images that aren't the base OS image, we can export them into an .appx package file.
Export-ContainerImage -Image $image1 -Path "C:\exports"
# This should create a .appx file in the C:\exports folder.
# If you've given your image the same publisher, name, and version we used earlier,
# you'd expect the resulting .appx to be named "CN=Test_Image1_1.0.0.0.appx".

# Before we can try importing the image again, we need to remove the image.
# (If you have any running containers that depend on this image, you'll want to stop them first.)
Remove-ContainerImage -Image $image1

# Now let's import the image again:
Import-ContainerImage -Path C:\exports\CN=Test_Image1_1.0.0.0.appx

# We'd previously created a container dependent on this image. You should be able to start it:
Start-Container -Container $container2 
```

### Erstellen Sie Ihr eigenes Beispiel
Sie sehen alle den Container Cmdlets mit "Get-Command - Modul-Container.  Es gibt mehrere andere Cmdlets, die hier nicht beschrieben sind die wir Ihnen über Lernen auf eigene Faust verlassen werde.    
Dies wird nicht **Note** zurück, das "Enter-PSSession" und "Invoke-Command" Cmdlets, die Teil des Kernes PowerShell sind.

Außerdem erhalten Sie Hilfe über alle Cmdlet 'Get-Help [Cmdlet Name]', mit oder äquivalent: '[Cmdlet Name]-?'. 

Ein schöner Weg, um die Syntax zu entdecken ist die PowerShell ISE, die du nicht vor betrachtet haben können wenn Sie PowerShell noch nicht sehr viel verwendet. 

PS: Nur um zu beweisen, dass es getan werden kann, ist hier eine PowerShell-Funktion, die einige der Cmdlets komponiert haben wir bereits in ein Ersatz 'Hafenarbeiter ausführen' gesehen. 

``` PowerShell
function Run-Container ([string]$ContainerImageName, [string]$Name="fancy_name", [switch]$Remove, [switch]$Interactive, [scriptblock]$Command) {
    $image = Get-ContainerImage -Name $ContainerImageName
    $container = New-Container -Name $Name -ContainerImage $image
    Start-Container $container

    if ($Interactive) {
         Start-Process powershell ("-NoExit", "-c", "Enter-PSSession -ContainerId $($container.Id)") -Wait
    } else {
        Invoke-Command -ContainerId $container.Id -ScriptBlock $Command
    }

    Stop-Container $container

    if ($Remove) {
        Remove-Container $container -Force
    }
} 
```

## Hafenarbeiter
Windows Server-Container können mit Docker Befehle verwaltet werden.  Während Windows Container sollten ihre Linux-Pendants vergleichbar und haben das gleiche Management durch Docker erleben, gibt es einige Docker-Befehle, die einfach keinen Sinn mit einem Windows-Container machen. 

In dem Bemühen, die API-Dokumentation Docker nicht duplizieren ist hier ein Link zu ihrer Verwaltungs-APIs. 

Wir sind Dinge verfolgen, die tun und nicht in die Docker-APIs in unserem Zwischenlager-Dokument arbeiten.