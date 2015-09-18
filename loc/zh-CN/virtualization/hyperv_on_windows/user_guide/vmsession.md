# 管理 Windows PowerShell Direct 与 #
你可以使用 PowerShell Direct 从 Windows 10 或 Windows 服务器技术预览 HYPER-V 主机远程管理 Windows 10 或 Windows 服务器技术预览虚拟机。PowerShell 直接允许 PowerShell 无论网络配置或远程管理设置 HYPER-V 主机上的 virtual machine 或虚拟机内部的管理。

有两种方法运行 PowerShell 直接:  
* 创建和退出使用 PSSession cmdlet PowerShell 直接会话
* 与调用命令 cmdlet 运行脚本或命令

如果您管理的旧的虚拟机，使用虚拟机连接 (VMConnect) 或 [配置虚拟机的虚拟网络] (http://technet.microsoft.com/library/cc816585.aspx)。 

## 创建和退出使用 PSSession cmdlet PowerShell 直接会话
1. 在 HYPER-V 主机上，以管理员身份打开 Windows PowerShell。

3. 运行以下命令以创建会话所使用的虚拟机的名称或 GUID 之一:  
``` PowerShell
Enter-PSSession -VMName VMName
Enter-PSSession -VMGUID VMGUID
```

4. 运行您需要的任何命令。
5. 当你完成后时，请运行以下命令以关闭会话:  
``` PowerShell
Exit-PSSession 
``` 

> 注意: 如果你是会话不会连接，请确保您使用凭据您要连接到 — — 不是 HYPER-V 主机的虚拟机。

要了解更多有关这些 cmdlet，见 [enter 键-PSSession] (http://technet.microsoft.com/library/hh849707.aspx) 和 [退出-PSSession] (http://technet.microsoft.com/library/hh849743.aspx)。 

## 与调用命令 cmdlet 运行脚本或命令

您可以使用 [调用命令] (http://technet.microsoft.com/library/hh849719.aspx) cmdlet 在虚拟机上运行一组预先确定的命令。

 ``` PowerShell
 Invoke-Command -VMName PSTest -FilePath C:\script\foo.ps1 
 ```

若要运行一个命令，请使用 * *-简言之 * * 参数:

 ``` PowerShell
 Invoke-Command -VMName PSTest -ScriptBlock { cmdlet } 
 ```

## 有什么要求，使用 PowerShell 直接?
在虚拟机上创建 PowerShell 直接会话
* 虚拟机必须运行在主机上的本地和引导。 
* 您必须登录到主机计算机，作为 HYPER-V 管理员。
* 您必须提供有效的用户凭据为该虚拟机。
* 主机操作系统必须运行 Windows 10、 Windows 服务器技术预览或更高版本。  
* 虚拟机必须运行 Windows 10、 Windows 服务器技术预览或更高版本。  

检查您正在使用的凭据具有 HYPER-V 管理员角色，看看哪个虚拟机在主机上本地运行和启动，您可以使用 [Get-VM] (http://technet.microsoft.com/library/hh848479.aspx) cmdlet。

## 你可以用 PowerShell 直接做什么?

参阅 [PowerShell 直接片段] (.../ develop/powershell_snippets.md) 的许多示例说明了如何在您的环境以及使用 PowerShell 直接作为提示和技巧写作与 PowerShell HYPER-V 脚本。


