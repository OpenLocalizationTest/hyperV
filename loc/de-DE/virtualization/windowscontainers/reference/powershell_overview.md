ms. ContentId: C49DA0E6-2E12-4D51-803A-31B1B5A8F85C
Titel: PowerShell-Referenz


# PowerShell für Container

## Install-ContainerOSImage

** NAME ** Install-ContainerOSImage

** Zusammenfassung ** installiert das angegebene WIM als Container OS Bild für die Verwendung mit Windows Server oder Hyper-V-Containern.


** SYNTAX **  
``` PowerShell  
Install-ContainerOSImage [-WimPath] <String> [-Force] [< CommonParameters >]
```

** Beschreibung ** installiert ein Basis-Image aus einer WIM-Datei in das gemeinsame zentrale Bild speichern für das Feature Windows Server und Hyper-V-Containern.

** PARAMETER **
``` PowerShell
    -WimPath <String>
        A path to the WIM file that will be installed.

        Required?                    true
        Position?                    1
        Default value
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Force [<SwitchParameter>]

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** keine

** Ausgänge ** keine

** ALIASE ** keine

-------------------------- EXAMPLE 1 --------------------------

``` PowerShell
PS C:\>Install-ContainerOSImage c:\baseimage.wim
```

## Deinstallieren-ContainerOSImage

** NAME ** deinstallieren-ContainerOSImage

** Zusammenfassung ** entfernt eine zuvor installierte Container OS-Bild

** SYNTAX **   
```PowerShell
Uninstall-ContainerOSImage [-ImageName] <string> [-Force]  [< CommonParameters >]

Uninstall-ContainerOSImage [-ContainerImage] <Object> [-Force]  [< CommonParameters >]
```

** PARAMETER **  
``` PowerShell
    -ContainerImage <Object>

        Required?                    true
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           ByContainerImage
        Aliases                      None
        Dynamic?                     false

    -Force

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -ImageName <string>

        Required?                    true
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           ByName
        Aliases                      None
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** keine


** Ausgänge ** System.Object

** ALIASE ** keine

## Hinzufügen-ContainerNetworkAdapter ##

** NAME ** hinzufügen-ContainerNetworkAdapter

** Zusammenfassung ** fügen Sie einen neuen Netzwerkadapter an einen vorhandenen Container

** SYNTAX ** 
``` PowerShell  
Add-ContainerNetworkAdapter [-ContainerName] <string[]> [-CimSession <CimSession[]>] [-ComputerName <string[]>]
    [-Credential <pscredential[]>] [-SwitchName <string>] [-Name <string>] [-DynamicMacAddress] [-StaticMacAddress
    <string>] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Add-ContainerNetworkAdapter [-Container] <Container[]> [-SwitchName <string>] [-Name <string>]
    [-DynamicMacAddress] [-StaticMacAddress <string>] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Container <Container[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Object
        Aliases                      None
        Dynamic?                     false

    -ContainerName <string[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -DynamicMacAddress

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Name <string>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Passthru

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -StaticMacAddress <string>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -SwitchName <string>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```


** Eingaben ** System.String\[\] Microsoft.Containers.PowerShell.Objects.Container\[\]


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerNetworkAdapter


** ALIASE ** keine

## Verbinden-ContainerNetworkAdapter

** NAME ** verbinden-ContainerNetworkAdapter

** Zusammenfassung ** Connect Pro Container-Netzwerkkarte mit einem virtuellen switch

** SYNTAX **  
``` PowerShell
    Connect-ContainerNetworkAdapter [-ContainerName] <string[]> [[-Name] <string[]>] [-SwitchName] <string>
    [-Passthru] [-CimSession <CimSession[]>] [-ComputerName <string[]>] [-Credential <pscredential[]>] [-WhatIf]
    [-Confirm]  [<CommonParameters>]

    Connect-ContainerNetworkAdapter [-NetworkAdapter] <ContainerNetworkAdapter[]> [-SwitchName] <string> [-Passthru]
    [-WhatIf] [-Confirm]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name_SwitchName
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name_SwitchName
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -ContainerName <string[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           Name_SwitchName
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name_SwitchName
        Aliases                      None
        Dynamic?                     false

    -Name <string[]>

        Required?                    false
        Position?                    1
        Accept pipeline input?       false
        Parameter set name           Name_SwitchName
        Aliases                      None
        Dynamic?                     false

    -NetworkAdapter <ContainerNetworkAdapter[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Object_SwitchName
        Aliases                      None
        Dynamic?                     false

    -Passthru

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -SwitchName <string>

        Required?                    true
        Position?                    1
        Accept pipeline input?       false
        Parameter set name           Object_SwitchName, Name_SwitchName
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.ContainerNetworkAdapter\[\]


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerNetworkAdapter


** ALIASE ** keine

## Trennen-ContainerNetworkAdapter

** NAME ** trennen-ContainerNetworkAdapter

** Zusammenfassung ** trennen Sie ein Container-Netzwerkkarte aus einen virtuellen switch

** SYNTAX **  
``` PowerShell
    Disconnect-ContainerNetworkAdapter [-ContainerName] <string[]> [[-Name] <string[]>] [-CimSession <CimSession[]>]
    [-ComputerName <string[]>] [-Credential <pscredential[]>] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Disconnect-ContainerNetworkAdapter [-NetworkAdapter] <ContainerNetworkAdapter[]> [-Passthru] [-WhatIf] [-Confirm]
    [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -ContainerName <string[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Name <string[]>

        Required?                    false
        Position?                    1
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -NetworkAdapter <ContainerNetworkAdapter[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           ResourceObject
        Aliases                      None
        Dynamic?                     false

    -Passthru

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.ContainerNetworkAdapter\[\]


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerNetworkAdapter


** ALIASE ** keine

## Export-ContainerImage

** NAME ** Export-ContainerImage

** Zusammenfassung ** Kopie Container Bild aus dem lokalen Speicher

** SYNTAX **  
``` PowerShell
    Export-ContainerImage [[-Name] <string>] [-Path] <string> [[-Version] <version>] [-CimSession <CimSession[]>]
    [-ComputerName <string[]>] [-Credential <pscredential[]>] [-AsJob] [-Passthru] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Export-ContainerImage [-Image] <ContainerImage[]> [-Path] <string> [-AsJob] [-Passthru] [-WhatIf] [-Confirm]
    [<CommonParameters>]
```

** PARAMETER **
``` PowerShell
    -AsJob

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Image <ContainerImage[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Image Object
        Aliases                      None
        Dynamic?                     false

    -Name <string>

        Required?                    false
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Passthru

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Path <string>

        Required?                    true
        Position?                    1
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Publisher <string>

        Required?                    false
        Position?                    1
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Version <version>

        Required?                    false
        Position?                    2
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.ContainerImage\[\]


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerImage


** ALIASE ** keine

## Get-Container

** NAME ** Get-Container

** Zusammenfassung ** Aufzählen von Containern auf dem aktuellen system

** SYNTAX **  
``` PowerShell
    Get-Container [[-Name] <string[]>] [-CimSession <CimSession[]>] [-ComputerName <string[]>] [-Credential
    <pscredential[]>]  [<CommonParameters>]

    Get-Container [[-Id] <guid>] [-CimSession <CimSession[]>] [-ComputerName <string[]>] [-Credential
    <pscredential[]>]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Id, Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Id, Name
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name, Id
        Aliases                      None
        Dynamic?                     false

    -Id <guid>

        Required?                    false
        Position?                    0
        Accept pipeline input?       true (ByValue, ByPropertyName)
        Parameter set name           Id
        Aliases                      None
        Dynamic?                     false

    -Name <string[]>

        Required?                    false
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** System.String\[\] System.Guid


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.Container


** ALIASE ** keine

## Get-ContainerHost

** NAME ** Get-ContainerHost

** Zusammenfassung ** erhalten der Host für den Container-Host-Objekt

** SYNTAX **  
``` PowerShell
    Get-ContainerHost [[-ComputerName] <string[]>] [[-Credential] <pscredential[]>]  [<CommonParameters>]

    Get-ContainerHost [-CimSession] <CimSession[]>  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -CimSession <CimSession[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByPropertyName)
        Parameter set name           CimSession
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           ComputerName
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    1
        Accept pipeline input?       true (ByValue)
        Parameter set name           ComputerName
        Aliases                      None
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Management.Infrastructure.CimSession\[\] System.String\[\] [System.Management.Automation.PSCredential\]


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerHost


** ALIASE ** keine

## Get-ContainerImage

** NAME ** Get-ContainerImage

** Zusammenfassung ** Liste Container Bilder auf dem Container-host

** SYNTAX **  
``` PowerShell
Get-ContainerImage [[-Name] <string>] [[-Publisher] <string>] [[-Version] <version>] [-ChildOf <ContainerImage>]
[-CimSession <CimSession[]>] [-ComputerName <string[]>] [-Credential <pscredential[]>]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -ChildOf <ContainerImage>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Name <string>

        Required?                    false
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Publisher <string>

        Required?                    false
        Position?                    1
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Version <version>

        Required?                    false
        Position?                    2
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** keine


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerImage


** ALIASE ** keine

## Get-ContainerNetworkAdapter

** NAME ** Get-ContainerNetworkAdapter

** Zusammenfassung ** Liste Netzwerkadapter zugeordnete container

** SYNTAX **  
``` PowerShell
    Get-ContainerNetworkAdapter [-ContainerName] <string[]> [[-Name] <string>] [-CimSession <CimSession[]>]
    [-ComputerName <string[]>] [-Credential <pscredential[]>]  [<CommonParameters>]

    Get-ContainerNetworkAdapter [-Container] <Container[]> [[-Name] <string>]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Container <Container[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Object
        Aliases                      None
        Dynamic?                     false

    -ContainerName <string[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Name <string>

        Required?                    false
        Position?                    1
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.Container\[\] System.String\[\]  


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerNetworkAdapter  


** ALIASE ** keine  

## Import-ContainerImage

** NAME ** Import-ContainerImage

** Zusammenfassung ** Import ein Container-Bild, das von einem anderen Computer exportiert wurde

** SYNTAX **  
``` PowerShell
    Import-ContainerImage [-Path] <string> [-AsJob] [-CimSession <CimSession[]>] [-ComputerName <string[]>]
    [-Credential <pscredential[]>] [-WhatIf] [-Confirm]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -AsJob

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Path <string>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** System.String


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerImage


** ALIASE ** keine

## Umzug-ContainerImageRepository

** NAME ** Move-ContainerImageRepository

** Zusammenfassung ** Änderung der Ort wo Container-Bilder gespeichert werden.  Ein Speicherort auf einer lokalen Festplatte müssen sein. 

** SYNTAX **  
``` PowerShell
    Move-ContainerImageRepository [-Path] <string> [-AsJob] [-Passthru] [-CimSession <CimSession[]>] [-ComputerName
    <string[]>] [-Credential <pscredential[]>] [-WhatIf] [-Confirm]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -AsJob

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Passthru

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Path <string>

        Required?                    true
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** keine


** Ausgänge ** Microsoft.HyperV.PowerShell.VMHost


** ALIASE **
Keine

## Neue Container

**Name** neue-Container

** Zusammenfassung ** erstellen einen neuen Container

** SYNTAX **  
``` PowerShell
    New-Container [[-Name] <string>] -ContainerImageName <string> [-ContainerImagePublisher <string>]
    [-ContainerImageVersion <version>] [-CimSession <CimSession[]>] [-ComputerName <string[]>] [-Credential
    <pscredential[]>] [-MemoryStartupBytes <long>] [-SwitchName <string>] [-Path <string>] [-AsJob] [-WhatIf]
    [-Confirm]  [<CommonParameters>]

    New-Container [[-Name] <string>] -ContainerImage <ContainerImage> [-MemoryStartupBytes <long>] [-SwitchName
    <string>] [-Path <string>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -AsJob

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Image Identifiers
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Image Identifiers
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -ContainerImage <ContainerImage>

        Required?                    true
        Position?                    Named
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Image Object
        Aliases                      None
        Dynamic?                     false

    -ContainerImageName <string>

        Required?                    true
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Image Identifiers
        Aliases                      None
        Dynamic?                     false

    -ContainerImagePublisher <string>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Image Identifiers
        Aliases                      None
        Dynamic?                     false

    -ContainerImageVersion <version>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Image Identifiers
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Image Identifiers
        Aliases                      None
        Dynamic?                     false

    -MemoryStartupBytes <long>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Name <string>

        Required?                    false
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           Container Image Identifiers, Container Image Object
        Aliases                      None
        Dynamic?                     false

    -Path <string>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -SwitchName <string>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.ContainerImage


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.Container


** ALIASE ** keine

## Neue ContainerImage

**Name** neue ContainerImage

** Zusammenfassung ** erstellen ein neuer Container Bild aus einen vorhandenen container

** SYNTAX **  
``` PowerShell
    New-ContainerImage [-ContainerName] <string> [-Name] <string> [-Publisher] <string> [-Version] <version>
    [-CimSession <CimSession[]>] [-ComputerName <string[]>] [-Credential <pscredential[]>] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    New-ContainerImage [-Container] <Container> [-Name] <string> [-Publisher] <string> [-Version] <version> [-WhatIf]
    [-Confirm]  [<CommonParameters>]

    New-ContainerImage [-ContainerId] <guid> [-Name] <string> [-Publisher] <string> [-Version] <version> [-CimSession
    <CimSession[]>] [-ComputerName <string[]>] [-Credential <pscredential[]>] [-WhatIf] [-Confirm]
    [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Id, Container Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name, Container Id
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Container <Container>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Object
        Aliases                      None
        Dynamic?                     false

    -ContainerId <guid>

        Required?                    true
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           Container Id
        Aliases                      None
        Dynamic?                     false

    -ContainerName <string>

        Required?                    true
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name, Container Id
        Aliases                      None
        Dynamic?                     false

    -Name <string>

        Required?                    true
        Position?                    1
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Publisher <string>

        Required?                    true
        Position?                    2
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Version <version>

        Required?                    true
        Position?                    3
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.Container


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerImage


** ALIASE ** keine

## Entfernen-Container

** NAME ** entfernen-Container

** Zusammenfassung ** Entfernen eines vorhandenen Containers aus dem System

** SYNTAX **  
``` PowerShell
    Remove-Container [-Name] <string[]> [-CimSession <CimSession[]>] [-ComputerName <string[]>] [-Credential
    <pscredential[]>] [-Force] [-AsJob] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Remove-Container [-Container] <Container[]> [-Force] [-AsJob] [-Passthru] [-WhatIf] [-Confirm]
    [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -AsJob

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Container <Container[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Object
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Force

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Name <string[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Passthru

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** System.String\[\] Microsoft.Containers.PowerShell.Objects.Container\[\]


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.Container


** ALIASE ** keine

## Entfernen-ContainerImage

** NAME ** entfernen-ContainerImage

** Zusammenfassung ** entfernen ein Containers image vom Host-container

** SYNTAX **  
``` PowerShell
    Remove-ContainerImage [[-Name] <string>] [[-Publisher] <string>] [[-Version] <version>] [-CimSession
    <CimSession[]>] [-ComputerName <string[]>] [-Credential <pscredential[]>] [-Force] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Remove-ContainerImage [-Image] <ContainerImage> [-Force] [-WhatIf] [-Confirm]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Force

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -Image <ContainerImage>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Image Object
        Aliases                      None
        Dynamic?                     false

    -Name <string>

        Required?                    false
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Publisher <string>

        Required?                    false
        Position?                    1
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Version <version>

        Required?                    false
        Position?                    2
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.ContainerImage


** Ausgänge ** System.Object

** ALIASE ** keine

## Entfernen-ContainerNetworkAdapter

** NAME ** entfernen-ContainerNetworkAdapter

** Zusammenfassung ** entfernen Sie einen Netzwerkadapter aus einem Container

** SYNTAX **  
``` PowerShell
    Remove-ContainerNetworkAdapter [-ContainerName] <string[]> [-CimSession <CimSession[]>] [-ComputerName <string[]>]
    [-Credential <pscredential[]>] [-Name <string>] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Remove-ContainerNetworkAdapter [-NetworkAdapter] <ContainerNetworkAdapter[]> [-Passthru] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Remove-ContainerNetworkAdapter [-Container] <Container[]> [-Name <string>] [-Passthru] [-WhatIf] [-Confirm]
    [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Container <Container[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Object
        Aliases                      None
        Dynamic?                     false

    -ContainerName <string[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Name <string>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name, Container Object
        Aliases                      None
        Dynamic?                     false

    -NetworkAdapter <ContainerNetworkAdapter[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           ResourceObject
        Aliases                      None
        Dynamic?                     false

    -Passthru

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.ContainerNetworkAdapter\[\] System.String\[\] Microsoft.Containers.PowerShell.Objects.Container\[\]


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerNetworkAdapter


** ALIASE ** keine

## Satz-ContainerNetworkAdapter

** NAME ** Set-ContainerNetworkAdapter

** Zusammenfassung ** legen Sie der MAC-Adresse auf einem Netzwerkadapter in einem container

** SYNTAX **  
``` PowerShell
    Set-ContainerNetworkAdapter [-ContainerName] <string> [-CimSession <CimSession[]>] [-ComputerName <string[]>]
    [-Credential <pscredential[]>] [-Name <string>] [-DynamicMacAddress] [-StaticMacAddress <string>] [-Passthru]
    [-WhatIf] [-Confirm]  [<CommonParameters>]

    Set-ContainerNetworkAdapter [-NetworkAdapter] <ContainerNetworkAdapter> [-DynamicMacAddress] [-StaticMacAddress
    <string>] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Set-ContainerNetworkAdapter [-Container] <Container> [-Name <string>] [-DynamicMacAddress] [-StaticMacAddress
    <string>] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Container <Container>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Object
        Aliases                      None
        Dynamic?                     false

    -ContainerName <string>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Name
        Aliases                      None
        Dynamic?                     false

    -DynamicMacAddress

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           ResourceObject, Container Object, Container Name
        Aliases                      None
        Dynamic?                     false

    -Name <string>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Container Object, Container Name
        Aliases                      None
        Dynamic?                     false

    -NetworkAdapter <ContainerNetworkAdapter>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           ResourceObject
        Aliases                      None
        Dynamic?                     false

    -Passthru

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -StaticMacAddress <string>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           ResourceObject, Container Object, Container Name
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** System.String Microsoft.Containers.PowerShell.Objects.ContainerNetworkAdapter Microsoft.Containers.PowerShell.Objects.Container


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerNetworkAdapter


** ALIASE ** keine

## Start-Container

** NAME ** Start-Container

** Zusammenfassung ** Start pro container

** SYNTAX **  
``` PowerShell
    Start-Container [-Name] <string[]> [-CimSession <CimSession[]>] [-ComputerName <string[]>] [-Credential
    <pscredential[]>] [-AsJob] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Start-Container [-Container] <Container[]> [-AsJob] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -AsJob

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Container <Container[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Object
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Name <string[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Passthru

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.Container\[\] System.String\[\]


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.Container


** ALIASE ** keine

## Stop-Container

** NAME ** Stop-Container

** Zusammenfassung ** Stop a container

** SYNTAX **  
``` PowerShell
    Stop-Container [-Name] <string[]> [-CimSession <CimSession[]>] [-ComputerName <string[]>] [-Credential
    <pscredential[]>] [-TurnOff] [-AsJob] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Stop-Container [-Container] <Container[]> [-TurnOff] [-AsJob] [-Passthru] [-WhatIf] [-Confirm]
    [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -AsJob

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Container <Container[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Object
        Aliases                      None
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Name <string[]>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Passthru

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -TurnOff

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.Container\[\] System.String\[\]


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.Container


** ALIASE ** keine

## Test-ContainerImage

** NAME ** Test-ContainerImage

** Zusammenfassung ** validieren ein Containers Bild auf dem Hostsystem container

** SYNTAX **  
``` PowerShell
    Test-ContainerImage [[-Name] <string>] [[-Publisher] <string>] [[-Version] <version>] [-CimSession <CimSession[]>]
    [-ComputerName <string[]>] [-Credential <pscredential[]>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Test-ContainerImage [-Image] <ContainerImage> [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]
```

** PARAMETER **  
``` PowerShell
    -AsJob

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      None
        Dynamic?                     false

    -CimSession <CimSession[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -ComputerName <string[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Confirm

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      cf
        Dynamic?                     false

    -Credential <pscredential[]>

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Image <ContainerImage>

        Required?                    true
        Position?                    0
        Accept pipeline input?       true (ByValue)
        Parameter set name           Container Image Object
        Aliases                      None
        Dynamic?                     false

    -Name <string>

        Required?                    false
        Position?                    0
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Publisher <string>

        Required?                    false
        Position?                    1
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -Version <version>

        Required?                    false
        Position?                    2
        Accept pipeline input?       false
        Parameter set name           Name
        Aliases                      None
        Dynamic?                     false

    -WhatIf

        Required?                    false
        Position?                    Named
        Accept pipeline input?       false
        Parameter set name           (All)
        Aliases                      wi
        Dynamic?                     false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
```

** Eingaben ** Microsoft.Containers.PowerShell.Objects.ContainerImage


** Ausgänge ** Microsoft.Containers.PowerShell.Objects.ContainerImageReport


** ALIASE ** keine