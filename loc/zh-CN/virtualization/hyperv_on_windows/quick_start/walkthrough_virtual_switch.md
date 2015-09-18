# 步骤 3: 创建一个虚拟交换机 

一个虚拟交换机允许您创建您的虚拟机的网络连接。  

对于这个示例，我们要创建一个外部开关。外部开关将允许您的虚拟机访问宿主机的网络适配器。 
 
我们还将设置开关允许主机共享此网络适配器。

<!-- We should have a userguide for setting up a private network/virtual network -->

1. 在 HYPER-V 管理器中，单击 * * 虚拟交换机经理 * *。

  ![] (media/virtual_switch_manager1.png)
  
2. 选择 * * 新虚拟网络交换机 * *。

  ![] (media/new_switch.png)
  
3. 选择 * * 外部 * * 和 * * 创建虚拟交换机 * *。

  ![] (media/new_switch_createbutton.png)
  
4. 根据 * * 名称 * *，类型 * * 外 * *。
5. 根据 * * 外部网络 * *，选择正确的网络适配器 (那里可能会只是一种选择)。  
6. 选择 * * 允许管理操作系统共享此网络适配器 * * 并单击 * * 好 * *。 
  
  ![] (media/share_nic.png)  
  
7. 你会得到一条消息，警告您，您的网络可能会断开而创建虚拟交换机。只需单击 * * 是 * *。
  
  ![] (media/network_warning.png)

## 下一步: 
[第 4 步: 创建一个 Windows 虚拟机从一个.iso 文件]() walkthrough_create_vm.md
