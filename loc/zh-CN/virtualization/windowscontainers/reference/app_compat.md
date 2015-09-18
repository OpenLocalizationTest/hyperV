ms。ContentId: 3fdd690d-4259-4066-8781-360bb0554512
标题: 运行程序在 Windows 容器

# 在 Windows 服务器容器的应用程序兼容性

是不是在此列表中?让我们知道什么失败和成功在您环境中通过 [论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。

## 哪些应用程序运行在 Windows 服务器容器

我们已经尝试在 Windows 服务器容器中运行以下应用程序。这些结果不能保证应用程序的工作。

|* * 名称 * * |* * 版本 * * |* * 它工作吗? * * |* * 注释 * * |
|:-----|:-----|:-----|:-----|
|.NET |3.5 |没有 |未能正确安装 |
|.NET |4.6 |是啊 |列入基本映像 |
|.NET CLR |5 β 6 |是啊 |同时，x 64 和 x86 |
|积极的 Python |3.4.1 |是啊 | |
|Apache CouchDB |1.6.1 |不 | |
|Apache HTTPD |2.4 |是啊 | |
|Apache Tomcat |8.0.24 x 64 |是啊 | |
|ASP.NET |3.5 |不 | |
|ASP.NET |4.5 |不 | |
|ASP.NET |5 β 6 |是啊 |同时，x 64 和 x86 |
|OTP |18.0 |不 | |
|FileZilla FTP 服务器 |0.9 |是啊 |已入容器通过 RDP 会话安装 |
|去编程语言 |1.4.2 |是啊 | |
|互联网信息服务 |10.0 |是啊 | |
|Java |1.8.0_51 |是啊 |使用的服务器版本。未正确安装的客户端版本 |
|码头 |9.3 |部分 |运行演示基地失败 |
|MineCraft 服务器 |1.8.5 |是啊 | |
|MongoDB |3.0.4 |是啊 | |
|MySQL |5.6.26 |是啊 | |
|NGinx |1.9.3 |是啊 | |
|Node.js |0.12.6 |部分 |Js 文件工程运行节点。新公共管理未能下载的软件包。以交互方式运行节点不能正常工作。|
|PHP |5.6.11 |部分 |与 Apache，IIS 通过 FastCGI 目前无法正常工作。|
|PostgreSQL |9.4.4 |是啊 | |
|Python |3.4.3 |是啊 | |
|R |3.2.1 |不 | |
|RabbitMQ |3.5.x |是啊 |已入容器通过 RDP 会话安装 |
|穿红衣的 |2.8.2101 |是啊 | |
|红宝石 |2.2.2 |是啊 |同时，x 64 和 x86 |
|Ruby 在轨道上 |4.2.3 |是啊 | |
|SQLite |3.8.11.1 |是啊 | |
|SQL 服务器快递 |2014 LocalDB |没有 | |
|Sysinternals 工具 |* |是啊 |只是试着那些不需要一个图形用户界面。 

## 我可以安装什么可选的 Windows 功能?

作为能安装方面证实了以下 Windows 可选功能。

* 广告证书
* 模数转换器证书权威
* 文件服务
 * FS 文件服务器
 * FS-VSS-代理
* DirectAccess VPN
* 路由
* 远程桌面服务
* VolumeActivation
* Web 服务器
* Web 服务器
* Web 普通 Http
* Web-默认-Doc
* Web 目录浏览
* Web Http 错误
* Web 静态内容
* Web-Http 重定向
* Web DAV 发布
* Web 健康
* Web Http 日志
* Web 自定义日志
* Web 日志库
* Web-ODBC 日志记录
* Web 请求监视器
* Web 性能
* 网站-Stat-压缩
* Web Dyn 压缩
* Web 安全
* 网页过滤
* Web-基本-身份验证
* Web CertProvider
* Web 客户端的身份验证
* Web-摘要-身份验证
* Web 证书验证
* Web IP 安全性
* Web Url 验证
* Web-Windows 身份验证
* Web 应用程序开发
* Web AppInit
* Web CGI
* Web ISAPI Ext
* Web-ISAPI 筛选器
* Web 包含
* Web Websocket
* Web 管理兼容
* Web 配置数据库
* BitLocker
* EnhancedStorage
* GPMC
* 隔离用户模式
* 服务器-媒体-地基
* MSMQ DCOM
* 多点-连接器-功能
* qWave
* RDC
* RSAT-特征-工具-BitLocker
* RSAT 聚类 PowerShell
* RSAT 聚类 AutomationServer
* RSAT 聚类 CmdInterface
* RSAT 屏蔽 VM 工具
* RSAT-AD-工具
* RSAT-广告-PowerShell
* RSAT 添加
* RSAT-广告-AdminCenter
* RSAT 添加工具
* RSAT ADLDS
* 超 V PowerShell
* UpdateServices API
* RSAT NetworkController
* Windows-面料-工具
* RSAT HostGuardianService
* 财政司司长 SMBBW
* 存储副本
* Telnet 客户端
* 是
 * 是过程模型
 * 是配置 Api
* Windows 服务器备份
* 迁移

是不是在此列表中?让我们知道什么失败和成功在您环境中通过 [论坛] (https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)。