# PowerShell 片段

PowerShell 是令人敬畏脚本，自动化和管理工具对 HYPER-V。这里是一个工具箱，探索一些很酷的事情，它可以做!

所有 HYPER-V 管理都需要运行管理员所以假设所有脚本和代码片段从一个 HYPER-V 管理员帐户，必须以管理员身份运行。

如果你不能确定的如果你有正确的权限，请键入 ' Get VM'，如果它运行，无任何错误，你准备好去。


## PowerShell 直接工具
所有脚本和本节中的代码段将依靠以下基本知识。

* * 要求 * *:  
*  PowerShell 直接。

* * 常用变量 * *: '$VMName' — — 这是 VMName 的字符串。看到 ' Get-VM' '$cred' — — 访客操作系统凭据的可用虚拟机的列表。可以使用填充 ' $cred = 获取凭据 '  

### 检查客人是否已启动

HYPER-V 管理器不会给你往往使得它很难知道是否访客操作系统已启动来宾操作系统的可视性。

使用此命令可以检查客人是否已启动。

``` PowerShell
if((Invoke-Command -VMName $VMName -Credential $cred {"Test"}) -ne "Test"){Write-Host "Not Booted"} else {Write-Host "Booted"}
```  

* * 结果 * * 打印一条友好消息宣布的访客操作系统状态。


### 锁定直到客人已启动脚本

下面的函数等待的采用相同的原则，要等到 PowerShell 是可用在客人 (即启动操作系统和大多数服务都在运行)，然后返回。

``` PowerShell
function waitForPSDirect([string]$VMName, $cred){
   Write-Output "[$($VMName)]:: Waiting for PowerShell Direct (using $($cred.username))"
   while ((Invoke-Command -VMName $VMName -Credential $cred {"Test"} -ea SilentlyContinue) -ne "Test") {Sleep -Seconds 1}}
```

* * 结果 * * 打印友好的消息，直到连接到 VM 锁成功。 
默默地成功。

### 锁定直到客人有一个网络的脚本
与 PowerShell 直接就可以获得连接到虚拟机虚拟机前内部 PowerShell 会话已获得 IP 地址。

``` PowerShell
# Wait for DHCP
while ((Get-NetIPAddress | ? AddressFamily -eq IPv4 | ? IPAddress -ne 127.0.0.1).SuffixOrigin -ne "Dhcp") {sleep -Milliseconds 10}
```

* * 结果 * *
锁定，直到收到 DHCP 租约。因为此脚本并不是为一个特定的子网或 IP 地址，它工作无论何种网络配置使用。 
默默地成功。

## 与 PowerShell 的管理凭据
超 V 脚本经常需要处理一个或多个虚拟机，HYPER-V 主机，或这两种凭据。

有多种方法可以完成此工作时使用 PowerShell 直接或远程处理 PowerShell 标准:

1. 第一个 (最简单) 的方法是有相同的用户凭据在主机和来宾或本地和远程主机有效。 
  如果您使用您的 Microsoft 帐户-登录，或者如果你是在域环境中，这是很容易的。 
  在这种情况下您可以只运行 ' 调用命令 VMName"测试"{get 过程}'。

2. 让的 PowerShell 提示你如果您的凭据不匹配您的凭据将自动获得凭据提示允许您为虚拟机提供相应的凭据。

3. 将凭据存储在一个变量中重用。
  运行一个简单的命令，像这样:  
  ``` PowerShell
  $localCred = Get-Credential
   ```
  然后运行这样的事情:
  ``` PowerShell
  Invoke-Command -VMName "test" -Credential $localCred  {get-process} 
  ```
  将的意思是，你只得到提示每次您的凭据的脚本/PowerShell 会话。

4. 进入您的脚本代码您的凭据。* * 为任何实际工作负载或系统 * * 不做这
 > 警告: 竭尽不做这在生产系统中。不这样做与真实密码。 _
  
  你能不能交手工创建一个 PSCredential 对象，这样的代码:  
  ``` PowerShell
  $localCred = New-Object -typename System.Management.Automation.PSCredential -argumentlist "Administrator", (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force) 
  ```
  严重的不安全感 — — 但有用的测试。 

