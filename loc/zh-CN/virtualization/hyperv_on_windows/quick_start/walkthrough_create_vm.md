# 第 4 步: 创建一个 Windows 虚拟机从一个.iso 文件 

对于这一步，如果你已经有了一个.iso 文件为受支持的 64 位操作系统，你可以使用的。如果不是，你可以下载.iso [8.1 Windows 企业] (http://www.microsoft.com/en-us/evalcenter/evaluate-windows-8-1-enterprise)，选择 64 位版。 

1. 在 HYPER-V 管理器中，单击的 * * 行动 * * 菜单 > * * 新 * * > * * 虚拟机 * *。 
2. 在虚拟机向导中，请使用以下选项:

    <table>
    <tr><th>Page</th><th>Entry</th></tr>
    <tr><td>Name:</td><td>Type in <b>Windows Walkthrough VM</b></td></tr>
    <tr><td>Generation:</td><td><b>Generation 2</b></td></tr>
    <tr><td>Startup Memory:</td><td><b>1024</b> and leave dynamic memory selected</td></tr>
	<tr><td>Configure Networking:</td><td><b>External</b> (this is the virtual switch you created in Step 3)</td></tr>
    <tr><td>Connect virtual hard disk:</td><td><b>Create a virtual hard disk</b> (keep the other default values) </td></tr>
    <tr><td>Installation Options:</td><td><b>Install an operating system from a bootable CD/DVD-ROM</b>. Under <b>Media</b>, select <b>Image file (iso)</b> and then click <b>Browse</b> to point to the .iso file.</td></tr>
    </table>
  
3. 当一切看起来都正确时，请单击 * * 完成 * *。 

> * * 请注意: * * 如果你只有 32 位版本的 Windows，您需要选择在代 1 * * 代 * * 的向导一节。

## 下一步: 
[第 5 步: 连接到虚拟机并完成安装]() walkthrough_vmconnect.md

