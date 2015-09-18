ms。ContentId: 347fa279-d588-4094-90ec-8c2fc241f5b6
标题: 管理 Windows 服务器容器多克

#Quick 开始: Windows 服务器容器和码头工人

这篇文章将走过管理 windows 服务器容器与码头工人的基本原理。涵盖的项目将包括创建 Windows 服务器容器和 Windows 服务器容器图像、 删除 Windows 服务器容器和容器图像和最终部署到 Windows 服务器容器应用程序。

有问题吗?去询问他们对 [Windows 容器论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。

> * * 请注意: * * 使用 PowerShell 创建 Windows 容器不可以目前管理与码头工人和签证反之亦然。若要使用 PowerShell 创建容器，请参阅 [快速启动: Windows 服务器容器和 PowerShell](./manage_powershell.md)。<br /><br />如果你想要知道更多，[阅读常见问题] (.../ about/faq.md#WhydoIhavetopickbetweenDockerandPowerShellforWindowsServerContainermanagement)。

## 系统必备组件
若要完成此演练下列项目必须要到位。

- Windows 服务器 2016 TP3 或稍后配置为具有 Windows 服务器容器功能。
- 这个系统必须连接到网络并能够访问互联网。

如果您需要配置容器功能，请参阅下列指南: [在 Azure 容器安装] (./azure_setup.md) 或 [容器安装 HYPER-V 中] (./container_setup.md)。 

## 与码头工人的基本容器管理

这第一个示例将遍历创建和删除 Windows 服务器容器和 Windows 服务器容器图像与码头工人的基本知识。

若要开始通过日志走进您的 Windows 服务器容器主机系统，您将看到 Windows 命令提示符。

![] (media/cmd.png)

通过键入 'powershell' 启动 PowerShell 会话。你会知道你是在当提示更改从 PowerShell 会话中 'C:\directory >' 到' PS C:\directory >'。
```
C:\> powershell
Windows PowerShell
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\>
```
> 本快速入门将重点码头命令，然而一些如管理防火墙规则和复制文件的步骤将使用 PowerShell 命令运行。

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

与码头工人创建 Windows 服务器容器之前，您需要的名称或 ID exsisitng Windows 服务器容器图像。

查看所有图像加载容器主机上使用 '码头图像命令。

``` PowerShell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
windowsservercore   latest              9eca9231f4d4        30 hours ago        9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        30 hours ago        9.613 GB
```

现在，使用跑码头，创建一个新的 Windows 服务器容器。

``` PowerShell
docker run -it --name dockerdemo windowsservercore cmd
```
命令完成时你将工作在控制台会话中的容器。

工作在一个容器中是几乎相同的工作在虚拟或物理计算机上安装了 windows。您可以运行如 ipconfig 命令返回的容器，mkdir 来创建新的目录或 'powershell' 启动 PowerShell 会话的 IP 地址。往前走，到容器如创建的文件或文件夹进行更改。

``` PowerShell
ipconfig > c:\ipconfig.txt
```

你可以阅读文件，确保命令成功完成的内容。

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-94a3e12ad262b3059e08edc4d48fca3c8390e38c3b219023d4a0a4951883e658-0):

   Connection-specific DNS Suffix  . : 
   Link-local IPv6 Address . . . . . : fe80::cc1f:742:4126:9530%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1
```

现在，该容器已被修改，运行以下命令停止把你背在容器主机控制台会话中控制台会话。

``` PowerShell
exit
```

最后要看到一个容器列表容器上主机使用 '码头 ps — —' 命令。

``` PowerShell
docker ps -a

CONTAINER ID        IMAGE               COMMAND        CREATED             STATUS                     PORTS     NAMES
4f496dbb8048        windowsservercore   "cmd"          2 minutes ago       Exited (0) 2 minutes ago             dockerdemo
``` 

### 步骤 2-创建一个新的集装箱图像

现在可从这个容器的图像。

要创建一个新的映像运行下面的命令。

``` PowerShell
docker commit dockerdemo newcontainerimage
```

若要查看主机上的所有图像，请运行码头工人图像。

``` PowerShell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
newcontainerimage   latest              4f8ebcf0a334        2 minutes ago       9.613 GB
windowsservercore   latest              9eca9231f4d4        30 hours ago        9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        30 hours ago        9.613 GB
```

### 第 3 步-从图像创建新的容器

现在，你有一个自定义容器形象，部署新的容器，命名为 'newcontainer' 从 'newcontainerimage' 和打开容器与交互式 shell 会话。

``` PowerShell
docker run –it --name newcontainer newcontainerimage cmd
```

看看这个新的容器的 c:\ 驱动器并注意 ipconfig.txt 文件是本。

退出的新创建的容器返回到容器主机控制台会话。

``` PowerShell
exit
```

这个练习显示图像取自改装过的集装箱将包括所有的修改。虽然这里的例子是简单的文件修改，这同样适用如果您要将软件安装到 web 服务器等容器。

### 第 4 步-删除容器和图像

若要删除容器后就不再需要使用 '码头 rm' 命令。

``` PowerShell
docker rm newcontainer
```
若要删除容器图像，当他们不再需要使用 '码头 rmi' 命令。

下面的命令移除命名为 'newcontainerimage' 的集装箱图像。
``` PowerShell
docker rmi newcontainerimage

Untagged: newcontainerimage:latest
Deleted: 4f8ebcf0a334601e75070a92294d993b0f182abb6f4c88740c75b05093e6acff
```

## 主机在一个容器中的 Web 服务器

下一个例子将展示一个更实际的用例为 Windows 服务器容器。

### 第 1 步-下载 Web 服务器软件

在创建容器图像 web 之前服务器软件将需要下载和容器主机上上演。Windows 软件对于这个示例，我们将使用 nginx。* * 注意 * * 这一步将要求容器主机连接到互联网。

在集装箱主机创建将用于本示例的目录结构上运行下面的命令。

``` PowerShell
mkdir c:\build\nginx\source
```

在容器主机下载到 'c:\nginx-1.9.3.zip' nginx 软件上运行此命令。

``` PowerShell
wget -uri 'http://nginx.org/download/nginx-1.9.3.zip' -OutFile "c:\nginx-1.9.3.zip"
```

最后下面的命令将提取 nginx 软件到 'C:\build\nginx\source'。 

``` PowerShell
Expand-Archive -Path C:\nginx-1.9.3.zip -DestinationPath C:\build\nginx\source -Force
```

### 步骤 2-创建 Web 服务器映像
在前面的示例中，您手动创建、 更新和俘获容器图像。此示例将演示创建容器图像使用 Dockerfile 的自动化的方法。Dockerfiles 包含指令码头引擎用来生成和修改容器和容器然后提交一个容器的形象。
有关 dockerfiles，详细信息请参见 [Dockerfile 参考] (https://docs.docker.com/reference/builder/)。

使用以下命令来创建空的 dockerfile。

``` PowerShell
new-item -Type File c:\build\nginx\dockerfile
```
用记事本打开 dockerfile。

```
notepad.exe c:\build\nginx\dockerfile
```

复制并将以下文本粘贴到记事本中，保存文件并关闭记事本。

``` PowerShell
FROM windowsservercore
LABEL Description="nginx For Windows" Vendor="nginx" Version="1.9.3"
ADD source /nginx
```

在这一点上的 dockerfile 将在 'c:\build\nginx' 和 nginx 软件提取到 'c:\build\nginx\source'。
你现在准备好建立 web 服务器容器图像基于 dockerfile 中的说明操作。

``` PowerShell
docker build -t nginx_windows C:\build\nginx
```
此命令指示码头引擎使用位于 'C:\build\nginx' dockerfile 来创建名为 nginx_windows 的图像。

输出将类似于这样:

![] (media/docker1.png)

当完成时，看看图像对主机使用 '码头图像命令。您应该看到名为 nginx_windows 的新形象。
``` PowerShell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE

nginx_windows       latest              d792268338d0        5 seconds ago       9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        35 hours ago        9.613 GB
windowsservercore   latest              9eca9231f4d4        35 hours ago        9.613 GB
```

### 步骤 3 – 为容器应用程序中配置网络
因为你将会举办一个容器内的网站几个网络相关的配置需要进行。第一次的防火墙规则需要将允许网站访问容器主机上创建。在这个例子中我们将访问该网站通过端口 80。运行下面的脚本来创建此防火墙规则。 

``` powershell
if (!(Get-NetFirewallRule | where {$_.Name -eq "TCP80"})) {
    New-NetFirewallRule -Name "TCP80" -DisplayName "HTTP on TCP/80" -Protocol tcp -LocalPort 80 -Action Allow -Enabled True
}
```

下一步如果您正在从 Azure 并不已经创建了一个虚拟机端点将需要创建一个现在。在 Azure VM 终结点上的详细信息请参阅这篇文章: [设置 Azure VM 端点] (https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/)。

### 第 4 步-部署 Web 服务器准备好容器

要部署基于 'nginx_windows' 的 Windows 服务器容器容器运行下面的命令。这将创建一个名为 'nginxcontainer' 的新容器，在容器上启动控制台会话。 

``` powershell
docker run -it --name nginxcontainer -p 80:80 nginx_windows cmd
```
一旦工作在容器内，可以启动 nginx web 服务器和 web 内容上演。

``` powershell
cd c:\nginx\nginx-1.9.3
```

启动 nginx web 服务器。
``` powershell
start nginx
```
### 第 5 步 – 访问容器承载的网站

使用创建的 web 服务器容器，您可以现在结帐容器中承载的应用程序。要这样做，打开另一台计算机上的浏览器并输入 'http://containerhost-ipaddress'。请注意在这里，您将浏览到容器主机和不是容器本身的 IP 地址。 

如果一切都已正确配置，您将看到 nginx 的欢迎页面。

![] (media/nginx.png)

在这一点上，随时更新网站。

```powershell
powershell wget -uri 'https://raw.githubusercontent.com/Microsoft/Virtualization-Documentation/master/doc-site/virtualization/windowscontainers/quick_start/SampleFiles/index.html' -OutFile "C:\nginx\nginx-1.9.3\html\index.html"
```

在更新该网站后，导航回 'http://containerhost-ipaddress'。

![] (media/hello.png)

> * * 请注意: * * 如果你想要改变的码头工人守护程序设置 (例如，更改它侦听的端口，远程连接到一个容器)，您将需要在容器中，编辑"C:\ProgramData\docker\runDockerDaemon.cmd"文件，然后您将需要重新启动服务与 PowerShell 使用 '' 请重新启动服务码头 ' '。

## 视频演练

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Deploying-and-Managing-Windows-Server-Containers-with-Docker/player" width="800" height="450"  allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>

## 接下来的步骤
现在，你有容器设置和介绍的工具，去建立自己的容器应用程序。

请记住，这是 * * 预览 * * 有 bug，我们有很多的工作进展。[此页](../ about/work_in_progress.md) 包含了许多我们已知的问题。

意识到有一些已知的码头命令，[不工作] (.../ about/work_in_progress.md#DockermanagementDockercommandsthatdontworkwithWindowsServerContainers) 和一些，只有 [部分工作] (.../ about/work_in_progress.md#DockermanagementDockercommandsthatpartiallyworkwithWindowsServerContainers)

我们也非常密切地监测 [论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。

[GitHub] (https://github.com/Microsoft/Virtualization-Documentation/tree/master/windows-server-container-samples) 上也有预先制作的样品。

-----------------------------------
[回容器首页](../ containers_welcome.md) [为当前版本中的已知问题] (.../ about/work_in_progress.md)