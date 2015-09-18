ms。ContentId: 5bbac9eb-c31e-40db-97b1-f33ea59ac3a3
标题: 工作进展

# 进展中的工作

如果你不看看你在这里讨论的问题或有疑问，请将它们贴 [论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。

-----------------------

## 一般功能

### 容器的 Windows 映像必须完全匹配容器主机
Windows 服务器容器需要匹配在尊重容器主机，以建立和补丁程序级别的操作系统映像。

如果你安装针对您将需要更新容器基本操作系统映像，以具有匹配的 OS 更新 Windows 容器主机更新。
<!-- Can we give examples of behavior or errors?  Makes it more searchable -->

* * 工作周围: * * 下载并安装容器的基础图像匹配容器主机的操作系统版本和修补程序级别。


### 零星地命令失败 — — 再试一次
在我们的测试中，有时需要多次运行命令。同样的原则适用于其他的操作。 
例如，如果您创建一个新文件，就不会出现，试着抚摸该文件。  

如果你有做到这一点，让我们知道通过 [论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。

* * 解决方法: * * 生成脚本等，他们多次尝试命令。  

### 所有非 c: / 驱动器自动映射到新的容器
所有非 c: / 对容器主机可用的驱动器自动映射到新运行 Windows 服务器容器。

在这个时间点有是没有办法到有选择性地地图文件夹到一个容器里，会自动映射驱动器的临时变通。

* * 工作周围: * * 我们正在努力。


### Windows 服务器容器非常缓慢地开始
如果你的容器以超过 30 秒开始，它可能正在执行许多重复的病毒扫描。

许多反恶意软件解决方案，例如 Windows Defender，也许不必要地扫描包括的所有操作系统的二进制文件和文件容器 OS 映像中的文件与在容器图像。出现这种情况何时创建新的容器，从反恶意软件的角度来看，所有的"容器的文件"看起来像以前尚未扫描的新文件。所以当容器内的进程尝试读取这些文件的反恶意软件组件首先扫描他们之前允许对文件的访问。在现实中这些文件已经被扫描集装箱图像被导入或拉到服务器时。 

--------------------------

## 网络

### 网络车厢每个集装箱的数量
在此版本中，我们支持一网络室每个集装箱。这意味着如果您与多个网络适配器有一个容器，你不能访问相同的网络端口，每个适配器上的 (例如

* * 工作周围: * * 如果多个终结点需要公开的容器，使用 NAT 端口映射。

### Windows 容器没有获得 ip 地址
如果您要连接到 windows 服务器容器用 DHCP VM 开关是集装箱主机能够接收 IP 是容器则不可能。

容器获得 169.254.* * *.* * * APIPA IP 地址。

* * 周围的工作: * *
这是共享内核的一个副作用。

启用 MAC 地址欺骗容器主机上。

这可以实现使用 PowerShell
```
Get-VMNetworkAdapter -VMName "[YourVMNameHere]"  | Set-VMNetworkAdapter -MacAddressSpoofing On
```

### 创建文件共享不能在容器中

目前它是不可能创建一个容器内的文件共享。如果你运行净份额你将看到这样的错误:

```
The Server service is not started.

Is it OK to start it? (Y/N) [Y]: y
The Server service is starting.
The Server service could not be started.

A service specific error occurred: 2182.

More help is available by typing NET HELPMSG 3547.
```

* * 周围的工作: * *
如果你想要将文件复制到一个容器可以使用其他方式圆通过在容器内运行 net use。 
```
net use S: \\your\sources\here /User:shareuser [yourpassword]
```

--------------------------

## 应用程序兼容性

有哪些应用程序工作和不工作在 Windows 服务器容器中的许多问题，我们决定分手成 [它自己的文章] 应用程序兼容性信息，(....../ reference/app_compat.md)。

一些最常见的问题也设在这里。

### WinRM 无法启动 Windows 服务器容器中
WinRM 启动，将引发错误，并再次停止。

* * 周围的工作: * *
使用 WMI，[RDP](#RemoteDesktopAccessOfContainers) 或输入 PSSession ContainerID

### 不能与容器使用 DISM 中的 IIS 安装 ASP.NET 4.5 或 ASP.NET 3.5 
在一个容器中安装 IIS ASPNET45 不工作 Windows 服务器容器内。

``` PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ASPNET45
```

此操作失败，因为 ASP.NET 4.5 不在容器中运行。

* * 工作周围: * * 相反，安装使用 IIS 的 Web 服务器角色。 

``` PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName Web-Server
```

请参阅 [应用程序兼容性文章] (.../ reference/app_compat.md) 有关哪些应用程序可以使用集装箱详细信息。

--------------------------


## 码头工人管理

### 码头工人客户端进行不安全的默认
在此预发行版，码头工人沟通是公共的如果你知道去哪里找。

### 不要使用 Windows 服务器容器的码头工人命令

已知的会失败的命令:

|* * 码头命令 * * |* * 在哪里它运行 * * |* * 错误 * * |* * 注意 * * |
|:-----|:-----|:-----|:-----|
|* * 码头提交 * * |图像 |码头工人停止运行容器并不会显示正确的错误消息 |犯下停止的容器工程。为运行容器: 我们正在对它:) |
|* * 码头 diff * * |守护程序 |错误: 不支持 windows graphdriver Changes() | |
|* * 码头杀 * * |集装箱 |错误: 无效的信号: 杀错误: 未能杀死容器: [] | |
|* * 码头负载 * * |图像 |默默地失败 |没有错误，但图像没有加载或 |
|* * 码头暂停 * * |集装箱 |错误: Windows 容器不能暂停。可能不支持 | |
|* * 港口码头 * * |集装箱 | |没有端口上市，我们甚至可以能到 RDP。
|* * 码头拉 * * |守护程序 |错误: 系统找不到的文件路径。我们不能运行容器使用此映像。|获取添加图像不能使用。我们正在对它:) |
|* * 码头重新启动 * * |集装箱 |错误: 系统关机是在进步。| |
|* * 码头取消暂停 * * |集装箱 | |不能测试，因为暂停还不工作。

如果任何不在此列表失败 (或如果命令失败比预期的不一样)，让我们知道通过 [论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。



### 部分工作与 Windows 服务器容器的码头工人命令

具有部分功能的命令:

|* * 码头命令 * * |* * 上运行......* * |* * 参数 * * |* * 注意 * * |
|:-----|:-----|:-----|:-----|
|* * 码头附加 * * |集装箱 |— — 没有 stdin = false |该命令不退出时按下 Ctrl P 和 CTRL-Q |
| | |— — sig 代理 = true |工程 |
|* * 码头生成 * * |图像 |-f — 文件 |错误: 无法准备上下文: 无法获取 synlinks |
| | |— — 力 rm = false |工程 |
| | |— — 无缓存 = false |工程 |
| | |-q，— — 安静 = false | |
| | |— — rm = true |works|
| | |-t，--标记 =""|工程 |
|* * 码头登录 * * |守护程序 |-e，-p，-u |sporratic 行为 |
|* * 码头工人推 * * |守护程序 | |获取偶尔"存储库中不存在"的错误。|
|* * 码头 rm * * |集装箱 |-f |错误: 系统关机是在进步。

如果有不在此列表中的任何失败，如果命令失败不同于预期，或如果你发现周围的工作，让我们知道通过 [论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。


### 粘贴到交互式码头会话命令仅限于 50 个字符
如果您将一个命令行复制到码头的交互式会话，它是目前仅限于 50 个字符。

这不是由设计，我们正在解除限制。

### net 使用返回系统错误 1223年而不是提示输入用户名或密码
解决方法: 指定用户名和密码，同时，当运行净使用。
```
net use S: \\your\sources\here /User:shareuser [yourpassword]
``` 

### HCS 垫片错误时创建新的容器图像
如果你遇到这样的错误信息:
```
hcsshim::ExportLayer - Win32 API call returned error r1=2147942523 err=The filename, directory name, or volume label syntax is incorrect. layerId=606a2c430fccd1091b9ad2f930bae009956856cf4e6c66062b188aac48aa2e34 flavour=1 folder=C:\ProgramData\docker\windowsfilter\606a2c430fccd1091b9ad2f930bae009956856cf4e6c66062b188aac48aa2e34-1868857733
```

你在打击由零天修补程序的 Windows 服务器 2016 TP3 解决问题。

如果你打其他 hcsshim 错误，让我们知道通过 [论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。


## 访问 windows 服务器容器与远程桌面 
Windows 服务器容器可以管理/互动与通过 RDP 会话。

以下步骤需要远程连接到使用 RDP 的 Windows 服务器容器。它假定该容器连接到网络通过 NAT 开关。

* * 在容器中，你想要连接到 * *

以下步骤要求要么管理容器使用码头，或当使用 PowerShell，指定 '-RunAsAdministrator' 切换时连接到容器。

1. 获取容器的 IP 地址

  ```
  ipconfig
  ```
  
  返回与此类似
  
  ```
  Windows IP Configuration

  Ethernet adapter vEthernet (Virtual Switch-f758a5a9519e1956cc3bef06eb03e5728d3fb61cf6d310246185587be490210a-0):

  Connection-specific DNS Suffix  . :
  Link-local IPv6 Address . . . . . : fe80::91cd:fb4c:4ea5:51df%17
  IPv4 Address. . . . . . . . . . . : 172.16.0.2
  Subnet Mask . . . . . . . . . . . : 255.240.0.0
  Default Gateway . . . . . . . . . : 172.16.0.1
  ```
  
  请注意 IPv4 地址通常是在格式 172.16.x.x

2. 为容器为内置管理员用户设置密码

  ```
  net user administrator [yourpassword]
  ```

3. 对容器启用内置管理员用户

  ```
  net user administrator /active:yes
  ```

* * 容器主机上 * *

由于 Windows 服务器已具有默认启用的高级安全性的 Windows 防火墙我们需要按顺序为 RDP 上班打开一些端口来进行通信。

以下步骤要求容器主机上以管理员身份启动 PowerShell。

1. 允许默认 RDP 端口通过 Windows 高级防火墙

  ```
  New-NetFirewallRule -Name "RDP" -DisplayName "Remote Desktop Protocol" -Protocol TCP -LocalPort @(3389) -Action Allow
  ```

2. 允许为 RDP 连接到容器的额外端口

  ```
  New-NetFirewallRule -Name "ContainerRDP" -DisplayName "RDP Port for connecting to Container" -Protocol TCP -LocalPort @(3390) -Action Allow
  ```
  
  这一步开辟了集装箱主机上的端口 3390。它将用于打开 RDP 会话到容器。 

3. 添加现有 NAT 端口映射

  在此步骤中，您需要从步骤 1 容器内的 IP 地址

  ```
  Add-NetNatStaticMapping -NatName ContainerNAT -Protocol TCP -ExternalPort 3390 -ExternalIPAddress 0.0.0.0 -InternalPort 3389 -InternalIPAddress [your container IP]
  ```
  
  在这里你确保端口 3390 进来的容器主机通信重定向到端口 3389 上的容器运行在您指定的 IP 地址。

* * 到容器通过 RDP 连接 * *

最后，您可以连接到使用 RDP 的容器。为了做，请运行以下命令了 (如安装了远程桌面客户端的系统上吗 

```
mstsc /v:[ContainerHostIP]:3390 /prompt
```

请指定管理员作为用户名称和密码，你选择了作为密码。

远程桌面连接会问你是否你想要连接到系统尽管会出现证书错误。  

* * 请注意: * * 退出集装箱 RDP 会话没有注销可能阻止容器关闭。

--------------------------

## PowerShell 管理

### 输入 PSSession 有 containerid 参数，不需要新 PSSession

这是正确的。


觉得免费的语音功能请求在 [论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。 

--------------------------
[回容器首页](../ containers_welcome.md)