# Schritt 2: Installieren von Hyper-V unter Windows 10

Hyper-V kann installiert werden [Programme und Features](#UsingProgramsandFeatures) oder [Windows Powershell](#UsingPowerShell).

## Programme und Funktionen
1. Mit der rechten Maustaste die ** Windows ** und klicken dann Sie auf ** Programme und Features **.

  ! [] (media\programs_and_features.png)
  
2. Klicken ** Windows-Funktionen ein- oder ausschalten **.

3. Wählen Sie ** Hyper-V **, klicken ** OK **

  ! [] (Media\hyper-v_feature_selected.png)
  
4. Wenn die Installation abgeschlossen ist, müssen Sie den Computer neu starten.

  ! [] (media\restart.png)
  
## Mithilfe von PowerShell
Weitere Informationen finden Sie in der PowerShell Hilfe [Enable-WindowsOptionalFeature] (https://technet.microsoft.com/library/hh852172.aspx).

1. Klicken Sie auf die ** Windows ** Knopf und Suche nach ** Windows PowerShell **.  
2. Mit einem Rechtsklick ** Windows PowerShell ** und klicken Sie dann auf ** führen Sie als Administrator **.  
3. Geben Sie Folgendes an der Eingabeaufforderung den Windows Powerhshell, und drücken Sie dann die ** ** Enter-Taste:  
``` PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
``` 
4. Wenn die Installation abgeschlossen ist, starten Sie den Computer. 

## Woher weiß ich die Hyper-V richtig installiert?
Nach dem Neustart Ihres Computer-Start der Hyper-V-Manager-Tool. 

1. Klicken Sie auf die ** Windows ** Knopf und Typ ** Hyper-V **.
2. Klicken Sie auf ** Hyper-V Manager ** in der Liste.
3. Die Hyper-V-Manager-Anwendung sollte beginnen.


## Nächsten Schritt 
[Schritt 3: Erstellen Sie einen virtuellen Switch] (walkthrough_virtual_switch.md) 