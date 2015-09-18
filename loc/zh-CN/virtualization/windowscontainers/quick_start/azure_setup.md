ms。ContentId: 1ab7bfe1-da35-4ff1-916f-936fedf536a0
标题: 安装 Windows Azure 中的容器

# 微软 Azure 准备 Windows 服务器容器

之前创建和管理 Windows 服务器容器在 Azure 中您将需要部署已预先配置的 Windows 服务器容器功能的 Windows 服务器 2016年技术预览图像。

> 其他入门指南:
  * 在 [新的 HYPER-V 虚拟机] 中运行 Windows 服务器容器 (./container_setup.md)。
  * 在 [现有的虚拟机] 中运行 Windows 服务器容器 (./inplace_setup.md)
  * [关于物理的 Windows 服务器核心安装] 安装 Windows 服务器容器 (./inplace_setup.md)

## 开始使用 Azure 门户
如果你有一个蔚蓝的帐户，跳过直以 [创建容器主机 VM](#CreateacontainerhostVM)。

1. 转到 [azure.com] (https://azure.com) 并按照步骤为 [Azure 免费试用] (https://azure.microsoft.com/en-us/pricing/free-trial/)。
2. 使用您的 Microsoft 帐户登录。
3. 当您的帐户是准备去时，登录到 [Azure 管理门户] (https://portal.azure.com)。

## 创建容器主机 VM

单击以下链接以启动 VM 创建过程 — — [新 Windows 服务器容器主机在 Azure] (https://portal.azure.com/#gallery/Microsoft.WindowsServer2016TechnicalPreviewwithContainers)。 

您还可以搜索蔚蓝的库中的图像。

单击创建按钮。

![] (./ media/newazure1.png)

给虚拟机的名称，选择一个用户名和密码。

![] (media/newazure2.png)

选择可选配置 > 终结点 > 和输入 HTTP 端点与私人和公共的 80 端口，如下图所示。

![] (./ media/newazure3.png)

选择创建按钮以启动虚拟机部署过程。

![] (media/newazure2.png)

VM 部署完成后，选择连接按钮来启动 Windows 服务器容器主机与 RDP 会话。

![] (media/newazure6.png)

登录使用的用户名和密码在 VM 创建向导中指定的 VM。

![] (media/newazure7.png) 

## 视频演练

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Configure-Windows-Server-Containers-in-Microsoft-Azure/player" width="800" height="450"  allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>


## 下一步-开始使用容器

现在，你有一个 Windows 服务器 2016年系统运行 Windows 服务器容器功能跳转到以下指南开始使用 Windows 服务器容器和 Windows 服务器容器的图像。 

[快速启动: Windows 服务器容器和码头工人](./ manage_docker.md) 
[快速启动: Windows 服务器容器和 PowerShell](./ manage_powershell.md) 

-------------------
[回容器首页](../ containers_welcome.md) [为当前版本中的已知问题] (.../ about/work_in_progress.md)