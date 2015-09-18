# 管理远程超 V 主机与超 V 经理 #

HYPER-V 管理器提供了工具来诊断和管理您本地的 HYPER-V 主机和远程主机的小数目。

若要连接到 HYPER-V 主机在 HYPER-V 管理器中，请确保 * * HYPER-V 管理器 * * 是在左窗格中选择，然后选择 * * 连接到服务器......* * 在右侧窗格中。

![] (媒体/HyperVManager-ConnectToHost.png)

## 支持的 HYPER-V 主机组合与 HYPER-V 管理器
在 Windows 10 HYPER-V 管理器允许您管理:
* Windows 10
* Windows 8.1 和 Windows 服务器 2012 R2 HYPER-V 主机
* Windows 8 和 Windows 2012 HYPER-V 主机

在 Windows 8.1 和 Windows Server 2012 R2 HYPER-V 管理器允许您管理:
* Windows 8.1 和 Windows 服务器 2012 R2 HYPER-V 主机
* Windows 8 和 Windows 2012 HYPER-V 主机

> * * 请注意: * * 适合所有主机版本并不是所有 HYPER-V 管理器的功能。

## 管理本地主机 ##
若要添加 HYPER-V 管理器作为 HYPER-V 主机的本地主机，请选择 * * 本地计算机 * * 中 * * 选择计算机 * * 对话框。

![] (媒体/HyperVManager-ConnectToLocalHost.png)

如果无法建立连接:
*  请确保启用 HYPER-V 服务器角色。请参阅 [检查兼容性演练部分] (.../ quick_start/walkthrough_compatibility.md)。
*  确认您的用户帐户是 HYPER-V 管理员组的一部分。


## 管理您的域中的 HYPER-V 主机 ##

若要添加一个远程的 HYPER-V 主机到 HYPER-V 管理器，请选择 * * 另一计算机 * * 中 * * 选择计算机 * * 对话框和文本字段中输入远程主机的主机名、 NetBIOS 或 FQDN。

![] (媒体/HyperVManager-ConnectToRemoteHost.png)

Windows 10 大大扩展了远程连接类型的可能的组合。 
现在你可以连接到远程 Windows 10 或稍后使用的主机名称或 IP 地址的主机。  

为了管理远程 HYPER-V 主机，必须在两台计算机上启用远程管理。

你可以通过系统属性-远程管理设置 > 或以管理员身份运行下面的 PowerShell 命令:  

``` PowerShell
winrm quickconfig
```

如果你当前的用户帐户匹配一个 HYPER-V 管理员帐户在远程主机上的，往前走，然后按 * * 好 * * 连接。  

这是唯一受支持的方法来管理远程主机在 HYPER-V 管理器在 Windows 8 或 Windows 8.1。


### 不同的用户身份连接到远程主机
在 Windows 10，如果你不运行正确的用户帐户的远程主机，您可以连接作为另一个用户使用备用凭据。

若要指定远程 HYPER-V 主机的凭据，请选择 * * 作为另一个用户连接: * * 中 * * 选择计算机 * * 对话盒然后选择 * * 设置用户......* *。

![] (媒体/HyperVManager-ConnectToRemoteHostAltCreds.png)

> 注意: 它是很容易被人们遗忘的用户设置和与不指定用户单击确定。

### 使用连接到远程主机的 IP 地址
有时它是更容易使用的 IP 地址，而不是主机名称进行连接。

要使用 IP 地址的连接，请输入 IP 地址到 * * 另一计算机 * * 文本字段。


## 管理 HYPER-V 主机您的域以外 (或不带有域) ##
<!--Assuming this isn't done yet...again needs context.-->
Local Hyper-V Host:
1.	Enable-PSRemoting
Came back with netowork set to public.
Ran
Set-NetConnectionProfile -Name "name" -NetworkCategory private
2. Set-Item WSMan:\localhost\Client\TrustedHosts * -Force
3. Enable-WSManCredSSP -Role client -DelegateComputer *

为仅限工作组:
1. (应完成)Policy\Administrative Templates\System\Credentials Delegation\Allow 委派新鲜凭据 → 计算机设置为启用，并添加 WSMAN / *]。

2. 计算机 Policy\Administrative Templates\System\Credentials Delegation\Allow 委派新鲜凭据与仅 NTLM 服务器身份验证 → 设置为启用，并添加 WSMAN / * 到的计算机的列表，检查连接 OS 默认值与输入上面的框
3. 设置为已启用的计算机 Policy\Administrative \windows 组件 \windows 远程管理 (WinRM) \WinRM Client\Allow CredSSP 身份验证 →

远程超 V 主机:
1. :) 禁用防火墙
2. 启用 PSRemoting
3. 设置项目 WSMan:\localhost\Client\TrustedHosts *-力
所以这是我用的只演示说明。取代 * 和关闭防火墙与一台电脑，让 credssp 和通过 winRM


