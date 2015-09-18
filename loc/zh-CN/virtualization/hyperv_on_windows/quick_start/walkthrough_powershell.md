# 第 8 步: 实验与 Windows PowerShell

现在，你走过了部署 HYPER-V，创建虚拟机和管理这些虚拟机的基础知识，让我们探讨如何可以自动执行许多与 PowerShell 这些活动。

### 返回 HYPER-V 命令的列表

1.	单击 Windows 开始按钮，类型 * * PowerShell * *。
2.	运行以下命令来显示可用 HYPER-V PowerShell 模块 PowerShell 命令可搜索列表。

 ```powershell
get-command –module hyper-v | out-gridview
```
  你得到这样的事情:

  ![] (media\command_grid.png)

3. 若要了解更多关于特定 PowerShell 命令使用获取帮助。例如运行下面的命令将返回有关 ' get vm' 超-V 命令的信息。

  ```powershell
get-help get-vm
```
 输出显示你如何构建命令，必需和可选的参数是什么，你可以使用别名。

 ![] (media\get_help.png)


### 返回虚拟机的列表

使用 get vm' 命令返回虚拟机的列表。

1. 在 PowerShell，请运行以下命令:
 
 ```powershell
get-vm
```
 这将显示类似这样:

 ![] (media\get_vm.png)

2. 若要返回只通电的虚拟机的列表添加 ' get vm' 命令筛选器。可以通过使用 where 对象命令添加筛选器。有关筛选的详细信息请参阅 [使用 Where 对象] (https://technet.microsoft.com/en-us/library/ee177028.aspx) 文件。   

 ```powershell
 get-vm | where {$_.State –eq ‘Running’}
 ```
3.  若要列出所有虚拟机在动力处于关闭状态，请运行以下命令。

 ```powershell
 get-vm | where {$_.State –eq ‘Off’}
 ```

### 启动和关闭虚拟机

1. 若要启动一个特定的虚拟机，虚拟机的名称与运行以下命令:

 ```powershell
 Start-vm –Name virtual machine name
 ```

2. 若要启动所有当前已关闭虚拟机，获取的那些机器列表和管到 ' 启动 vm' 命令列表:

  ```powershell
 get-vm | where {$_.State –eq ‘Off’} | start-vm
 ```
3. 若要关闭所有正在运行的虚拟机，请运行这:
 
  ```powershell
 get-vm | where {$_.State –eq ‘Running’} | stop-vm
 ```

### 创建一个虚拟机检查点

若要创建使用 PowerShell 的一个检查站，选择使用 get vm' 命令的虚拟机和管这对 ' 检查站 vm' 命令。最后给出了检查点名称使用 '-snapshotname'。

 ```powershell
 get-vm -Name VM Name | checkpoint-vm -snapshotname name for snapshot
 ```
例如，下面是一道关卡，DEMOCP 的名称:
 
 ![] (media\POSH_CP2.png)

### 创建一个新的虚拟机

下面的示例演示如何创建一个新的虚拟机在 PowerShell 集成脚本环境 (ISE)。

1. 若要打开 PowerShell ISE 单击开始，键入 * * PowerShell ISE * *。
2. 运行以下代码，以创建一台虚拟机。看到新 VM 命令的 [新 VM] (https://technet.microsoft.com/en-us/library/hh848537.aspx) 文件的详细信息。

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

## 总结和引用

这份文件表明一些简单的步骤，到资源管理器，HYPER-V PowerShell 模块以及一些示例方案。在 HYPER-V PowerShell 模块的详细信息，请参阅 [在 Windows PowerShell 参考 HYPER-V Cmdlet] (https://technet.microsoft.com/%5Clibrary/Hh848559.aspx)。  
 