# Schritt 3: Erstellen Sie einen virtuellen switch 

Ein virtueller Switch können Sie eine Netzwerkverbindung für den virtuellen Computer erstellen.   

In diesem Beispiel wollen wir einen externen Schalter zu erstellen.  Der externe Schalter können Ihre virtuelle Maschine auf den Host zugreifen Netzwerkadapter des Computers.  
 
Wir werden auch die Umstellung auf dem Host diese Netzwerkkarte Teilen ermöglichen festlegen. 

<!-- We should have a userguide for setting up a private network/virtual network -->

1. Klicken Sie im Hyper-V-Manager ** Virtual Switch Manager **.

  ! [] (media/virtual_switch_manager1.png)
  
2. Wählen Sie ** neues virtuelles Netzwerk Switch **.

  ! [] (media/new_switch.png)
  
3. Wählen Sie ** externe ** und ** Erstellen virtueller Switch **.

  ! [] (media/new_switch_createbutton.png)
  
4. Unter ** Name **, Typ ** externe **.
5. Unter ** externe Netzwerk **, wählen Sie den richtigen Netzwerk-Adapter (es wird wahrscheinlich nur eine Option sein).  
6. Wählen Sie ** Verwaltungsbetriebssystem teilen diese Netzwerk-Adapter **, und klicken Sie auf erlauben ** OK **. 
  
  ! [] (media/share_nic.png)  
  
7. Sie erhalten eine Warnung, dass Ihr Netzwerk trennen könnte, während der virtuelle Switch erstellt wird. Klicken Sie einfach ** ja **. 
  
  ! [] (media/network_warning.png)

## Nächster Schritt: 
[Schritt 4: Erstellen eine virtuellen Windows-Maschine aus einer .iso-Datei] (walkthrough_create_vm.md)
