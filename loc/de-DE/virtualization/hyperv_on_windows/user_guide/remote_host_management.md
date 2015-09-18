# Verwalten von Remote-Hyper-V-Hosts mit Hyper-V-Manager #

Hyper-V Manager bietet Tools für die Diagnose und Verwaltung von Ihrem lokalen Hyper-V-Host und eine kleine Anzahl von entfernten Rechnern. 

Zum Verbinden mit Hyper-V-Hosts im Hyper-V-Manager sicherstellen ** Hyper-V Manager ** ist im linken Bereich ausgewählt und wählen Sie dann ** verbinden mit Server... ** im rechten Fensterbereich.

! [] (Medien/HyperVManager-ConnectToHost.png)

## Unterstützte Kombinationen der Hyper-V-Host mit Hyper-V Manager
Hyper-V-Manager in Windows 10 können Sie verwalten:
* Windows 10
* 8.1 für Windows und Windows Server 2012 R2 Hyper-V-hosts
* Windows 8 und Windows 2012 Hyper-V-hosts

Hyper-V-Manager in Windows 8.1 und Windows Server 2012 R2 können Sie verwalten:
* 8.1 für Windows und Windows Server 2012 R2 Hyper-V-hosts
* Windows 8 und Windows 2012 Hyper-V-hosts

> ** Hinweis: ** nicht alle Funktionen von Hyper-V Manager funktioniert für alle Host-Versionen.

## Verwalten von "localhost" ##
Um Hyper-V Manager als Hyper-V Host "localhost" hinzuzufügen, wählen Sie ** lokale Computer ** in der ** wählen Sie Computer ** Dialog-Box.

! [] (Medien/HyperVManager-ConnectToLocalHost.png)

Wenn keine Verbindung hergestellt werden kann:
*  Stellen Sie sicher, dass die Hyper-V-Serverrolle aktiviert ist.  Abschnitt [Exemplarische Vorgehensweise für die Überprüfung der Kompatibilität] (.. / quick_start/walkthrough_compatibility.md).
*  Bestätigen Sie, dass Ihr Benutzerkonto in der Hyper-V-Administratorgruppe ist.


## Hyper-V-Hosts in Ihrer Domäne zu verwalten ##

Wählen Sie zum Hinzufügen eines Hyper-V-Remotehosts, um Hyper-V Manager ** ein weiterer Computer ** in der ** wählen Sie Computer ** Dialog Feld und geben Sie des remote-Hosts Hostname, NetBIOS- oder FQDN in das Textfeld ein.

! [] (Medien/HyperVManager-ConnectToRemoteHost.png)

Stark erweitert Windows 10 möglichen Kombinationen der Remoteverbindung Typen.  
Jetzt können Sie auf einen entfernten Windows-10 oder später Host verwenden entweder den Hostnamen oder die IP-Adresse verbinden.   

Um remote Hyper-V-Hosts zu verwalten, muss die Remoteverwaltung auf beiden Computern aktiviert sein.

Sie erreichen dies durch 'Systemeigenschaften-> Remote-Management-Einstellungen' oder durch den folgenden PowerShell-Befehl als Administrator ausführen:  

``` PowerShell
winrm quickconfig
```

Wenn Ihre aktuellen Benutzerkonto ein Hyper-V-Administratorkonto auf dem entfernten Host entspricht, gehen Sie voran und drücken Sie ** OK ** zu verbinden.  

Dies ist der einzige unterstützte Weg zu einen Remotehost in Hyper-V-Manager in Windows 8 oder Windows 8.1 verwalten.


### Verbinden Sie mit dem Remotehost als anderer Benutzer
In Windows 10 wenn Sie nicht mit dem richtigen Benutzer-Account für die remote-Host ausführen, können Sie als ein anderer Benutzer mit alternativen Anmeldeinformationen verbinden.

Um Anmeldeinformationen für den Hyper-V-Remotehost anzugeben, wählen Sie ** Connect als ein anderer Benutzer: ** in der ** wählen Sie Computer ** Dialog box wählen Sie ** Benutzer setzen **.

! [] (Medien/HyperVManager-ConnectToRemoteHostAltCreds.png)

> Hinweis: Es ist sehr einfach zu vergessen, den Benutzer und klicken Sie auf OK mit Benutzer nicht angegeben. 

### Verbinden Sie mit dem remote-Host mit IP-Adresse
Manchmal ist es einfacher, eine Verbindung mit IP-Adresse als Host-Namen. 

Um die Verbindung mit IP-Adresse, IP-Adresse in der ** ein weiterer Computer ** Text-Feld.


## Verwalten von Hyper-V-Hosts außerhalb Ihrer Domäne (oder ohne Domäne) ##
<!--Assuming this isn't done yet...again needs context.-->
Local Hyper-V Host:
1.	Enable-PSRemoting
Came back with netowork set to public.
Ran
Set-NetConnectionProfile -Name "name" -NetworkCategory private
2. Set-Item WSMan:\localhost\Client\TrustedHosts * -Force
3. Enable-WSManCredSSP -Role client -DelegateComputer *

Für nur Workgroup:
1. (sollte erfolgen) Computer → Policy\Administrative Templates\System\Credentials Delegation\Allow delegieren frisch Anmeldeinformationen festlegen auf aktiviert, und fügen Sie WSMAN / *]. 

2. Policy\Administrative Templates\System\Credentials Delegation\Allow delegieren frisch Computeranmeldeinformationen mit Server nur NTLM-Authentifizierung → festlegen auf aktiviert, und fügen Sie WSMAN / * Liste der Computer, aktivieren Sie das Kontrollkästchen für verketten OS Defaults mit Eingang oben
3. Computer Policy\Administrative Vorlagen\Windows-Komponenten\Windows-Remoteverwaltung (WinRM) \WinRM Client\Allow CredSSP Authentifizierung → festlegen auf aktiviert

Remote-Hyper-V-Host:
1. Deaktiviert die Firewall :)
2. Enable-PSRemoting
3. Mengenelement WSMan:\localhost\Client\TrustedHosts *-Kraft
Also ist die Demo nur Anweisungen habe, die ich verwendet.  Ersetzen * und deaktivieren Sie die Firewall mit einem einzelnen Computer und lassen Credssp und WinRM durch


