ms。ContentId: 44b138bb-962f-4474-a0c4-284646a872e2
标题: 安装 Windows 容器到位

# 准备 Windows 服务器容器中的物理计算机或现有的虚拟机


为创建和管理 Windows 服务器容器，必须编写 Windows 服务器 2016年技术预览环境。 

> 其他入门指南:
  * [Azure] (./azure_setup.md) 中运行 Windows 服务器容器。
  * 在 [新 HYPER-V 虚拟机] 中运行 Windows 服务器容器 (./container_setup.md)。

  * * 请阅读安装容器 OS 映像之前: * * ("许可条款") Microsoft Windows 服务器预发行软件的许可条款适用于您使用 Microsoft Windows 容器 OS 映像补充 ("辅助软件)。下载和使用辅助软件，您同意许可条款，且你不可能使用它，如果你还不接受许可协议条款。  

* * 系统 (或 VM) 要求: * *
* 运行 Windows 服务器技术预览 3 服务器核心的系统。
* 10 GB 可用存储为 OS 基础映像和安装程序脚本的。
* 计算机或虚拟机上的管理员权限。

## 设置容器现有虚拟机或裸露的金属主机
Windows 服务器容器需要容器 OS 基础映像。我们已经把一个脚本，将下载并安装此为你。

以管理员身份启动 PowerShell 会话。

``` powershell
powershell.exe
```

请确保 windows 的标题是"管理员: Windows PowerShell"。

``` powershell
start-process powershell -Verb runas
```

使用下面的命令来下载安装脚本。此外可以把脚本手动从这个位置 — — [配置脚本] (http://aka.ms/setupcontainers) 下载。
 
``` PowerShell
wget -uri https://aka.ms/setupcontainers -OutFile C:\ContainerSetup.ps1
```
   
 下载完成后，执行该脚本。
``` PowerShell
C:\ContainerSetup.ps1
```

该脚本将然后开始下载和配置 Windows 服务器容器组件。此过程可能需要很长一段时间由于大下载。这台机器可能会在过程中重新启动。 

 完成这些项目与您的系统应该准备 Windows 服务器容器。 


## 下一步-开始使用容器

现在，你正在运行 Windows 服务器容器，跳转到以下指南开始使用 Windows 服务器容器和 Windows 服务器容器的图像。 
 
[快速启动: Windows 服务器容器和码头工人](./ manage_docker.md) 

[快速启动: Windows 服务器容器和 PowerShell](./ manage_powershell.md) 

-------------------

[回容器首页](../ containers_welcome.md) [为当前版本中的已知问题] (.../ about/work_in_progress.md)