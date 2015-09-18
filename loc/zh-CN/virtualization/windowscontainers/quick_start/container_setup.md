ms。ContentId: 71a03c62-50fd-48dc-9296-4d285027a96a
标题: 本地的虚拟机中安装 Windows 容器

# Windows 服务器技术预览准备 Windows 服务器容器

为创建和管理 Windows 服务器容器，必须编写 Windows 服务器 2016年技术预览环境。

> 其他入门指南:
  * [Azure] (./azure_setup.md) 中运行 Windows 服务器容器。
  * 在 [现有的虚拟机] 中运行 Windows 服务器容器 (./inplace_setup.md)。
  * [关于物理的 Windows 服务器核心安装] 安装 Windows 服务器容器 (./inplace_setup.md)。

  * * 请阅读安装容器 OS 映像之前: * * ("许可条款") Microsoft Windows 服务器预发行软件的许可条款适用于您使用 Microsoft Windows 容器 OS 映像补充 ("辅助软件)。下载和使用辅助软件，您同意许可条款，且你不可能使用它，如果你还不接受许可协议条款。  

* 系统运行 Windows 10 / 2 或更高版本的 Windows 服务器技术预览版。
* HYPER-V 角色启用 ([见说明] (https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install#UsingPowerShell))。
* 20 GB 可用存储容器主机图像、 OS 基础映像和安装程序脚本。
* 在 HYPER-V 主机上的管理员权限。

> Windows 服务器容器不需要 HYPER-V 然而保持事情简单本指南假定一个 HYPER-V 环境被用来运行 Windows 服务器容器主机。

## 安装新的虚拟机上的一个新的集装箱主机
Windows 服务器容器包含几个组件如 Windows 服务器容器主机和容器 OS 基础映像。我们已经把一个脚本，将下载并为您配置这些项目。

以管理员身份启动 PowerShell 会话。

``` powershell
start-process powershell -Verb runAs
```

使用下面的命令来下载配置脚本。此外可以把脚本手动从这个位置 — — [配置脚本] (http://aka.ms/newcontainerhost) 下载。
 
``` PowerShell
wget -uri https://aka.ms/newcontainerhost -OutFile New-ContainerHost.ps1
```
   
运行以下命令来创建和配置容器主机在哪里 '<containerhost>' 将虚拟机的名称和 '<password>' 会被分配给管理员帐户的密码。</password> </containerhost>

``` powershell
.\New-ContainerHost.ps1 –VmName <containerhost> -Password <password>
```
  
脚本开始时将会要求您阅读并接受许可条款。

```
Before installing and using the Windows Server Technical Preview 3 with Containers virtual machine you must:
    1. Review the license terms by navigating to this link: http://aka.ms/WindowsServerTP3ContainerVHDEula
    2. Print and retain a copy of the license terms for your records.
By downloading and using the Windows Server Technical Preview 3 with Containers virtual machine you agree to such
license terms. Please confirm you have accepted and agree to the license terms.
[N] No  [Y] Yes  [?] Help (default is "N"): Y
```

该脚本将然后开始下载和配置 Windows 服务器容器组件。此过程可能需要很长一段时间由于大下载。  

窗口服务器容器主机在部署过程中，您可能会收到下面的消息。 
```
This VM is not connected to the network. To connect it, run the following:
Get-VM | Get-VMNetworkAdapter | Connect-VMNetworkAdapter -Switchname <switchname>
```  
如果你这样做，检查虚拟机的属性，并将虚拟机连接到一个虚拟交换机。您还可以运行下面的 PowerShell 命令在哪里 '<switchname>' 是您想要连接到虚拟机的 HYPER-V 虚拟交换机的名称。</switchname>

``` powershell 
Get-VM | Get-VMNetworkAdapter | Connect-VMNetworkAdapter -Switchname <switchname>
```

当配置脚本已完成时，启动虚拟机。
  
<center>![] (./ media/containerhost2.png)</center><br />
  
最后登录到虚拟机中使用在配置过程中指定的密码，请确保虚拟机具有一个有效的 IP 地址。 

## 视频演练

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Configure-Windows-Server-Containers-on-a-Local-System/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>


## 下一步-开始使用容器

现在，你有一个 Windows 服务器 2016年系统运行 Windows 服务器容器功能跳转到以下指南开始使用 Windows 服务器容器和 Windows 服务器容器的图像。 
 
[快速启动: Windows 服务器容器和码头工人](./ manage_docker.md) 

[快速启动: Windows 服务器容器和 PowerShell](./ manage_powershell.md) 

-------------------

[回容器首页](../ containers_welcome.md) [为当前版本中的已知问题] (.../ about/work_in_progress.md)
