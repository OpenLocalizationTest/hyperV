ms。ContentId: d0a07897-5fd2-41a5-856d-dc8b499c6783
标题: 管理 Windows PowerShell 的服务器容器

# 快速启动: Windows 服务器容器 PowerShell

这篇文章将走过管理 Windows PowerShell 的服务器容器的基本原理。涵盖的项目将包括创建 Windows 服务器容器和 Windows 服务器容器图像、 删除 Windows 服务器容器和容器图像和最终部署到 Windows 服务器容器应用程序。

有问题吗?去询问他们对 [Windows 容器论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。

> * * 请注意: * * 使用 PowerShell 创建的 Windows 服务器容器不能目前管理与码头工人和签证反之亦然。若要创建容器与码头工人相反，请参阅 [快速启动: Windows 服务器容器和 Docker](./manage_docker.md)。<br /><br />如果你想要知道更多，[阅读常见问题] (.../ about/faq.md#WhydoIhavetopickbetweenDockerandPowerShellforWindowsServerContainermanagement)。

## 系统必备组件
若要完成此演练下列项目必须要到位。

- Windows 服务器 2016 TP3 或稍后配置为具有 Windows 服务器容器功能。
- 这个系统必须连接到网络并能够访问互联网。

如果您需要配置容器功能，请参阅下列指南: [在 Azure 容器安装] (./azure_setup.md) 或 [容器安装 HYPER-V 中] (./container_setup.md)。 

## PowerShell 基本容器管理

这第一个示例将遍历创建和删除 Windows 服务器容器和 Windows 服务器容器图像与 PowerShell 的基础知识。

若要开始通过日志走进您的 Windows 服务器容器主机系统，您将看到 Windows 命令提示符。

![] (media/cmd.png)

通过键入 'powershell' 启动 PowerShell 会话。你会知道你是在当提示更改从 PowerShell 会话中 'C:\directory >' 到' PS C:\directory >'。

```
C:\> powershell
Windows PowerShell
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\>
```

使用 Get 命令 ' 看到容器模块中可用的命令

```
PS C:\> Get-Command -Module containers

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Function        Install-ContainerOSImage                           1.0.0.0    Containers
Function        Uninstall-ContainerOSImage                         1.0.0.0    Containers
Cmdlet          Add-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Connect-ContainerNetworkAdapter                    1.0.0.0    Containers
Cmdlet          Disconnect-ContainerNetworkAdapter                 1.0.0.0    Containers
Cmdlet          Export-ContainerImage                              1.0.0.0    Containers
Cmdlet          Get-Container                                      1.0.0.0    Containers
Cmdlet          Get-ContainerHost                                  1.0.0.0    Containers
Cmdlet          Get-ContainerImage                                 1.0.0.0    Containers
Cmdlet          Get-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Import-ContainerImage                              1.0.0.0    Containers
Cmdlet          Move-ContainerImageRepository                      1.0.0.0    Containers
Cmdlet          New-Container                                      1.0.0.0    Containers
Cmdlet          New-ContainerImage                                 1.0.0.0    Containers
Cmdlet          Remove-Container                                   1.0.0.0    Containers
Cmdlet          Remove-ContainerImage                              1.0.0.0    Containers
Cmdlet          Remove-ContainerNetworkAdapter                     1.0.0.0    Containers
Cmdlet          Set-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Start-Container                                    1.0.0.0    Containers
Cmdlet          Stop-Container                                     1.0.0.0    Containers
Cmdlet          Test-ContainerImage                                1.0.0.0    Containers
```


接下来请确保您的系统具有有效的 IP 地址，使用 ipconfig 并注意到此地址以供以后使用。

```
ipconfig

Ethernet adapter Ethernet 3:

   Connection-specific DNS Suffix  . :
   IPv6 Address. . . . . . . . . . . : 2601:600:8f01:84eb::e
   IPv6 Address. . . . . . . . . . . : 2601:600:8f01:84eb:a8c1:a3e:96b7:ffcb
   Link-local IPv6 Address . . . . . : fe80::a8c1:a3e:96b7:ffcb%5
   IPv4 Address. . . . . . . . . . . : 192.168.1.25
```

如果您正在从 Azure 而不是使用 ipconfig 您将需要获取的公共 IP 地址 Azure 虚拟机的虚拟机。

![] (media/newazure9.png)

### 步骤 1-创建一个新的容器

在创建 Windows 服务器容器之前您需要容器映像的名称和虚拟交换机将附加到新的容器的名称。

使用 Get ContainerImage 命令返回容器图像列表加载在主机上。
``` PowerShell
Get-ContainerImage

Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
WindowsServerCore CN=Microsoft 10.0.10514.0 True
```

使用 Get VMSwitch' 命令返回主机上可用的开关的列表。

``` PowerShell
Get-VMSwitch

Name           SwitchType NetAdapterInterfaceDescription
----           ---------- ------------------------------
Virtual Switch NAT
```

运行以下命令来创建一个容器。当运行 ' 新货柜的你将命名容器，指定容器的形象，并选择网络交换机容器用。注意在此示例中的输出放在一个变量 $container。 

``` PowerShell
$container = New-Container -Name "MyContainer" -ContainerImageName WindowsServerCore -SwitchName "Virtual Switch"
```

要在主机上看到一个容器列表并验证创建容器，请使用 ' Get 货柜的命令。

``` PowerShell
Get-Container

Name        State Uptime   ParentImageName
----        ----- ------   ---------------
MyContainer Off   00:00:00 WindowsServerCore
```

若要启动容器，请使用 ' 开始-货柜的 proivding 容器的名称。

``` PowerShell
Start-Container -Name "MyContainer"
```

您可以与使用 PowerShell 远程处理命令如 '调用命令' 或 ' enter 键-PSSession' 的容器交互。下面的示例将远程 PowerShell 会话创建到使用输入-PSSession' 命令的容器。此命令所需的容器 id 创建远程会话。创建容器时，容器 id 是 '$container' 变量中存储。 

请注意，一旦创建了远程会话命令提示符将更改为包含容器 id ' [2446380e-629]' 首先 11 字符。

``` PowerShell
Enter-PSSession -ContainerId $container.ContainerId -RunAsAdministrator

[2446380e-629]: PS C:\Windows\system32>
```

容器可以管理的非常像物理计算机或虚拟机上。如 ipconfig 命令来返回容器，'mkdir 来创建一个目录中的容器和像 '如果' PowerShell 命令所有工作的 IP 地址。往前走，到容器如创建的文件或文件夹进行更改。

``` PowerShell
ipconfig > c:\ipconfig.txt
```

你可以阅读文件，确保命令成功完成的内容。

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-E0D87408-325B-4818-ADB2-2EC7A2005739-0):

   Connection-specific DNS Suffix  . : corp.microsoft.com
   Link-local IPv6 Address . . . . . : fe80::400e:1e0e:591c:beef%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1
```

现在，该容器已被修改，退出远程 PowerShell 会话。

``` PowerShell
exit
```

通过提供容器名称到 ' 停止货柜的命令来停止容器。

``` PowerShell
Stop-Container -Name "MyContainer"
```

### 步骤 2-创建一个新的集装箱图像

现在可从这个容器的图像。

要创建一个新的映像，命名为 'newimage' 使用 ' 新 ContainerImage' 命令。

``` PowerShell
$newimage = New-ContainerImage -ContainerName MyContainer -Publisher Demo -Name newimage -Version 1.0
```

使用 Get ContainerImage' 返回容器映像的列表。

``` PowerShell
Get-ContainerImage

Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
newimage          CN=Demo      1.0.0.0      False
WindowsServerCore CN=Microsoft 10.0.10254.0 True
```

### 第 3 步-从图像创建新的容器

现在，您已创建一个自定义的容器形象，往前走和部署新的容器，从这张图片。

创建一个名为 'newcontainer' 从容器图像命名为 'newimage' 的容器，把结果输出到一个名为 $newcontainer 变量。

``` PowerShell
$newcontainer = New-Container -Name "newcontainer" -ContainerImageName newimage -SwitchName "Virtual Switch"
```

开始新的容器。
``` PowerShell
Start-Container $newcontainer
```

创建与容器的远程 PowerShell 会话。
``` PowerShell
Enter-PSSession -ContainerId $newcontainer.ContainerId -RunAsAdministrator
```

最后请注意，此新的容器包含较早前在本练习中创建的 ipconfig.txt 文件。

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-E0D87408-325B-4818-ADB2-2EC7A2005739-0):

   Connection-specific DNS Suffix  . : corp.microsoft.com
   Link-local IPv6 Address . . . . . : fe80::400e:1e0e:591c:beef%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1
```

 一旦你做工作与此容器，退出远程 PowerShell 会话。

``` PowerShell
exit
```

这个练习显示图像取自改装过的集装箱将包括所有的修改。虽然这里的例子是简单的文件修改，这同样适用如果您要将软件安装到 web 服务器等容器。

### 第 4 步-删除容器和容器图像

要停止正在运行的所有容器，请都运行下面的命令。

``` PowerShell
Get-Container | Stop-Container
```
运行以下命令删除所有容器。

``` PowerShell
Get-Container | Remove-Container -Force
```
若要删除名为 'newimage' 的集装箱图像，请运行以下命令。

``` PowerShell
Get-ContainerImage -Name newimage | Remove-ContainerImage -Force
```

## 主机在一个容器中的 Web 服务器

下一个例子将展示一个更实际的用例为 Windows 服务器容器。

### 第 1 步 – 从 Windows 服务器核心 OS 映像创建容器

若要创建 web 服务器容器图像，你首先需要部署和启动容器从 Windows 服务器核心 OS 映像。
``` PowerShell
$container = New-Container -Name webbase -ContainerImageName WindowsServerCore -SwitchName "Virtual Switch"
 ```

启动容器。
``` PowerShell
Start-Container $container
```

当容器，容器创建远程 PowerShell 会话。
``` PowerShell
Enter-PSSession -ContainerId $container.ContainerId -RunAsAdministrator
```

### 第 2 步-安装 Web 服务器软件

下一步是安装 web 服务器软件。本示例将使用 nginx 的 Windows。使用下面的命令来自动下载并解压缩到 c:\nginx-1.9.3 nginx 软件。* * 注意 * * 这一步将要求容器主机连接到互联网。

下载 nginx 软件。
``` PowerShell
wget -uri 'http://nginx.org/download/nginx-1.9.3.zip' -OutFile "c:\nginx-1.9.3.zip"
```

提取 nginx 软件。
``` PowerShell
Expand-Archive -Path C:\nginx-1.9.3.zip -DestinationPath c:\ -Force
```
这是所有需要 nginx 软件安装完成。

退出远程 PowerShell 会话。
``` PowerShell
exit
```

停止使用下面的命令的容器。 
``` PowerShell
Stop-Container $container
```
### 第 3 步-从 Web 服务器容器创建图像

与容器修改以包含 nginx web 服务器软件，您现在可以创建图像从这个容器。
``` PowerShell
$webserverimage = New-ContainerImage -Container $container -Publisher Demo -Name nginxwindows -Version 1.0
```
当完成时，使用 Get ContainerImage 命令来验证已创建的图像。

``` PowerShell
Get-ContainerImage

Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
nginxwindows      CN=Demo      1.0.0.0      False
WindowsServerCore CN=Microsoft 10.0.10254.0 True
```

### 第 4 步-部署 Web 服务器准备好容器

若要部署基于 'nginxwindows' 图像的 Windows 服务器容器，请使用 ' 新货柜的 PowerShell 命令。

``` PowerShell
$webservercontainer = New-Container -Name webserver1 -ContainerImageName nginxwindows -SwitchName "Virtual Switch"
```

启动容器。
``` PowerShell
Start-Container $webservercontainer
```

创建与新的容器的远程 PowerShell 会话。
``` PowerShell
Enter-PSSession -ContainerId $webservercontainer.ContainerId -RunAsAdministrator
```

一旦工作在容器内，可以启动 nginx web 服务器和 web 内容上演。
``` PowerShell
cd c:\nginx-1.9.3\
```

启动 nginx web 服务器。
``` PowerShell
start nginx
```

并退出本届 PS。
``` PowerShell
exit
```

### 第 5 步-配置容器网络

根据容器主机和网络的配置，容器将要么接收 IP 地址从 DHCP 服务器或容器主机本身使用网络地址转换 (NAT)。这个引导的步行通过配置为使用 nat。在此配置中从容器的端口映射到容器主机上的端口。在容器中承载的应用程序然后可以通过 IP 地址访问 / 集装箱主机的名称。例如如果端口 80 从容器被映射到容器主机上的端口 55534，一个典型的 http 请求到应用程序看起来和这个 http://contianerhost:55534。 

对于这个实验我们需要创建此端口映射。为此，我们需要知道容器和内部 (应用程序) 和外部 (容器主机) 端口，将配置的 IP 地址。对于这个示例让我们保持它的简单和映射端口 80 从容器到主机的端口 80。使用添加-NetNatStaticMapping' 命令 '— — InternalIPAddress 将会在本演练中的容器应该是' 172.16.0.2 的通信的 IP 地址。

``` PowerShell
Add-NetNatStaticMapping -NatName "ContainerNat" -Protocol TCP -ExternalIPAddress 0.0.0.0 -InternalIPAddress 172.16.0.2 -InternalPort 80 -ExternalPort 80
```
在创建端口映射时你还需要配置入站的防火墙规则的配置的端口。要做到为端口 80 运行下面的命令。 

``` PowerShell
if (!(Get-NetFirewallRule | where {$_.Name -eq "TCP80"})) {
    New-NetFirewallRule -Name "TCP80" -DisplayName "HTTP on TCP/80" -Protocol tcp -LocalPort 80 -Action Allow -Enabled True
}
```

下一步如果您正在从 Azure 并不已经创建了一个虚拟机端点将需要创建一个现在。在 Azure VM 终结点上的详细信息请参阅这篇文章: [设置 Azure VM 端点] (https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/)。

### 步骤 6 – 访问容器承载的网站
使用创建的 web 服务器容器，您可以现在结帐容器中承载的应用程序。要这样做，打开另一台计算机上的浏览器并输入 'http://containerhost-ipaddress'。请注意在这里，您将浏览到容器主机和不是容器本身的 IP 地址。 

如果一切都已正确配置，您将看到 nginx 的欢迎页面。

![] (media/nginx.png)

在这一点上，随时更新网站。在您自己的示例网站，复制或使用已创建一个简单的 Hello World 示例站点为此演示。

首先，你将需要重新创建远程的 PS 会话与容器。
``` PowerShell
Enter-PSSession -ContainerId $webservercontainer.ContainerId -RunAsAdministrator
```
然后运行以下命令以下载并替换 index.html 文件。

``` powershell
wget -uri 'https://raw.githubusercontent.com/Microsoft/Virtualization-Documentation/master/doc-site/virtualization/windowscontainers/quick_start/SampleFiles/index.html' -OutFile "C:\nginx-1.9.3\html\index.html"
```
   
在更新该网站后，导航回 'http://containerhost-ipaddress'。

![] (media/hello.png)

## 视频演练

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Deploying-and-Managing-Windows-Server-Containers-with-PowerShell/player" width="800" height="450"  allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>


## 接下来的步骤
现在，你有容器设置和介绍的工具，去建立自己的容器应用程序。

这里是一个更完整的 [PowerShell 参考] (.../ reference/powershell_overview.md)。

请记住，这是 * * 预览 * * 有 bug，我们有很多的工作进展。[此页](../ about/work_in_progress.md) 包含了许多我们已知的问题。

我们也非常密切地监测 [论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。

[GitHub] (https://github.com/Microsoft/Virtualization-Documentation/tree/master/windows-server-container-samples) 上也有预先制作的样品。

-----------------------------------
[回容器首页](../ containers_welcome.md) [为当前版本中的已知问题] (.../ about/work_in_progress.md)
