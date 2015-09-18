ms。ContentId: 4981828d-1a08-4d8c-a99d-874a926a153f
标题: PowerShell 到码头比较

# PowerShell 到码头比较用于管理 Windows 服务器容器

有很多的方法来管理 Windows 服务器容器使用 Windows 工具框中 (在此预览 PowerShell) 和开放源代码管理工具，例如码头。 
这里概述了这两个人可得到的指南:
* [管理 Windows 服务器容器多克](../ quick_start/manage_docker.md)
* [管理 Windows PowerShell 的服务器容器](../ quick_start/manage_powershell.md) 

此页面是在深度参照比较多克工具和 PowerShell 管理工具。

## PowerShell 的容器与 HYPER-V 虚拟机
您可以创建、 运行和与使用 PowerShell cmdlet 的 Windows 服务器容器进行交互。

如果您已经使用 HYPER-V PowerShell，cmdlet 的设计应该是非常熟悉的你。大量的工作流是类似于你将如何管理虚拟机使用 HYPER-V 模块。而不是 '新 VM'、' Get VM'、 '开始-VM'、' 停止 VM'，你有 ' 新-容器 '，' Get-集装箱 '，' 开始-集装箱 '，' 停止货柜的。

## PowerShell 管理与码头工人如何比较? 
容器 PowerShell cmdlet 公开的 API，并不是完全一样的码头;作为一般规则，这些 cmdlet 都更细粒度的操作。

|码头工人命令 |	PowerShell Cmdlet |
|----|----|
|' 码头 ps-a' |'获取容器' |
|码头工人图像' |' 获取-ContainerImage' |
|码头工人 rm' |'删除容器' |
|码头工人 rmi' |' 删除-ContainerImage' |
|码头工人创建 |' 新货柜的 |
|码头工人提交<container id="">' | '新 ContainerImage-容器<container>' |
|码头工人负载<tarball>' | '导入 ContainerImage <AppX package="">' |
|'保存码头' |	' 出口-ContainerImage' |
|码头工人开始 |	' 开始-货柜的 |
|'码头站' |	' 停止货柜的 |</AppX></tarball></container></container>

PowerShell cmdlet 并不是确切的完美奇偶校验，有相当多的命令，我们不会提供 PowerShell 的替换 * (尤其是 '码头建设' 和 '码头 cp')。但什么可能会跳出来，你就是没有单一的一线替换为跑码头。

\ * 如有更改。

### 但我需要码头运行!这是怎么回事？  
我们做一对夫妇的事情在这里稍微熟悉的交互模型为用户提供已经知道他们周围 PowerShell 的方式。

1.	在 PowerShell 模型容器的生命周期是略有不同。在容器 PowerShell 模块中，我们公开 '新货柜的 (这将创建一个新的容器，停止) 和' 开始-货柜的更细粒度的操作。
  
  在创建和启动容器，您还可以配置容器的设置;对于 TP3，我们打算去揭露的其他配置只是设置容器的网络连接的能力。

2.	你目前不能通过上运行，在容器内开始的命令。然而，你仍然可以对正在运行的容器，使用 'enter 键-PSSession-ContainerId <ID of="" a="" running="" container="">' PowerShell 的交互式会话，可以执行命令里面运行的容器使用 '调用命令-ContainerId <container id="">-简言之 {代码运行在容器内}' 或' 调用命令-ContainerId <container id="">-FilePath <path to="" script="">'。 
两条命令允许可选 '-RunAsAdministrator' 高特权操作标志。</path> </container> </container> </ID>  


## 注意事项和已知的问题
1.  现在，容器 cmdlet 有关于任何容器或图像创建通过码头工人，没有知识和码头工人不知道任何关于容器和通过 PowerShell 创建的图像。

2.  我们有相当多的工作，我们想要改善最终用户体验 — — 更好的错误消息、 好进度报告、 无效事件字符串，等等。

## 快速的 runthrough
这里是步行穿过的一些常见的工作流程。

这假定您已经安装 OS 容器映像命名为"ServerDatacenterCore"并创建了一个名为"虚拟交换机"(使用新 VMSwitch) 的虚拟交换机。

``` PowerShell
### 1. Enumerating images
# At this point, you can enumerate the images on the system:
Get-ContainerImage

# Get-ContainerImage also accepts filters.
# For example, this will return all container images whose Name starts with S (case-insensitive):
Get-ContainerImage -Name S*

# You can save the results of this to a variable.
# (If you're not familiar with PowerShell, the "$" denotes a variable.)
$baseImage = Get-ContainerImage -Name ServerDatacenterCore
$baseImage

### 2. Creating and enumerating containers
# Now, we can create a new container using this image:
New-Container -Name "MyContainer" -ContainerImage $baseImage -SwitchName "Virtual Switch"

# Now we can enumerate all containers.
Get-Container

# Similarly, we can save this container to a variable:
$container1 = Get-Container -Name "MyContainer"

### 3. Starting containers, interacting with running containers, and stopping containers
# Now let's go ahead and start the container.
Start-Container -Name "MyContainer"

# (We could've also started this container using "Start-Container -Container $container1".)

# With the container now running, let's go ahead and enter an interactive PowerShell session:
Enter-PSSession -ContainerId $container1.Id

# This should eventually bring up a PowerShell prompt from inside the container.
# You can try all the things that you did in the interactive cmd prompt given by "docker run -it".
# For now, just to prove we've been here, we can create a new file:
cd \
mkdir Test
cd Test
echo "hello world" > hello.txt
exit

# Now we should be back in the outside world. Even though we've exited the PowerShell session,
# the container itself is still running, as you can see by printing out the container again:
$container1

# Before we can commit this container to a new image, we need to stop the container.
# Let's do that now.
Stop-Container -Container $container1

### 4. Creating a new container image
# And now let's commit it to a new image.
$image1 = New-ContainerImage -Container $container1 -Publisher Test -Name Image1 -Version 1.0

# Enumerate all the images again, for sanity's sake:
Get-ContainerImage

# Rinse and repeat! Make another container based on the new image.
$container2 = New-Container -Name "MySecondContainer" -ContainerImage $image1 -SwitchName "Virtual Switch"

# (If you like, you can start the second container and verify that the new file
# "\Test\hello.txt" is there as expected.)

### 5. Removing a container
# The first container we created is now stopped. Let's get rid of it:
Remove-Container -Container $container1

# And confirm that it's gone:
Get-Container

### 6. Exporting, removing, and importing images
# For images that aren't the base OS image, we can export them into an .appx package file.
Export-ContainerImage -Image $image1 -Path "C:\exports"
# This should create a .appx file in the C:\exports folder.
# If you've given your image the same publisher, name, and version we used earlier,
# you'd expect the resulting .appx to be named "CN=Test_Image1_1.0.0.0.appx".

# Before we can try importing the image again, we need to remove the image.
# (If you have any running containers that depend on this image, you'll want to stop them first.)
Remove-ContainerImage -Image $image1

# Now let's import the image again:
Import-ContainerImage -Path C:\exports\CN=Test_Image1_1.0.0.0.appx

# We'd previously created a container dependent on this image. You should be able to start it:
Start-Container -Container $container2 
```

### 建立您自己的示例
你可以看到所有容器 cmdlet 使用 ' Get 命令-模块容器。有几个其他 cmdlet 的介绍不在这里，而我们会留给你，了解你自己。   
**Note** 这不会返回 Enter PSSession' 和 '调用命令' cmdlet，是核心 PowerShell 的一部分。

您还可以使用获取帮助 [cmdlet 名称]'，任何 cmdlet 的帮助或等价地 '[cmdlet 名称]-?'。

更好的方式来发现语法是 PowerShell ISE，你可能没有之前看过如果你还没有使用 PowerShell 非常多。

PS: 只是 cmdlet 的为了证明这是 cmdlet 的可以做到，这里是 cmdlet 的撰写一些我们已经看过了到代用品跑码头 PowerShell 功能。

``` PowerShell
function Run-Container ([string]$ContainerImageName, [string]$Name="fancy_name", [switch]$Remove, [switch]$Interactive, [scriptblock]$Command) {
    $image = Get-ContainerImage -Name $ContainerImageName
    $container = New-Container -Name $Name -ContainerImage $image
    Start-Container $container

    if ($Interactive) {
         Start-Process powershell ("-NoExit", "-c", "Enter-PSSession -ContainerId $($container.Id)") -Wait
    } else {
        Invoke-Command -ContainerId $container.Id -ScriptBlock $Command
    }

    Stop-Container $container

    if ($Remove) {
        Remove-Container $container -Force
    }
} 
```

## 码头工人
Windows 服务器容器可以管理与码头工人命令。虽然 Windows 容器应相当于 Linux 的同行和有相同的管理经验通过码头工人，有一些码头命令，简直毫无意义与 Windows 容器。

为了不重复的 API 文档提供的码头，这里是一个链接到他们的管理 Api。

我们追踪并不在我们的进展中的工作文件中的码头工人 Api 工作的事情。