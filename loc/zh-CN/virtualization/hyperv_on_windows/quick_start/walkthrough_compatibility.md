# 第 1 步: 确保你的机器可以运行 HYPER-V

只有 Windows 10 临和 Windows 10 企业支持 HYPER-V。

> 如果您正在运行 Windows 10 首页--你可以升级到赢得 10 临在激活页面位于安全设置。

超 V 不是可用在 Windows 10 移动 / Windows 10 移动企业

HYPER-V 需要至少 4 GB 的 RAM，但你可能需要更多，如果你想要同时运行多个虚拟机。

启动在 Windows 10，HYPER-V 需要 64 位处理器与翻译 (金属板) 的第二层地址。

## 验证硬件兼容性

若要验证兼容性，打开 PowerShell 或 Windows 命令提示符 (cmd.exe) 和类型: 'systeminfo.exe'。

所有项下 * * HYPER-V 要求 * * 必须具有值如果 * * 是 * *。

! [] (media\systeminfo.PNG)

有关各节:
*  OS 名称 — — 必须是 Windows 8 或更高和行业或企业。
*  HYPER-V 要求 — — 所有这些必须是 true (值为"Yes")，但一些可以在 BIOS 中配置。
	*  虚拟机监视器模式扩展 — — 硬件属性。
	*  虚拟化在固件中启用 — — 可以在 BIOS 中启用
	*  '第二层地址翻译' — — 硬件属性。
	*  '预防数据执行可用' — — 可以在 BIOS 中启用
	
如果已经启用 HYPER-V，HYPER-V 要求节会阅读:  
```
Hyper-V Requirements: A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```

## 下一步: 
[第 2 步: 安装超 V]() walkthrough_install.md