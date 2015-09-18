<!--Reviewed by liwer 7/8/15 -->
# Export and Import virtual machines
You can use the export and import functionality to quickly duplicate virtual machines or to move them from one host to another.
You don't need to export a virtual machine to be able to import it. You can simply copy a virtual machine and its associated files to the new host, and then use the **Import Virtual Machine** wizard to specify the location of the files. This registers the virtual machine with Hyper-V and makes it available to be used.

## 导出虚拟机
准备要导入的虚拟机的简单方法是 * * 导出虚拟机 * * 向导。

1. 在 HYPER-V 管理器中，选择一个或多个虚拟机，用鼠标右键单击您的选择和选择 * * 出口 * *。
2. 单击 * * 浏览 * * 在对话框中框中，选择您想要导出的 VM，然后单击哪里 * * 选择文件夹 * *。
3. 在 * * 导出虚拟机 * * 对话框中，单击 * * 出口 * *。

有关使用 Windows PowerShell 导出虚拟机的信息，请参阅 [出口-VM] (https://technet.microsoft.com/library/hh848491.aspx)

## 导入虚拟机
1. 在 * * HYPER-V 管理器 * *，* * 行动 * * 菜单，单击 * * 导入虚拟机 * *。
2. 在查找文件夹部分中，单击浏览，导航到虚拟机文件位于何处。<! — — 要检查这是否是解决 — — 这种行为是从我的角度--> 请注意，使用该向导你可以一次导入一个 VM，不得不选择虚拟机的文件夹而不是一般的输出文件夹中的 bug。单击 * * 下一步 * * 时完成。
3. 选择虚拟机导入，然后单击 * * * * 下一步。
4. 在选择导入类型部分中，您可以选择如何导入虚拟机:
  -  * * 注册 * *-使用现有的唯一 ID 的虚拟机并将其在地方注册。
  - * * 还原 * *-使用原始虚拟机的唯一 ID，也会将虚拟机文件复制到指定的主机的默认位置。
  - * * 副本 * *-创建新的唯一 ID 的虚拟机，也会将虚拟机文件复制到指定的主机的默认位置。

5. 选择后如何导入虚拟机，请单击 * * * * 下一步。
6. 在选择目标部分中，您可以选择在何处存储虚拟机的文件，或把它们留在它们的当前位置。当你完成时，单击 * * * * 下一步。
7. 在选择存储文件夹中，您可以选择另一个位置存储.vhdx 文件或离开他们他们在哪里。当你完成时，单击 * * * * 下一步。
8. 完成导入虚拟机后，你会看到摘要页描述新的 VM 文件位于何处。

导入虚拟机向导还引导您完成步骤解决不兼容性，将虚拟机导入到新的主机的时候 — — 所以此向导可以帮助与物理硬件，如内存、 虚拟交换机和虚拟处理器相关联的配置。

要导入的虚拟机，该向导将执行以下操作:
1. 创建虚拟机配置文件的一个副本。
2. 验证硬件。
3. 编译错误的列表。
4. 显示相关的网页，一次一个类别。
5. 删除配置文件的副本。

向导，除了 Windows PowerShell 的 HYPER-V 模块包括 cmdlet 用于导入的虚拟机。更多的信息，请参阅 [导入 VM] (https://technet.microsoft.com/library/hh848495.aspx)。