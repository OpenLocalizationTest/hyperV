# 第 2 步: 在 Windows 10 上安装超 V

超 V 可以安装使用 [程序和 Features](#UsingProgramsandFeatures) 或 [Windows Powershell](#UsingPowerShell)。

## 使用程序和功能
1. 用鼠标右键单击 * * Windows * * 按钮，然后单击 * * 程序和功能 * *。

  ![] (media\programs_and_features.png)
  
2. 单击 * * 打开或关闭 Windows 功能 * *。

3. 选择 * * 超-V * *，请单击 * * 好 * *

  ![] (media\hyper-v_feature_selected.png)
  
4. 完成安装后，您将需要重新启动计算机。

  ![] (media\restart.png)
  
## 使用 PowerShell
有关详细信息，请参阅 [启用-WindowsOptionalFeature] (https://technet.microsoft.com/library/hh852172.aspx) PowerShell 帮助。

1. 单击 * * Windows * * 按钮并搜索 * * Windows PowerShell * *。  
2. 用鼠标右键单击 * * Windows PowerShell * *，然后单击 * * 作为管理员 * * 运行。  
3. 在 Windows Powerhshell 提示符下，键入以下命令，然后按 * * 输入 * * 键:  
``` PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
``` 
4. 完成安装后，重新启动计算机。 

## 怎么知道 HYPER-V 已正确安装?
在你之后重新启动计算机启动 HYPER-V 管理器工具。 

1. 单击 * * Windows * * 按钮，并键入 * * 超-V * *。
2. 单击 * * HYPER-V 管理器 * * 在列表中。
3. HYPER-V 管理器应用程序将启动。


## 下一步 
[第 3 步: 创建一个虚拟交换机]() walkthrough_virtual_switch.md 