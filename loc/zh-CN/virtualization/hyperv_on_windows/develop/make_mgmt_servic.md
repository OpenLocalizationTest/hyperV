# 使新的管理服务 #
本文档介绍了 VM 服务建立在 HYPER-V 套接字和如何开始使用它们。

![](../ media/1.png)

## 虚拟机服务是什么?
虚拟机服务是跨越 HYPER-V 主机和主机上运行的虚拟机的服务。

HYPER-V 现在 (Windows 10 和服务器 + 2016年) 提供非网络连接使您能够创建跨越主机/虚拟机边界，同时保留 HYPER-V 的基本要求周围房客/宿主隔离、 控制，服务和诊断。

超 V 将继续提供一组基本的框中服务 (集成服务) 的基本要素 (比如时间同步) 并为共同请我们收到，但现在任何人都可以编写和部署 VM 服务所需。

PowerShell 直接是 VM 服务在框示例。

## HYPER-V 的套接字是什么?
超 V 套接字是类似 TCP 套接字的不依赖于网络。

## 系统要求

* * 受支持的主机操作系统 * *
*	Windows 10
*	Windows 服务器技术预览版 3
*	将来的版本 (2016 服务器 +)

* * 受支持的来宾操作系统 * *
*	Windows 10
*	Windows 服务器技术预览版 3
*	将来的版本 (2016 服务器 +)
*	Linux

## 功能和局限性
内核模式或用户模式数据流只没有块内存所以不是最好的备份/视频  

## 入门

本指南假定您熟悉使用套接字在 C/c + + 编程。

### 第 1 步-注册您的 HYPER-V 主机上的服务
为了使用与 HYPER-V 集成的自定义服务，必须与 HYPER-V 主机注册表注册新服务。

通过在注册表中注册该服务，您可以:
*  WMI 管理启用、 禁用和列出可用的服务
*  上的服务列表允许直接与虚拟机通信。

* * 注册表位置和信息 * *  

``` 
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Virtualization\VirtualDevices\6C09BB55-D683-4DA0-8931-C9BF705F6480\GuestCommunicationServices\
```
在此注册表位置，你会看到几个 GUID。

每个服务注册表中的信息:
* ' 服务 GUID'   
    * 无法识别 (REG_SZ)' — — 这是服务的友好名称

要注册您自己的服务，请创建一个新的注册表项，使用您自己的 GUID 和友好名称。

注册表项将如下所示:
```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Virtualization\GuestCommunicationServices\
    999E53D4-3D5C-4C3E-8779-BED06EC056E1\
	    ElementName	REG_SZ	VM Session Service
    YourGUID\
	    ElementName	REG_SZ	Your Service Friendly Name
```

> * * 提示: * * 要在 PowerShell 生成一个 GUID，并将其复制到剪贴板，请运行:  
``` PowerShell
[System.Guid]::NewGuid().ToString() | clip.exe
```

<!-- How do customers know this worked -->

### 步骤 2-创建一个简单的主机端服务



### 第 3 步-创建一个简单的客户端服务

## 有关 AF_HYPERV 的详细信息
由于 HYPER-V 套接字不依赖于网络的堆栈，TCP/IP，DNS，等。套接字终结点需要非 IP 不是主机名，仍然描述连接的格式。而不是 IP 或主机名，AF_HYPERV 端点严重依赖于两个 GUID:  
* VM ID — — 这是每个虚拟机分配的唯一 ID。
```PowerShell
(Get-VM -Name vmname).Id
```
* 服务 ID – 下服务在 HYPER-V 主机注册表中注册的 GUID。请参阅 [注册新的 Service](#GettingStarted)。

从上到上一个 VM 的服务主机的服务连接: VMID 和服务 ID
从虚拟机上的服务连接到主机上的服务: 零 GUID 和服务 ID

## 支持套接字命令

Socket()
Bind()
连接)
Send)
Listen()
Accept)


 
