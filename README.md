
# Transwarp Case Diagnostic Tool (CDT) 使用手册

**适用版本：1.0.x**

**编写时间：2022-01-25**

**更新时间：2022-02-16**

----

## 什么是 Transwarp Case Diagnostic Tool (CDT)

Transwarp Case Diagnostic Tool (CDT) 是一款适配 Transwarp Data Hub （即 TDH）集群的运维诊断辅助工具。Transwarp Case Diagnostic Tool (CDT) 旨在帮助 TDH 集群运维人员高效、简便地获取 TDH 集群后台日志和诊断信息，从而保障集群的稳定运行。

不需要懂 Linux ，不需要懂 Docker ，不需要懂 K8S ，只需要输入一些集群的基本信息，再动动鼠标，后台日志和诊断信息就能即刻出现在您的眼前。

无论是自行排查日志，还是将日志和诊断信息打包发送给售后支持人员，Transwarp Case Diagnostic Tool (CDT) 都能够大大提高 Troubleshooting 效率。

----

## 环境要求

### 本机操作系统

#### Windows

Transwarp Case Diagnostic Tool (CDT) 可以运行在64位 x86 架构的 Windows 操作系统当中，尽管我们还没有进行全面的测试，但理论上支持 Windows 7、Windows 8、Windows 8.1、Windows 10 和 Windows 11 操作系统。

注意，如果您的设备的位数是32位，或者不是 x86 架构（可能是 ARM 或其他架构），那么 TDH Collector 可能将无法运行在您的设备上。

在较早版本的 Windows 或不完整的 Windows 操作系统中，常常出现C++运行时不完整的情况，如果您遇到类似的报错信息，请下载并安装[Microsoft Visual C++ Redistributable for Visual Studio 2022](https://aka.ms/vs/17/release/VC_redist.x64.exe)。

#### MacOS

Transwarp Case Diagnostic Tool (CDT) 可以运行在64位 x86 架构的 MacOS 操作系统当中，尽管我们还没有进行全面的测试，但理论上支持 Mojave (10.14) 以来的所有版本。

请注意，Apple Silicon Chip 版本的 MacOS 虽然可以通过 Rosetta 2 来载入 x86 架构的应用，但我们当前并不能保证一定可以在 Apple Silicon Chip 版本的 MacOS 中成功运行，请知悉。随着 Apple Silicon Chip 版本越来越成为主流，我们在后续也会推出全面适配该版本的 Transwarp Case Diagnostic Tool (CDT) 。

#### 其他 OS

很遗憾，目前 Transwarp Case Diagnostic Tool (CDT) 还没有在非 Windows 和 MacOS 操作系统上提供应用程序，请您尽量在 Windows 或 MacOS 操作系统上使用本软件。

### 集群兼容性

#### 版本兼容性

Transwarp Case Diagnostic Tool (CDT) 当前理论上支持 Transwarp Manager 5.x - 8.x 的所有版本，TDH 服务 5.x - 8.x 所有版本，Transwarp Guardian 所有版本，Transwarp Aquila 所有版本，TDS 服务 1.x - 2.x 所有版本，Transwarp ArgoDB 所有版本，Transwarp Sophon 所有版本。

当然，因为版本众多，我们无法所有版本都进行测试，当前还无法保证所有版本都没有任何兼容性问题。

#### 操作系统兼容性

考虑到 Linux 众多的发行版，一些命令逻辑在不同的 Linux 发行版上可能略微有些区别，所以我们无法确保所有功能都能够在每个发行版上完美运行。

我们目前确保集群操作系统在 CentOS/RHEL 7.x 版本下，Transwarp Case Diagnostic Tool (CDT) 的所有功能都能够实现，后续也会继续增加对其他版本和操作系统的支持。

### 网络要求

#### 本机与集群间网络要求

Transwarp Case Diagnostic Tool (CDT) 部署于笔记本电脑或台式电脑，而 TDH 集群则位于服务器上，所以不可避免会出现网络通信和交互。

如果要实现最基本的功能，那么集群所有节点的 SSH/SFTP 端口（通常为22端口）以及 Manager 节点的页面访问端口（通常为8180端口）都需要对安装 Transwarp Case Diagnostic Tool (CDT) 的计算机开放。

如果想要不受限制地使用所有功能，那么所有服务的入口端口（包括但不限于 Inceptor 的10000端口、Slipstream 的 10010 端口等）也需要对安装 Transwarp Case Diagnostic Tool (CDT) 的计算机开放。

#### 互联网网络要求

Transwarp Case Diagnostic Tool (CDT) 本身不需要依赖于互联网，可以在内网环境下实现所有的功能。

*唯一与互联网有关的功能为检查更新，用户可手动在界面上点选【检查更新】菜单，此时会打开您的浏览器访问下载地址，如果您没有互联网连接或网络连接不畅通，则会更新失败。*

*此外，【帮助】菜单栏下的部分菜单也会使用您的浏览器打开一些外部链接，如果您没有互联网连接或网络连接不畅通，则会无法打开相应的页面。*

### 权限要求

#### 节点登录用户

我们非常推荐使用`root`用户。

如果要实现最基本的功能，那么节点配置的用户应需要有 SSH 和 SFTP 访问权限。

如果想要不受限制地使用所有功能，那么则需要使用有 SSH 和 SFTP 访问权限的`root`用户。

注意，目前 Transwarp Case Diagnostic Tool (CDT) 仅支持节点密码登录。

#### Manager 用户

目前 Transwarp Case Diagnostic Tool (CDT) 仅支持 Manager 的 `admin` 用户登录。

----

## 安装及更新 Transwarp Case Diagnostic Tool (CDT)

### 获取安装包

您可以随时联系星环科技售后支持来获取 Transwarp Case Diagnostic Tool (CDT) 的安装包。

此外，您也可以在[此链接](https://nj.transwarp.club:666/main.html?download&weblink=54114b4d0e00c74076d9900df88bfd21)中获取 Transwarp Case Diagnostic Tool (CDT) 的最新安装包。

*每个版本的 Windows 安装包和 MacOS 安装包发布的时间可能不同。*

### Windows 安装

Windows 版本的 Transwarp Case Diagnostic Tool (CDT) 安装包是一个 exe 可执行文件，直接打开即可安装。

### MacOS 安装

MacOS 版本的 Transwarp Case Diagnostic Tool (CDT) 安装包是一个 dmg 文件，打开该文件后，将 app 程序拖入应用程序目录中即可完成安装。

### 软件更新

可以直接下载最新版本的安装包来覆盖安装，也可以点击【关于】菜单栏下的【检查更新】菜单在线下载最新安装包。

----

## 快速开始

本章节将从一个典型场景入手，帮助您快速上手 Transwarp Case Diagnostic Tool (CDT) 。

### 添加集群节点案例

安装完成后，打开 Transwarp Case Diagnostic Tool (CDT) ，界面如下所示。

![image.png](https://s2.loli.net/2022/01/25/zdio5ZKIyH2XRGA.png)

首次使用时需要添加节点信息，每个节点信息只需要添加一次，后续使用如果节点信息没有变化，无需修改。

点击菜单栏【配置】-【节点配置】。

![image.png](https://s2.loli.net/2022/01/25/qkJyouDIv5OTHjh.png)

此时会弹出节点窗口。

![image.png](https://s2.loli.net/2022/01/25/Qx47AsTpwrPOZgu.png)

例如这个TDH集群有3个节点。

点击右下角的【批量添加】，并在弹出窗口中将第一个节点的基本信息填好。

![image.png](https://s2.loli.net/2022/01/25/jklnrhRIEbaG4oA.png)

点击2次【复制】按钮，将我们填写好的节点信息复制2份。

![image.png](https://s2.loli.net/2022/01/25/CImvAwDRsHeS1pq.png)

此时再根据我们集群的实际情况，将2、3两个节点的信息修改正确，注意节点名称和IP地址是不能重复的，如果有其他信息也跟1节点不同，那么也需要对应修改正确。

![image.png](https://s2.loli.net/2022/01/25/mq1ce9JB7olYfub.png)

确认完信息无误后，点击【保存】。

此时会回到节点窗口，确保集群的所有节点都添加完毕，如下图所示。

![image.png](https://s2.loli.net/2022/01/25/R3NskHrvVYpuEbo.png)

3个节点都已经添加好了，但是似乎它们都显示不是 Manager 节点，接下来我们就要将其中的 Manager 节点设置正确。

假设 tdh1 节点为 Manager 节点，那么就点击 tdh1 节点的【编辑】按钮，勾选上【是否为当前 Manager 节点】，并填写好 Manager 的端口号和 admin 用户密码。

![image.png](https://s2.loli.net/2022/01/25/1VvgPDEL3Z6OzA8.png)

确认无误后，点击【保存】。

此时节点信息就完全正确了。

![image.png](https://s2.loli.net/2022/01/25/48fUdXmeGio2FhI.png)

### 更新服务信息案例

节点信息添加完毕后，点击窗口的【X】按钮，关闭节点页面，此时会弹出确认提示。

![image.png](https://s2.loli.net/2022/01/24/QBYMaKRVmxEluIU.png)

点击【Yes】，此时会弹出另一个确认提示。

![image.png](https://s2.loli.net/2022/01/24/upIlAeiwHMGSaZE.png)

点击【Yes】，此时返回主界面，主界面的服务数量和主显示区域内容已经更新完毕。

![image.png](https://s2.loli.net/2022/01/24/oDZXqbW6TE73xud.png)

### 获取特定角色日志案例

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

### 执行预定义 CheckList 诊断案例

除了最基本的日志收集功能，Transwarp Case Diagnostic Tool (CDT) 还预定义了一些常用的 CheckList ，用于在出现特定问题时一键收集所有信息。

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

## 配置

本章节详细描述 Transwarp Case Diagnostic Tool (CDT) 的配置信息。

### 节点配置

Transwarp Case Diagnostic Tool (CDT) 通过节点配置来管理集群的节点信息，也包括执行具体的日志获取或诊断任务时连接节点的信息。

#### 节点配置页面

节点配置入口在页面的节点数右侧的【详情】按钮及【配置】菜单栏下的【节点配置】菜单，两者都会点击打开节点配置页面。

![image.png](https://s2.loli.net/2022/01/25/qkJyouDIv5OTHjh.png)

![image.png](https://s2.loli.net/2022/01/25/3RCVBAnXs4yxcop.png)

节点配置页面如图所示。

![image.png](https://s2.loli.net/2022/01/25/48fUdXmeGio2FhI.png)

在此页面中，上中部分是一个可滚动区域，显示了当前所有的节点。在没有配置节点时，此区域为空。下部有两个按钮，【批量添加】按钮用于一次性添加多个节点信息，【添加】按钮用于添加单个节点信息。

每个节点的信息会放在一个灰色边框的区域，此区域的左上角为节点名称。区域中央部分显示了该节点的 IP 地址及是否为 Manager 节点。区域下部有三个按钮，【测试】按钮用于测试该节点的 SSH/SFTP 连通性，【编辑】按钮用于修改该节点的信息，【删除】按钮用于删除该节点。

#### 添加单个节点

在节点配置页面中，点击【添加】按钮即可打开节点编辑页面添加单个节点。

![image.png](https://s2.loli.net/2022/01/25/6EJW3aIb2wOD7B9.png)

节点编辑页面如图所示。

![image.png](https://s2.loli.net/2022/01/25/Ea1K45pelTSU6Xo.png)

每个字段的填写要求如下。

 - 节点名称/别名

    该字段必填。该字段代表 Transwarp Case Diagnostic Tool (CDT) 管理集群节点时的唯一标识及别名，不可重复。注意，该字段并不一定必须是节点实际的 hostname 。

 - IP 地址

    该字段必填。该字段代表节点的访问 IP 地址，用于 SSH 连接或 Manager 8180 页面的访问。当然，如果该 IP 地址已经配置到了您本机的 hosts 文件中，那么也可以配置为本机 hosts 文件中该 IP 地址对应的域名。

 - 端口号

    该字段必填。该字段的值必须是 1-65535 中的整数。该字段代表节点的 SSH 端口号，用于 SSH 和 SFTP 连接。默认值为 22 。

 - SSH 用户名（管理员权限）

    该字段必填。该字段代表 SSH 和 SFTP 连接节点时的登录用户。需要注意的是，如果该字段的值配置的不是 root ，那么可能部分诊断任务会因为权限问题无法完成。如果希望 Transwarp Case Diagnostic Tool (CDT) 不仅仅简单地收集服务角色的日志，那么我们建议您配置为 root 。

 - SSH 用户密码

    该字段必填。该字段代表SSH 用户名（管理员权限）的值对应的用户密码，供 SSH 和 SFTP 连接节点时使用。

 - 是否为当前 Manager 节点

    该字段选填。该字段代表该节点是否为**当前**的 Manager 节点。如果节点是**当前**的 Manager 节点，那么需要勾选，否则不需要勾选。注意，如果 Manager 开了高可用（HA），那么请只在当前的 Manager 节点（即当前 8180 页面对应的 Manager 节点）勾选此字段。

 - 是否启用 HTTPS

    该字段选填。当是否为当前 Manager 节点没有勾选时，该字段无效。当是否为当前 Manager 节点被勾选时，该字段代表 Manager 是否开了 HTTPS 访问，如果 Manager 开启了 HTTPS 访问，那么需要勾选，否则不需要勾选。

 - Manager 端口号

    该字段选填。该字段的值必须是 1-65535 中的整数。当是否为当前 Manager 节点没有勾选时，该字段无效。当是否为当前 Manager 节点被勾选时，该字段变为必填，代表 Manager 的访问端口号。默认值为 8180 。

 - Manager admin 用户密码

    该字段选填。当是否为当前 Manager 节点没有勾选时，该字段无效。当是否为当前 Manager 节点被勾选时，该字段变为必填，代表 Manager 的 admin 用户的登录密码。

正确将节点信息填写完毕后，点击【保存】按钮即可添加节点。

#### 批量添加节点

在节点配置页面中，点击【批量添加】按钮即可打开批量节点编辑页面添加多个节点。

![image.png](https://s2.loli.net/2022/01/25/x26rWmUE7dkIPpL.png)

注意，批量添加节点功能无法直接将节点设置为 Manager 节点，如需要添加 Manager 节点，必须使用添加单个节点功能或在批量节点添加完毕后，手动编辑节点信息将其设置为 Manager 节点。

【新增】按钮会添加一条空的节点记录，每个节点记录的【复制】按钮会将这条节点记录的信息复制一份到新的节点记录中，每个节点记录的【删除】按钮会将这条节点记录删除。

每个节点记录中的字段填写要求如下。

 - 节点名称/别名

    该字段必填。该字段代表 Transwarp Case Diagnostic Tool (CDT) 管理集群节点时的唯一标识及别名，不可重复。注意，该字段并不一定必须是节点实际的 hostname 。

 - IP 地址

    该字段必填。该字段代表节点的访问 IP 地址，用于 SSH 连接或 Manager 8180 页面的访问。当然，如果该 IP 地址已经配置到了您本机的 hosts 文件中，那么也可以配置为本机 hosts 文件中该 IP 地址对应的域名。

 - 端口号

    该字段必填。该字段的值必须是 1-65535 中的整数。该字段代表节点的 SSH 端口号，用于 SSH 和 SFTP 连接。默认值为 22 。

 - SSH 用户名（管理员权限）

    该字段必填。该字段代表 SSH 和 SFTP 连接节点时的登录用户。需要注意的是，如果该字段的值配置的不是 root ，那么可能部分诊断任务会因为权限问题无法完成。如果希望 Transwarp Case Diagnostic Tool (CDT) 不仅仅简单地收集服务角色的日志，那么我们建议您配置为 root 。

 - SSH 用户密码

    该字段必填。该字段代表SSH 用户名（管理员权限）的值对应的用户密码，供 SSH 和 SFTP 连接节点时使用。

正确将所有节点信息填写完毕后，点击【保存】按钮即可批量添加所有节点。

#### 测试节点连通性

在节点配置页面中点击每个节点的【测试】按钮可以用来测试该节点的 SSH/SFTP 连通性。

![image.png](https://s2.loli.net/2022/01/26/GbVy2ZjUBxSNuRL.png)

点击【测试】后，稍等片刻会出现测试结果。

出现如图所示的 Success 提示框说明 SSH/SFTP 连接测试成功。

![image.png](https://s2.loli.net/2022/01/26/IecGHWJDa7NotrO.png)

如果出现如图所示的 Error 提示框，那么说明 SSH 和 SFTP 至少有一个连接测试失败，可能是密码错误，也可能是服务器的其他原因。

![image.png](https://s2.loli.net/2022/01/26/fogzw8mtxvLpj4E.png)

#### 编辑节点信息

在节点配置页面中，点击对应节点信息的【编辑】按钮即可打开节点编辑页面编辑该节点信息。

![image.png](https://s2.loli.net/2022/01/26/jNUQC9BbgoqDlzZ.png)

页面与添加单个节点完全相同。需要注意的是，节点名称作为唯一主键，是不支持修改的，如果有修改节点名称的需求，需要删除并重新添加节点。

![image.png](https://s2.loli.net/2022/01/26/Ii9L4RovKS3JqEr.png)

在该页面编辑节点信息，每个字段的填写要求如下。

 - IP 地址

    该字段必填。该字段代表节点的访问 IP 地址，用于 SSH 连接或 Manager 8180 页面的访问。当然，如果该 IP 地址已经配置到了您本机的 hosts 文件中，那么也可以配置为本机 hosts 文件中该 IP 地址对应的域名。

 - 端口号

    该字段必填。该字段的值必须是 1-65535 中的整数。该字段代表节点的 SSH 端口号，用于 SSH 和 SFTP 连接。默认值为 22 。

 - SSH 用户名（管理员权限）

    该字段必填。该字段代表 SSH 和 SFTP 连接节点时的登录用户。需要注意的是，如果该字段的值配置的不是 root ，那么可能部分诊断任务会因为权限问题无法完成。如果希望 Transwarp Case Diagnostic Tool (CDT) 不仅仅简单地收集服务角色的日志，那么我们建议您配置为 root 。

 - SSH 用户密码

    该字段必填。该字段代表SSH 用户名（管理员权限）的值对应的用户密码，供 SSH 和 SFTP 连接节点时使用。

 - 是否为当前 Manager 节点

    该字段选填。该字段代表该节点是否为**当前**的 Manager 节点。如果节点是**当前**的 Manager 节点，那么需要勾选，否则不需要勾选。注意，如果 Manager 开了高可用（HA），那么请只在当前的 Manager 节点（即当前 8180 页面对应的 Manager 节点）勾选此字段。

 - 是否启用 HTTPS

    该字段选填。当是否为当前 Manager 节点没有勾选时，该字段无效。当是否为当前 Manager 节点被勾选时，该字段代表 Manager 是否开了 HTTPS 访问，如果 Manager 开启了 HTTPS 访问，那么需要勾选，否则不需要勾选。

 - Manager 端口号

    该字段选填。该字段的值必须是 1-65535 中的整数。当是否为当前 Manager 节点没有勾选时，该字段无效。当是否为当前 Manager 节点被勾选时，该字段变为必填，代表 Manager 的访问端口号。默认值为 8180 。

 - Manager admin 用户密码

    该字段选填。当是否为当前 Manager 节点没有勾选时，该字段无效。当是否为当前 Manager 节点被勾选时，该字段变为必填，代表 Manager 的 admin 用户的登录密码。

正确将节点信息编辑完毕后，点击【保存】按钮即可保存节点信息。

#### 删除节点信息

在节点配置页面中，点击对应节点信息的【删除】按钮即可删除该节点信息。

![image.png](https://s2.loli.net/2022/01/26/jmA1dTh9fxaIzlv.png)

### 服务配置

Transwarp Case Diagnostic Tool (CDT) 通过服务配置来管理集群的服务信息。服务配置可以认为是 Manager REST API 上服务角色信息的缓存，通过主动更新服务信息可以重新从 Manager REST API 上获取最新的服务信息。

#### 直接更新服务信息

服务配置入口在页面的服务数右侧的【更新】按钮及【配置】菜单栏下的【服务配置】菜单，两者都会点击发起服务更新请求。

![image.png](https://s2.loli.net/2022/01/26/ZL5XEnRHs6DbC9A.png)

![image.png](https://s2.loli.net/2022/01/26/HpO36Tw5svIaiyb.png)

点击后，会弹出服务更新提示框。

![image.png](https://s2.loli.net/2022/01/24/upIlAeiwHMGSaZE.png)

点击【Yes】，此时返回主界面，主界面的服务数量和主显示区域内容已经更新完毕。

![image.png](https://s2.loli.net/2022/01/24/oDZXqbW6TE73xud.png)

#### 节点配置后更新服务信息

除了主动直接更新服务信息，在节点配置完成后也可以立即更新服务信息。

点击节点配置窗口的【X】按钮，关闭节点页面，此时会弹出确认提示。

![image.png](https://s2.loli.net/2022/01/24/QBYMaKRVmxEluIU.png)

点击【Yes】，此时会弹出另一个确认提示。

![image.png](https://s2.loli.net/2022/01/24/upIlAeiwHMGSaZE.png)

点击【Yes】，此时返回主界面，主界面的服务数量和主显示区域内容已经更新完毕。

![image.png](https://s2.loli.net/2022/01/24/oDZXqbW6TE73xud.png)

### 映射配置

Transwarp Case Diagnostic Tool (CDT) 通过映射配置来管理集群的服务名称映射信息。如果在 TDH 安装服务时没有使用默认的服务名称，或是集群有多次删除服务重装的场合，显示的服务名称与后台服务器中实际的服务 SID 可能会有区别。这种情况下，就需要配置映射来让 Transwarp Case Diagnostic Tool (CDT) 正确识别到服务，否则可能无法正确获取服务日志及诊断信息。

反过来说，如果是正常安装的 TDH 集群，且没有自行修改过服务名称，那么是无需配置映射的。

#### 映射配置页面

映射配置入口在页面的服务数右侧的【映射】按钮，点击它即可打开映射配置页面。

![image.png](https://s2.loli.net/2022/01/26/zlHP7gunVYk1Ns8.png)

映射配置页面如图所示。

![image.png](https://s2.loli.net/2022/01/26/d1aZpw9nseJYuKF.png)

在此页面中，上方有一个【添加新映射】按钮用于新增映射信息。中央部分是一个可滚动区域，显示了当前所有的映射。在没有配置映射时，此区域为空。下部有一个【保存】按钮用于保存映射的更改。

每个映射的信息会放在一个灰色边框的区域，此区域中央部分显示了该映射的服务原始名称和服务映射名称，【删除】按钮用于删除该映射。

#### 添加映射信息

可以通过在映射配置页面点击【添加新映射】按钮，打开映射编辑页面来添加新的映射信息。

![image.png](https://s2.loli.net/2022/01/26/dYaVvWoeMEH5Gzq.png)

映射编辑页面中需要从下拉框中选择服务原始名称，并在输入窗口中输入服务映射名称。

每个字段的填写要求如下。

 - 服务原始名称

    该字段必填。该字段代表该映射的服务原名，及 Manager 页面显示的服务名和 Manager API 获取的服务名。

 - 服务映射名称

    该字段必填。该字段代表映射的服务实际 SID，与集群服务器上存放的服务配置、日志路径名非常类似。必须注意的是，集群服务器上存放的服务配置、日志路径名通常为**全部小写**字母，但该字段**必须**配置为通常服务的形式，例如 Manager 上有一个 Inceptor1 服务，实际上在服务其中它的配置和日志目录名称为 `inceptor2` ，但服务映射名称必须配置为 `Inceptor2` ，这样才能让 Transwarp Case Diagnostic Tool (CDT) 正确识别到这个服务。

填写完毕后，点击【保存】按钮即可将新的映射信息保存。

#### 删除映射信息

在映射配置页面中，点击对应映射信息的【删除】按钮即可删除该映射信息。

![image.png](https://s2.loli.net/2022/01/26/bha2rQedkGjO4Fx.png)

### 配置初始化

Transwarp Case Diagnostic Tool (CDT) 通过配置初始化来还原配置。配置初始化会将现有的节点配置、服务配置和映射配置全部删除，还原成初始的空配置。在新安装的 Transwarp Case Diagnostic Tool (CDT) 首次运行时，程序会自动进行配置初始化的操作。

配置初始化入口在【配置】菜单栏下的【配置初始化】菜单。

![image.png](https://s2.loli.net/2022/01/26/NoqrMsSxn43z59g.png)

点击【配置初始化】，会弹出提示框，再点击【Yes】就开始进行配置初始化的操作。

![image.png](https://s2.loli.net/2022/01/26/CcKkMXJb2oiwZHF.png)

注意，配置初始化操作是不可逆的，一旦初始化，那么后续必须重新进行节点和服务配置才能够使用 Transwarp Case Diagnostic Tool (CDT) 。

### 语言设置

Transwarp Case Diagnostic Tool (CDT) 支持多国语言并可以随时切换。切换语言可以通过点击【国际化】菜单栏下的语言菜单进行。

![image.png](https://s2.loli.net/2022/01/26/2WeZztNshVr7Rvg.png)

当前 Transwarp Case Diagnostic Tool (CDT) 支持的语言如下。

 - English

    英文（美国）。

 - 简体中文

    中文简体字（中国大陆）。

 - 日本語

    日语（日本）。

 - 한국어

    朝鲜语（韩国）。

*可能存在部分页面翻译不完全的情况，这种情况下可能会有部分文本将显示为英文。*

在 Windows 系统中，如果系统语言为中文（中国），那么 Transwarp Case Diagnostic Tool (CDT) 将会自动设置语言为简体中文。在其他场合，Transwarp Case Diagnostic Tool (CDT) 的默认语言为英文。

----

## 使用方法

本章节主要介绍 Transwarp Case Diagnostic Tool (CDT) 的具体使用方法。需要注意的是，本章节内容的前提是按照[配置](#配置)章节完成好节点、服务和映射的配置。

### 查询服务及角色

有时集群上的服务非常多，此时我们可以善用查询功能来快速定位我们需要的服务及角色。搜索功能在页面的服务区域上方。

![image.png](https://s2.loli.net/2022/01/26/wVhUMaXsIgHbLPq.png)

左侧的【来源】下拉框决定了查询的范围。这个字段的取值如下。

 - All

    默认选择。表示查询范围为服务和角色。例如查询`inceptor`，既会返回 Inceptor 服务，也会返回 ArgoDB 等其他服务，因为 ArgoDB 中也有 Inceptor Server 等角色。

 - Services

    表示查询范围为服务。例如查询`txsql`，那么会返回 TxSQL 服务，但不会返回 Guardian 等其他服务，即使 Guardian 中也有 TxSQL Server 角色。

 - Roles

    表示查询范围为角色。例如查询`metastore`，会返回 Inceptor 、ArgoDB 、Slipstream 等所有名称包含 Metastore 角色的服务。

在中间的输入框中输入查询内容，再点击【查询】按钮即可完成查询。

![image.png](https://s2.loli.net/2022/01/26/FeaWYstHEwMyTIn.png)

*点击查询按钮可以使用快捷键 Enter （回车键）。*

### 获取服务角色日志

Transwarp Case Diagnostic Tool (CDT) 支持获取指定服务角色的日志信息。在页面服务区域中，选择需要获取日志的服务，点击其【角色】标签下的指定角色。

例如有一个 Inceptor Metastore 角色状态出现了异常，现在需要排查后台日志，点击【Inceptor Metastore】按钮。

![image.png](https://s2.loli.net/2022/01/24/1P8iFMTOlbJBjqh.png)

此时会弹出日志收集窗口。

![image.png](https://s2.loli.net/2022/01/24/qFYTDULl7SHA8wx.png)

日志收集窗口的上方显示了此次收集日志的服务和角色名，中间部分是一些可选的参数。这些参数的详细说明如下。

 - 节点

    该字段必填。该字段表示获取日志的节点名称。

 - 模式

    该字段必填。该字段表示获取日志的方式。该字段默认值为`Simple`。

    该字段的取值范围如下。

    1. Simple

        表示同种类的日志将获取最新的一个日志文件。该模式对所有日志都适用。

    2. by Number

        表示同种类的日志将获取指定个数的日志文件，个数将在【数量】参数中指定。该模式若要正常使用，需要日志的转储格式为 xxx.log 、xxx.log.1 、xxx.log.2 这种类型。

    3. by Date & Time

        表示同种类的日志将获取指定时间区间的所有日志文件，时间区间将在【开始时间】和【结束时间】中指定。该模式对大多数正常转储的日志都适用。

 - 数量

    该字段选填。该字段在【模式】的值为`by Number`时变为必填，否则该字段无效。该字段表示同种类的日志获取的文件个数，默认值为1。

 - 开始时间

    该字段选填。该字段在【模式】的值为`by Date & Time`时变为必填，否则该字段无效。该字段表示通过时间区间获取日志文件时的时间区间开始时间，默认值为当天的0点。

 - 结束时间

    该字段选填。该字段在【模式】的值为`by Date & Time`时变为必填，否则该字段无效。该字段表示通过时间区间获取日志文件时的时间区间结束时间，默认值为当前时间。

 - 下载目录

    该字段必填。该字段表示日志文件的下载存放目录，默认值为程序安装目录。

 - 多线程

    该字段选填。该字段表示获取日志时是否使用多线程技术，勾选代表使用，否则不使用。默认值为不勾选。

    多线程会增大连接服务器的开销，但加快下载文件的效率，请自行甄别是否需要启用多线程技术。一般来说，如果网络不是特别慢，建议不启用，如果网速很慢导致下载文件非常慢，那么建议使用多线程。

例如我们这次想要获取 `tdh1` 节点上 `Inceptor Metastore` 角色在1月22日至1月23日的日志，则可以按照如下进行设置。

![image.png](https://s2.loli.net/2022/01/24/ctnGyqg57f3QlSk.png)

配置完成后，点击【获取】。

![image.png](https://s2.loli.net/2022/01/24/lrPnCSg7pHLJWAX.png)

根据日志量的大小，稍等片刻后即可下载完成，并弹出提示，此时选择【Yes】。

![image.png](https://s2.loli.net/2022/01/24/QlNq6F8eHXcvVhu.png)

下载目录被自动打开，我们发现我们需要的日志文件已经下载完成了。

### 快捷功能

除了最基本的服务角色日志获取功能，Transwarp Case Diagnostic Tool (CDT) 还支持其他快捷功能，包括一些独立小工具和特定场景诊断。

快捷功能可以在每个服务的【快捷功能】标签下找到，每个服务的快捷功能各不相同，但基本上可以通过快捷功能的名称来区分它们。

#### 快捷功能：查看版本

查看版本是几乎所有的服务都有的快捷功能，它主要用于查看服务的版本号，便于确认版本信息。

![image.png](https://s2.loli.net/2022/01/26/BQEXC2nR1q5GULs.png)

点击【查看版本】按钮，会弹出目录选择页面，选择指定的下载目录后，稍等片刻即可执行成功，此时会弹 Success 提示对话框。

![image.png](https://s2.loli.net/2022/01/26/dP1iBqK3Avtr458.png)

点击【OK】，即可打开下载目录。

对于 Manager 服务，查看版本会收集 Manager 的 RPM 包版本信息；对于 TOS 服务，查看版本会收集 TOS 镜像和 Pod 描述信息；对于其他服务，查看版本会收集 Pod 描述信息。

#### 快捷功能：Manager 工具箱

Manager 工具箱是 Manager 服务特有的快捷功能，它主要用于方便 Manager 的运维。

![image.png](https://s2.loli.net/2022/01/26/1ymWcBAEN5bo7O4.png)

点击【Manager 工具箱】按钮，会弹出工具箱页面。

![image.png](https://s2.loli.net/2022/01/26/28JiTxzcgVaXK7v.png)

工具箱页面展示了 Manager 访问 URL 、版本号、是否开启 HA 。同时也包含了以下按钮。

 - Copy

    点击【Copy】按钮，会把 Manager 访问 URL 复制到剪切板中，方便粘贴到浏览器打开。

 - Start

    点击【Start】按钮，会启动 Manager 服务，并将最新的 Manager 服务状态展示在底部文本框。

 - Stop

    点击【Stop】按钮，会停止 Manager 服务，并将最新的 Manager 服务状态展示在底部文本框。

 - Restart

    点击【Restart】按钮，会重启 Manager 服务，并将最新的 Manager 服务状态展示在底部文本框。

 - Restart All

    点击【Restart All】按钮，会重启所有 Manager Agent 服务，并将结果打印在底部文本框中。

 - Check

    点击【Check】按钮，会展示当前的 Manager 服务状态，并展示在底部文本框中。

#### 快捷功能：8180 页面打不开

8180 页面打不开是 Manager 服务特有的快捷功能，它用于收集 8180 页面无法访问场景下的诊断信息。

![image.png](https://s2.loli.net/2022/01/27/UbmyJaqeYWPKj3z.png)

点击【8180 页面打不开】按钮，会弹出目录选择页面，选择指定的下载目录后，稍等片刻即可执行成功，此时会弹 Success 提示对话框。

![image.png](https://s2.loli.net/2022/01/26/dP1iBqK3Avtr458.png)

点击【OK】，即可打开下载目录。

8180 页面打不开会收集 Manager 节点使用 curl 命令访问 8180 页面的结果、Manager 服务状态、8180 端口监听情况和本机与 Manager 节点 8180 端口的连通性。

#### 快捷功能：TOS 异常

TOS 异常是 TOS 服务特有的快捷功能，它用于收集 TOS 服务状态异常或无法启动场景下的诊断信息。

![image.png](https://s2.loli.net/2022/01/27/HJcGObwlBCQEVgp.png)

点击【TOS 异常】按钮，会弹出目录选择页面，选择指定的下载目录后，稍等片刻即可执行成功，此时会弹 Success 提示对话框。

![image.png](https://s2.loli.net/2022/01/26/dP1iBqK3Avtr458.png)

点击【OK】，即可打开下载目录。

TOS 异常会收集 TOS Master Pod 状态、服务器基本信息、TOS Slave Journal 日志、TOS Master 镜像状态、TOS Slave 服务状态、Manager 日志、Manager Agent 日志。

#### 快捷功能：TxSQL 异常

TxSQL 异常是 TxSQL 服务特有的快捷功能，它用于收集 TxSQL 服务状态异常或无法启动场景下的诊断信息。

![image.png](https://s2.loli.net/2022/02/15/xsnHeiqQXPDoRMJ.png)

点击【TxSQL 异常】按钮，会弹出目录选择页面，选择指定的下载目录后，稍等片刻即可执行成功，此时会弹 Success 提示对话框。

![image.png](https://s2.loli.net/2022/01/26/dP1iBqK3Avtr458.png)

点击【OK】，即可打开下载目录。

TxSQL 异常会收集 Manager 日志、TxSQL 服务日志、TxSQL Pod 状态、TxSQL 主节点信息。

#### 快捷功能：HDFS 异常

HDFS 异常是 HDFS 服务特有的快捷功能，它用于收集 HDFS 服务状态异常或无法启动场景下的诊断信息。

![image.png](https://s2.loli.net/2022/02/15/gtLTIxpf7QrdB4Y.png)

点击【HDFS 异常】按钮，会弹出目录选择页面，选择指定的下载目录后，稍等片刻即可执行成功，此时会弹 Success 提示对话框。

![image.png](https://s2.loli.net/2022/01/26/dP1iBqK3Avtr458.png)

点击【OK】，即可打开下载目录。

HDFS 异常会收集 Manager 日志、HDFS 服务日志、HDFS Pod 状态、Namenode 页面信息。

#### 快捷功能：YARN 异常

YARN 异常是 YARN 服务特有的快捷功能，它用于收集 YARN 服务状态异常或无法启动场景下的诊断信息。

![image.png](https://s2.loli.net/2022/02/15/sHYQo9Fdlz2OKfa.png)

点击【YARN 异常】按钮，会弹出目录选择页面，选择指定的下载目录后，稍等片刻即可执行成功，此时会弹 Success 提示对话框。

![image.png](https://s2.loli.net/2022/01/26/dP1iBqK3Avtr458.png)

点击【OK】，即可打开下载目录。

YARN 异常会收集 Manager 日志、YARN 服务日志、YARN Pod 状态。

#### 快捷功能：Inceptor 异常

Inceptor 异常是 Inceptor、ArgoDB 等服务具有的快捷功能，它用于收集 Inceptor 或 ArgoDB 服务状态异常或无法启动场景下的诊断信息。

![image.png](https://s2.loli.net/2022/02/16/LYw1ofimNKAUQOc.png)

点击【Inceptor 异常】按钮，会弹出目录选择页面，选择指定的下载目录后，稍等片刻即可执行成功，此时会弹 Success 提示对话框。

![image.png](https://s2.loli.net/2022/01/26/dP1iBqK3Avtr458.png)

点击【OK】，即可打开下载目录。

Inceptor 异常会收集 Manager 日志、Inceptor 或 ArgoDB 服务日志、Inceptor 或 ArgoDB Pod 状态、本机到 Inceptor 或 ArgoDB 10000端口的连通情况。

#### 快捷功能：SQL 异常

SQL 异常是 Inceptor、ArgoDB 等服务具有的快捷功能，它用于收集 Inceptor 或 ArgoDB 的 SQL 执行发生错误等异常场景下的诊断信息。

![image.png](https://s2.loli.net/2022/02/16/bVdy3XiMZzBGtrc.png)

点击【SQL 异常】按钮，会弹出目录选择页面，选择指定的下载目录后，稍等片刻即可执行成功，此时会弹 Success 提示对话框。

![image.png](https://s2.loli.net/2022/01/26/dP1iBqK3Avtr458.png)

点击【OK】，即可打开下载目录。

SQL 异常会收集 Inceptor 或 ArgoDB 服务日志、本机到 Inceptor 或 ArgoDB 10000端口的连通情况。

#### 快捷功能：JVM 信息

JVM 信息是 Inceptor、Slipstream、ArgoDB 等服务具有的快捷功能，它用于收集对应服务的 JVM 诊断信息。

![image.png](https://s2.loli.net/2022/02/16/zyGkZ8gFSpB2Jjb.png)

点击【JVM 信息】按钮，会弹出 JVM 信息获取页面。

![image.png](https://s2.loli.net/2022/02/16/GcrTew2CqnifsIp.png)

JVM 信息获取页面包含了以下选项。

 - JSTACK

    勾选代表需要收集服务的 jstack 信息，默认勾选。

 - JMAP

    勾选代表需要收集服务的 jmap 信息，默认勾选。注意，收集 jmap 信息可能会导致一次完整的 GC 。

 - JSTAT

    勾选代表需要收集服务的 jstat 信息。注意，收集 jstat 信息一般耗时比较长，且服务安装的节点数越多耗时越长。

点击【Get】按钮，会弹出目录选择页面，选择指定的下载目录后，稍等片刻即可执行成功，此时会弹 Success 提示对话框。

![image.png](https://s2.loli.net/2022/01/26/dP1iBqK3Avtr458.png)

点击【OK】，即可打开下载目录。

JVM 信息会收集指定的 JVM 信息（jstack、jmap 或 jstat）。
