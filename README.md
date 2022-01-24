
# TDH Collector Desktop 使用手册

**适用版本：1.0.0**

**编写时间：2022-01-24**

**更新时间：2022-01-24**

----

## 什么是 TDH Collector Desktop

TDH Collector Desktop 是一款适配 Transwarp Data Hub （即 TDH）集群的运维辅助工具。TDH Collector Desktop 旨在帮助 TDH 集群运维人员高效、简便地获取 TDH 集群后台日志和诊断信息，从而保障集群的稳定运行。

不需要懂 Linux ，不需要懂 Docker ，不需要懂 K8S ，只需要输入一些集群的基本信息，再动动鼠标，后台日志和诊断信息就能即刻出现在您的眼前。

无论是自行排查日志，还是将日志和诊断信息打包发送给售后支持人员，TDH Collector Desktop 都能够大大提高 Troubleshooting 效率。

----

## 环境要求

### 本机操作系统

#### Windows

TDH Collector Desktop 可以运行在64位 x86 架构的 Windows 操作系统当中，尽管我们还没有进行全面的测试，但理论上支持 Windows 7、Windows 8、Windows 8.1、Windows 10 和 Windows 11 操作系统。

注意，如果您的设备的位数是32位，或者不是 x86 架构（可能是 ARM 或其他架构），那么 TDH Collector 可能将无法运行在您的设备上。

在较早版本的 Windows 或不完整的 Windows 操作系统中，常常出现C++运行时不完整的情况，如果您遇到类似的报错信息，请下载并安装[Microsoft Visual C++ Redistributable for Visual Studio 2022](https://aka.ms/vs/17/release/VC_redist.x64.exe)。

#### MacOS

TDH Collector Desktop 可以运行在64位 x86 架构的 MacOS 操作系统当中，尽管我们还没有进行全面的测试，但理论上支持 Mojave (10.14) 以来的所有版本。

请注意，Apple Silicon Chip 版本的 MacOS 虽然可以通过 Rosetta 2 来载入 x86 架构的应用，但我们当前并不能保证一定可以在 Apple Silicon Chip 版本的 MacOS 中成功运行，请知悉。随着 Apple Silicon Chip 版本越来越成为主流，我们在后续也会推出全面适配该版本的 TDH Collector Desktop 。

#### 其他 OS

很遗憾，目前 TDH Collector Desktop 还没有在非 Windows 和 MacOS 操作系统上提供应用程序。

### 集群兼容性

#### 版本兼容性

TDH Collector Desktop 当前理论上支持 Transwarp Manager 5.x - 8.x 的所有版本，TDH 服务 5.x - 8.x 所有版本，Transwarp Guardian 所有版本，TDS 服务 1.x - 2.x 所有版本，Transwarp ArgoDB 所有版本，Transwarp Sophon 所有版本。

当然，因为版本众多，我们无法所有版本都进行测试，当前还无法保证所有版本都没有任何兼容性问题。

#### 操作系统兼容性

考虑到 Linux 众多的发行版，一些命令逻辑在不同的 Linux 发行版上可能略微有些区别，所以我们无法确保所有功能都能够在每个发行版上完美运行。

我们目前确保集群操作系统在 CentOS/RHEL 7.x 版本下，TDH Collector Desktop 的所有功能都能够实现，后续也会继续增加对其他版本和操作系统的支持。

### 网络要求

TDH Collector Desktop 部署于笔记本电脑或台式电脑，而 TDH 集群则位于服务器上，所以不可避免会出现网络通信和交互。

如果要实现最基本的功能，那么集群所有节点的 SSH/SFTP 端口（通常为22端口）以及 Manager 节点的页面访问端口（通常为8180端口）都需要对安装 TDH Collector Desktop 的计算机开放。

如果想要不受限制地使用所有功能，那么所有服务的入口端口（包括但不限于 Inceptor 的10000端口、Slipstream 的 10010 端口等）也需要对安装 TDH Collector Desktop 的计算机开放。

### 权限要求

#### 节点登录用户

我们非常推荐使用`root`用户。

如果要实现最基本的功能，那么节点配置的用户应需要有 SSH 和 SFTP 访问权限。

如果想要不受限制地使用所有功能，那么则需要使用有 SSH 和 SFTP 访问权限的`root`用户。

注意，目前 TDH Collector Desktop 仅支持节点密码登录。

#### Manager 用户

我们非常推荐使用`admin`用户。

----

## 安装 TDH Collector Desktop

您可以在[此链接](https://github.com/Jovany-Rong/TDH_Collector_Desktop/releases/latest)中获取 TDH Collector Desktop 的最新安装包。如果您想要获取历史版本的安装包，那么您可以访问[此链接](https://github.com/Jovany-Rong/TDH_Collector_Desktop/releases)。

*这个 Repo 目前仅用于存放 TDH Collector Desktop 的更新信息。*

如果您的网络无法连接上面的链接，那么您还可以访问[这个链接](https://pan.baidu.com/s/1DPI68lRdCoBOlJMF7kI-gQ)来进行下载，提取码为`tcd8`。

*每个版本的 Windows 安装包和 MacOS 安装包发布的时间可能不同。*

----

## 快速开始

本章节将从一个典型场景入手，帮助您快速上手 TDH Collector Desktop 。

### 添加集群节点

安装完成后，打开 TDH Collector Desktop ，界面如下所示。

![image.png](https://s2.loli.net/2022/01/24/VWHCFILzsJM3lP9.png)

首次使用时需要添加节点信息，每个节点信息只需要添加一次，后续使用如果节点信息没有变化，无需修改。

点击菜单栏【配置】-【节点配置】。

![image.png](https://s2.loli.net/2022/01/24/p3tUhEGToFjbCWu.png)

此时会弹出节点窗口。

![image.png](https://s2.loli.net/2022/01/24/pE8UKnymCobRkDV.png)

点击右下角的【添加】，添加第一个节点，将节点的基本信息填好。

![image.png](https://s2.loli.net/2022/01/24/jA5qdkoFTWg1nI4.png)

如上图，如果该节点是 Manager 的主节点，那么请勾选【是否为当前 Manager 节点】勾选框，并填写 Manager admin 用户的密码。

如果该节点并不是 Manager 主节点，那么请不要勾选【是否为当前 Manager 节点】勾选框，如下图所示。

![image.png](https://s2.loli.net/2022/01/24/aNEPMtHbS9s13LZ.png)

确认完信息无误后，点击【保存】。

此时会回到节点窗口，请重复点击【添加】按钮，确保集群的所有节点都添加完毕，如下图所示。

![image.png](https://s2.loli.net/2022/01/24/iUdOAq4eToVgjGP.png)

### 更新服务信息

节点信息添加完毕后，点击窗口的【X】按钮，关闭节点页面，此时会弹出确认提示。

![image.png](https://s2.loli.net/2022/01/24/QBYMaKRVmxEluIU.png)

点击【Yes】，此时会弹出另一个确认提示。

![image.png](https://s2.loli.net/2022/01/24/upIlAeiwHMGSaZE.png)

点击【Yes】，此时返回主界面，主界面的服务数量和主显示区域内容已经更新完毕。

![image.png](https://s2.loli.net/2022/01/24/oDZXqbW6TE73xud.png)

### 获取特定角色日志

例如有一个 Inceptor Metastore 角色状态出现了异常，现在需要排查后台日志。

首先在搜索框中搜索 `metastore`，并输入回车键。

![image.png](https://s2.loli.net/2022/01/24/eX34ghrI9HMdEGS.png)

所有包含关键词 `metastore` 的服务和角色就会显示在主显示区域中。

接下来打开【Inceptor1】标签栏，并点击【角色】字样下方的【Inceptor Metastore】按钮。

![image.png](https://s2.loli.net/2022/01/24/1P8iFMTOlbJBjqh.png)

此时会弹出日志收集窗口。

![image.png](https://s2.loli.net/2022/01/24/qFYTDULl7SHA8wx.png)

【节点】下拉框可以选择我们需要收集的节点名称；【模式】下拉框可以选择我们需要收集日志的方式，默认为 `Simple` 即搜集最近的一个日志文件；【下载目录】则是日志文件下载的存放路径。

例如我们这次想要获取 `tdh1` 节点上 `Inceptor Metastore` 角色在1月22日至1月23日的日志，则可以按照如下进行设置。

![image.png](https://s2.loli.net/2022/01/24/ctnGyqg57f3QlSk.png)

配置完成后，点击【获取】。

![image.png](https://s2.loli.net/2022/01/24/lrPnCSg7pHLJWAX.png)

根据日志量的大小，稍等片刻后即可下载完成，并弹出提示，此时选择【Yes】。

![image.png](https://s2.loli.net/2022/01/24/QlNq6F8eHXcvVhu.png)

下载目录被自动打开，我们发现我们需要的日志文件已经下载完成了。

### 执行预定义 CheckList 诊断

除了最基本的日志收集功能，TDH Collector Desktop 还预定义了一些常用的 CheckList ，用于在出现特定问题时一键收集所有信息。

例如我们如果遇到 Manager 8180 页面打不开的问题。

首先在搜索框中搜索 `manager`，并输入回车键。

![image.png](https://s2.loli.net/2022/01/24/hzFHj8lg2muUis9.png)

所有包含关键词 `manager` 的服务和角色就会显示在主显示区域中。

接下来打开【Manager】标签栏，并点击【快捷功能】字样下方的【8180 页面打不开】按钮。

![image.png](https://s2.loli.net/2022/01/24/vM4KCRjJN1tSiZU.png)

此时会弹出文件选择对话框，选择 CheckList 诊断信息下载的目录，例如桌面。

![image.png](https://s2.loli.net/2022/01/24/M3g9GUAhpIrLvPK.png)

根据诊断信息的大小，稍等片刻后即可下载完成，并弹出提示，此时选择【OK】。

![image.png](https://s2.loli.net/2022/01/24/1olakxWBFVNC7LO.png)

下载目录被自动打开，我们发现我们需要的诊断信息已经下载完成了。

![image.png](https://s2.loli.net/2022/01/24/ei9Iz3CSW7AV6k5.png)

----

*To be continued ...*
