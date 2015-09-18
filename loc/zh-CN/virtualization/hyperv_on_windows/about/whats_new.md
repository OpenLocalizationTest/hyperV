# 什么是新超 v 上 Windows 10

本主题说明在 Windows 10 ® HYPER-V 中的新的和更改的功能。

## Windows PowerShell 直接

还有现在简便可靠的方法从主机操作系统运行在虚拟机中的 Windows PowerShell 命令。没有网络或防火墙的要求，也没有特殊的配置。
无论您的远程管理配置，它正常工作。

若要创建 PowerShell 直接会话，请使用以下命令之一:

``` PowerShell
Enter-PSSession -VMName VMName
Invoke-Command -VMName VMName -ScriptBlock { commands }
```

今天，HYPER-V 管理员依靠两个类别的工具连接到一台在 HYPER-V 主机上的虚拟机:
- 远程管理工具，如 PowerShell 或远程桌面
- 超 V 虚拟机连接 (VM 连接)

这两种技术工作很好，但是每个有权衡取舍随着 HYPER-V 部署。VMConnect 是可靠的但它很难实现自动化。 

Windows PowerShell 直接提供了一个功能强大的脚本和自动化经验与 VMConnect 的简单性。因为 Windows PowerShell 直接运行主机和虚拟机之间，那里是没有需要网络连接，或启用远程管理。

#### 要求
- 您必须连接到 Windows 10 或 Windows 服务器技术预览与运行 Windows 10 或 Windows 服务器技术预览作为客人的虚拟机的主机。
- 您需要使用主机上的 HYPER-V 管理员凭据登录。
- 您需要为该虚拟机的用户凭据。
- 您想要连接到的虚拟机必须运行和启动。


## 热添加和删除网络适配器和内存

现在，你可以添加或删除网络适配器在虚拟机运行时，无需停机。 

您也可以调整内存分配给虚拟机在它运行时，即使你还没有启用动态内存的数量。

## 生产检查站

生产检查站允许您轻松地创建虚拟机，可以完全支持所有生产工作负载的方式稍后恢复的"时间点"图像。这被通过使用备份技术内部客人来创建检查点，而不是使用保存的状态的技术。对于生产检查站卷快照服务 (VSS) 使用 Windows 虚拟机内。Linux 虚拟机刷新它们的文件系统缓冲区，以创建一个文件系统一致性检查点。 


> * * 重要: * * 新的虚拟机的默认值将与回退到标准检查点创建生产检查点。 
 

## HYPER-V 管理器的改进

- * * 备用凭据支持 * * — — 你现在可以使用一组不同的凭据在 HYPER-V 管理器连接到另一台 Windows 10 技术预览远程主机时。 

- * * 关闭级别管理 * *-你可以现在使用 HYPER-V 管理器来管理多个版本的 HYPER-V。

- * * 更新管理协议 * *-HYPER-V 管理器已被更新，以使用 WS 人协议，允许 CredSSP、 Kerberos 或 NTLM 身份验证的远程 HYPER-V 主机进行通信。当您使用 CredSSP 连接到远程的 HYPER-V 主机时，它允许您在 Active Directory 中执行没有第一次有利的受约束的委派的实时迁移。WS-以人为本的基础设施还简化了主机进行远程管理所需的配置。


## 连接待机作品 

当使用总是 On/Always 连接 (AOAC) 电源模型的计算机上启用 HYPER-V，则连接待机电源状态是现在可用。

在 Windows 8 和 8.1，HYPER-V 造成计算机总是 On/Always 连接 (AOAC) 功率模型 (也称为瞬子) 用于从来不睡觉。看到这 [KB 文章] (
https://support.microsoft.com/en-us/kb/2973536) 为一个完整的描述。


## Linux 安全启动 

更多的 Linux 操作系统，第 2 代虚拟机上运行现在可以使用启用了安全启动选项启动。安全启动运行技术预览版的主机上启用了 Ubuntu; 14.04，后来和 SUSE Linux 企业服务器 12。你第一次启动虚拟机之前，您必须指定虚拟机应该使用 Microsoft UEFI 证书颁发机构。

    Set-VMFirmware vmname -SecureBootTemplate MicrosoftUEFICertificateAuthority

在 HYPER-V 上运行 Linux 虚拟机的详细信息，请参阅 [Linux 和 FreeBSD 在 HYPER-V 虚拟机] (http://technet.microsoft.com/library/dn531030.aspx)。
 
 
## 虚拟机配置版本 

当您移动或导入从运行 Windows 8.1 主机上 Windows 10 运行 HYPER-V 主机的虚拟机时，虚拟机的配置文件不会自动升级。这允许虚拟机来运行 Windows 8.1 主机移回。 

虚拟机配置版本代表什么版本的 HYPER-V 虚拟机配置，保存的状态，和快照的文件是与兼容。虚拟机的配置版本 5 兼容 Windows 8.1，可以运行在 Windows 8.1 和 Windows 10。

#### 如何检查在 HYPER-V 上运行的虚拟机的配置版本? 

从提升的命令提示符下，运行以下命令:

``` PowerShell
Get-VM * | Format-Table Name, Version
```

#### 如何升级配置版本的虚拟机?  

从提升 Windows PowerShell 命令提示符下，运行以下命令之一:

``` PowerShell
Update-VmConfigurationVersion <vmname>
```

或

``` PowerShell
Update-VmConfigurationVersion <vmobject>
```


* * 重要: * *
- 您的虚拟机配置版本升级后，你不能将虚拟机移动到运行 Windows 8.1 的主机。
- 您不能降级版本 6 到版本 5 的虚拟机配置版本。
- 您必须先关闭虚拟机升级虚拟机的配置。
- 升级之后，虚拟机使用新的配置文件格式。


## 新的虚拟机配置文件格式

虚拟机现在有新的配置文件格式，旨在提高阅读和写作的虚拟机配置数据的效率。它同时也被为了减少潜在的数据损坏，如果存储故障。 


> * * 重要: * *。VMCX 文件是二进制的格式。



## 通过 Windows Update 提供一体化服务

集成服务为 Windows 客人的更新现在分布通过 Windows 更新。

集成组件 (也称为集成服务) 是合成的驱动程序，允许虚拟机与主机操作系统进行通信的一组。他们控制从时间同步到客人文件复制服务。

从历史上看，所有新版本的 HYPER-V 附带新的集成组件。升级 HYPER-V 主机升级集成组件在虚拟机以及必需。新的集成组件都包含在 HYPER-V 主机，然后他们在使用 vmguest.iso 的虚拟机中安装了。这个过程需要重新启动虚拟机，不能与其他 Windows 更新批处理。因为 HYPER-V 管理员必须提供 vmguest.iso 和虚拟机管理员不得不安装它们，集成组件升级所需的 HYPER-V 管理员具有管理员凭据在虚拟机 — — 这并非总是如此。

在 Windows 10 和前进，所有集成组件将交付给虚拟加工通过 Windows 更新和其他重要更新。

有可用更新今天为运行的虚拟机:
*  Windows 服务器 2012
*  Windows 服务器 2008 R2
*  Windows 8
*  Windows 7

虚拟机必须连接到 Windows Update 或 WSUS 服务器。

阅读更多有关我们如何确定适用性，看到这篇 [博客] (http://blogs.technet.com/b/virtualization/archive/2014/11/24/integration-components-how-we-determine-windows-update-applicability.aspx)。


见 [此博客] (http://blogs.msdn.com/b/virtual_pc_guy/archive/2014/11/12/updating-integration-components-over-windows-update.aspx) 职位的安装集成服务的详细演练。


> * * 重要: * * ISO 图像文件 vmguest.iso 不再需要更新集成组件。




## 下一步
[走过超 V 在 Windows 上 10](..) \quick_start\walkthrough.md 