ms. ContentId: 3fdd690d-4259-4066-8781-360bb0554512
Titel: Running Apps in Windows-Containern

# Anwendung Kompatibilität in Windows Server-Container

Ist etwas nicht auf dieser Liste?  Lassen Sie uns wissen, was schlägt fehl, und gelingt es in Ihrer Umgebung über [Foren] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).

## Welche Anwendungen laufen in einem Windows-Server-Container

Wir haben versucht, die folgenden Anwendungen in einem Windows Server-Container ausgeführt.  Diese Ergebnisse können nicht garantieren, dass die Anwendung funktioniert. 

| ** Name ** | ** Version ** | ** Funktioniert es? ** | ** Kommentar ** |
|:-----|:-----|:-----|:-----|
| .NET | 3.5 | Nein | Nicht richtig installiert | 
| .NET | 4.6 | Ja | Im Basisabbild enthalten | 
| .NET CLR | 5 Beta 6 | Ja | Beide, X 64 und X 86 | 
| Aktive Python | 3.4.1 | Ja ||
| Apache CouchDB | 1.6.1 | Nein ||
| Apache HTTPD | 2.4 | Ja ||
| Apache Tomcat | 8.0.24 X 64 | Ja ||
| ASP.NET | 3.5 | Nein ||
| ASP.NET | 4.5 | Nein ||
| ASP.NET | 5 Beta 6 | Ja | Beide, X 64 und X 86 |
| Erlang/OTP | 18,0 | Nein ||
| FileZilla FTP-Server | 0,9 | Ja | Durch eine RDP-Sitzung in den Container installiert werden muss | 
| Gehen Programmierung Sprache | 1.4.2 | Ja ||
| Internet-Informationsdienst | 10.0 | Ja ||
| Java | 1.8.0_51 | Ja | Verwenden Sie die Serverversion. Die Clientversion installiert nicht richtig |
| Mole | 9.3 | Teilweise | Demo-Base fehl laufen |
| MineCraft Server | 1.8.5 | Ja ||
| MongoDB | 3.0.4 | Ja ||
| MySQL | 5.6.26 | Ja ||
| NGinx | 1.9.3 | Ja ||
| Node.js | 0.12.6 | Teilweise | Ausführen von Knoten mit Js-Dateien arbeiten. NPM nicht Pakete herunterladen. Interaktives Ausführen von Knoten funktioniert nicht richtig. |
| PHP | 5.6.11 | Teilweise | Mit Apache funktioniert IIS über FastCGI derzeit nicht. |
| PostgreSQL | 9.4.4 | Ja ||
| Python | 3.4.3 | Ja ||
| R | 3.2.1 | Nein ||
| RabbitMQ | 3.5.x | Ja | Durch eine RDP-Sitzung in den Container installiert werden muss |
| Redis | 2.8.2101 | Ja ||
| Ruby | 2.2.2 | Ja | Beide, X 64 und X 86 | 
| Ruby on Rails | 4.2.3 | Ja ||
| SQLite | 3.8.11.1 | Ja ||
| SQL Server Express | 2014-LocalDB | Nein |  |
| Sysinternals-Tools | * | Ja | Nur versucht, solche, die keine GUI.  

## Welche optionalen Windows-Funktionen kann ich installieren?

Die folgenden optionalen Windows-Funktionen wurden bestätigt, als in der Lage zu installieren. 

* AD-Zertifikat
* MDE-Cert-Authority
* Datei-Services
 * FS-FileServer
 * FS-VSS-Agent
* DirectAccess-VPN
* Weiterleitung
* Remote-Desktop-Services
* VolumeActivation
* Web-Server
* Web-WebServer
* Web-Common-Http
* Web-Standard-Doc
* Browser-Dir
* Web-Http-Fehler
* Web-Static-Content
* Web-Http-Redirect
* Web-DAV-Publishing
* Web-Gesundheit
* Web-Http-Protokollierung
* Web-Custom-Logging
* Web-Log-Libraries
* Web-ODBC-Protokollierung
* Web-Anfrage-Monitor
* Web-Performance
* Web-Stat-Komprimierung
* Web-Dyn-Komprimierung
* Web-Security
* Web-Filter
* Web-Basic-Auth
* Web-CertProvider
* Web-Client-Auth
* Web-Digest-Auth
* Web-Cert-Auth
* Web-IP-Security
* Web-Url-Auth
* Web-Windows-Auth
* Web-App-Dev
* Web-AppInit
* Web-CGI
* Web-ISAPI-Ext
* Web-ISAPI-Filter
* Web-beinhaltet
* Web-WebSockets
* Web-Mgmt-Compat
* Web-Metabase
* BitLocker
* EnhancedStorage
* GRUPPENRICHTLINIEN-VERWALTUNGSKONSOLE
* Isoliert-UserMode
* Server-Medien-Stiftung
* MSMQ-DCOM
* Mehrpunkt-Connector-Feature
* qWave
* RDC
* RSAT-Feature-Tools-BitLocker
* RSAT-Cluster-PowerShell
* RSAT-Cluster-AutomationServer
* RSAT-Cluster-CmdInterface
* RSAT-geschirmt-VM-Tools
* AD-RSAT-Tools
* RSAT-AD-PowerShell
* RSAT-ADDS
* RSAT-AD-AdminCenter
* RSAT-fügt-Tools
* RSAT-ADLDS
* Hyper-V-PowerShell
* UpdateServices-API
* RSAT-NetworkController
* Windows-Stoff-Tools
* RSAT-HostGuardianService
* FS-SMBBW
* Speicher-Replik
* Telnet-Client
* WAR
 * WAR-Prozess-Modell
 * WAR-Config-APIs
* Windows-Server-Backup
* Migration

Ist etwas nicht auf dieser Liste?  Lassen Sie uns wissen, was schlägt fehl, und gelingt es in Ihrer Umgebung über [Foren] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).