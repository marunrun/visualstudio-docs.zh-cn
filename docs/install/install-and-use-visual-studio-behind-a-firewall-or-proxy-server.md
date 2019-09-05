---
title: 在防火墙或代理服务器背后安装和使用
description: 如果组织使用防火墙或代理服务器，请检查希望添加到允许列表或打开的域 URL、端口和协议
ms.date: 05/22/2019
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
- list of domains, locations, URLs
ms.assetid: ''
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: e102636793c306a4e8141294ad2573b57f03e889
ms.sourcegitcommit: 44e9b1d9230fcbbd081ee81be9d4be8a485d8502
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70180014"
---
# <a name="install-and-use-visual-studio-and-azure-services-behind-a-firewall-or-proxy-server"></a>在防火墙或代理服务器后面安装和使用 Visual Studio 和 Azure 服务

如果你或贵组织使用防火墙或代理服务器等安全措施，则会有可能需要将其添加到“允许列表”的域 URL，以及可能需要打开的端口和协议，以便在安装和使用 Visual Studio 以及 Azure 服务时获得最佳体验。

* **[安装 Visual Studio](#install-visual-studio)** ：这些表包括要添加到允许列表的域 URL，以便你可访问所需的所有组件和工作负载。

* **[使用 Visual Studio 和 Azure 服务](#use-visual-studio-and-azure-services)** ：此表包括要添加到允许列表的域 URL 以及要打开的端口和协议，以便你可访问所需的所有功能和服务。

> [!NOTE]
> 本文针对 Windows 上的 Visual Studio 编写，但部分信息也适用于在防火墙或代理服务器后[安装 Visual Studio for Mac](/visualstudio/mac/install-behind-a-firewall-or-proxy-server)。

## <a name="install-visual-studio"></a>安装 Visual Studio

### <a name="urls-to-add-to-an-allow-list"></a>要添加到允许列表的 URL

因为 Visual Studio 安装程序从各个域及其下载服务器下载文件，以下是你可能需要在 UI 或部署脚本中以可信方式添加到允许列表的域 URL。

#### <a name="microsoft-domains"></a>Microsoft 域

| Domain | 目标 |
| - | - |
| go.microsoft.com | 安装程序 URL 解析 |
| aka.ms | 安装程序 URL 解析 |
| download.visualstudio.microsoft.com | 安装包下载位置 |
| download.microsoft.com | 安装包下载位置 |
| download.visualstudio.com | 安装包下载位置 |
| dl.xamarin.com | 安装包下载位置 |
| marketplace.visualstudio.com | Visual Studio 扩展下载位置 |
| visualstudio.microsoft.com | 文档位置 |
| docs.microsoft.com | 文档位置 |
| msdn.microsoft.com | 文档位置 |
| www\.microsoft.com | 文档位置 |
| \*.windows.net | 登录位置 |
| \*.microsoftonline.com | 登录位置 |
| \*.live.com | 登录位置 |
| | |

#### <a name="non-microsoft-domains"></a>非 Microsoft 域

| Domain | 安装这些工作负载 |
| - | - |
| archive.apache.org | 使用 JavaScript 的移动开发 (Cordova) |
| cocos2d-x.org | 使用 C++ 的游戏开发 (Cocos) |
| download.epicgames.com | 使用 C++ 的游戏开发 (Unreal Engine) |
| download.oracle.com | 使用 JavaScript 的移动开发 (Java SDK) <br /><br />使用 .NET 的移动开发 (Java SDK) |
| download.unity3d.com | 使用 Unity 的游戏开发 (Unity) |
| netstorage.unity3d.com | 使用 Unity 的游戏开发 (Unity) |
| dl.google.com | 使用 JavaScript 的移动开发（Android SDK 和 NDK、仿真器） <br /><br />使用 .NET 的移动开发（Android SDK 和 NDK、仿真器） |
| www\.incredibuild.com | 使用 C++ 的游戏开发 (IncrediBuild) |
| incredibuildvs2017i.azureedge.net | 使用 C++ 的游戏开发 (IncrediBuild) |
| www\.python.org | Python 开发 (Python) <br /><br />数据科学和分析应用程序 (Python) |
| | |

## <a name="use-visual-studio-and-azure-services"></a>使用 Visual Studio 和 Azure 服务

### <a name="urls-to-add-to-an-allow-list-and-ports-and-protocols-to-open"></a>添加到允许列表的 URL 和要打开的端口和协议

若要确保在防火墙或代理服务器后面使用 Visual Studio 或 Azure 服务时可访问一切所需的内容，以下是应添加到允许列表的 URL 和你可能需要打开的端口及协议。

| 服务或方案 | DNS 终结点 | 协议 | 端口 | 说明 |
| - | - | - | - | - |
| URL<br>解析 | go.microsoft.com<br><br>aka.ms | | | 用于缩短 URL，然后解析为更长的 URL |
| 起始页 | vsstartpage.blob.core.windows.net | | 443 | 用于显示起始页上显示的开发人员新闻（仅 Visual Studio 2017） |
| 目标<br> 通知 <br>服务 | targetednotifications.azurewebsites.net <br><br>www.research.net | | 80<br><br>443 | 用于将全局通知列表筛选为一个仅适用于特定类型计算机/使用方案的列表 |
| 扩展名 <br>更新检查 | marketplace.visualstudio.com<br><br>&#42;.windows.net <br>&#42;.microsoftonline.com <br>&#42;.live.com | | 443 | 用于在已安装扩展有可用更新时提供通知 <br><br> 用作登录位置 |
| AI 项目 <br>集成 | az861674.vo.msecnd.net | | 443<br> | 用于配置新项目，以将使用情况数据发送到你注册的 Application Insights 帐户 |
| 代码透镜 | codelensprodscus1su0.app。<br>codelens.visualstudio.com | | 443 | 用于在编辑器中提供有关上次更新文件的时间、更改的时间线、更改与之关联的工作项、作者等信息 |
| 实验 <br>功能启用 | visualstudio-devdiv-c2s.msedge.net | | 80 | 用于激活实验性新功能或功能更改 |
| 标识“徽章” <br>（用户名和虚拟形象）<br>和 <br>漫游设置 | app.vssps.visualstudio.com <br><br>app.vsspsext.visualstudio.com<br><br>app.vssps.visualstudio.com<br><br> ns-sb2-prod-ch1-002.cloudapp.net <br><br>az700632.vo.msecnd.net | | 443 | 用于在 IDE 中显示用户的名称和虚拟形象 <br><br> 用于确保设置更改从一台计算机漫游到另一台计算机 |
| 远程设置 | az700632.vo.msecnd.net | | 443 | 用于关闭已知会在 Visual Studio 中引发问题的扩展 |
| Windows 工具 | developer.microsoft.com <br><br>dev.windows.com  <br><br>appdev.microsoft.com | https | 443 | 用于 Windows 应用商店方案 |
| JSON 架构 <br>发现 <br><br>JSON 架构 <br>定义<br><br>JSON 架构 <br>支持 <br>Azure 资源 | json.schemastore.org <br>schemastoreorg.azurewebsites.net<br><br>json-schema.org<br><br>schema.management.azure.com | http<br>https<br><br>http<br><br>https | 80<br>443 <br><br> 443<br><br>443 | 用于发现和下载 JSON 架构，用户在编辑 JSON 文档时可能会用到此架构 <br><br>用于获取 JSON 的元验证架构<br><br>用于获取 Azure 资源管理器部署模板的当前架构 |
| NPM 包 <br>发现 | Skimdb.npmjs.com <br><br>Registry.npmjs.org <br><br>Api.npms.io | https<br><br>http/s<br><br>https | 443<br><br>80/443<br><br>443 | 搜索 NPM 包的必要条件，并用于 Web 项目中客户端脚本包的安装 |
| Bower 包<br> 图标<br><br>Bower 包 <br>search | Bower.io <br><br>bowercache.azurewebsites.net <br>go.microsoft.com <br>Registry.bower.io | http<br><br>https<br>http<br>https | 80<br><br>443<br>80<br>443 | 提供默认的 Bower 包图标  <br><br>提供搜索 Bower 包的能力 |
| NuGet<br><br>NuGet 程序包<br> 发现 | Api.nuget.org <br>www.nuget.org <br>Nuget.org<br><br>crl3.digicert.com <br>crl4.digicert.com <br>ocsp.digicert.com <br>cacerts.digicert.com | https<br><br>http/s | 443<br><br>80/443<br> | 用于验证签名的 NuGet 包。<br><br>搜索 NuGet 包和版本的必要条件 |
| GitHub 存储库信息 | api.github.com | https | 443 | 获取有关 Bower 包其他信息的必要条件 |
| Web Linters | Eslint.org<br><br>www.Bing.com <br><br>www.coffeelint.org | http | 80 | |
| Cookiecutter<br>资源管理器模板<br>发现 <br><br>Cookiecutter <br>资源管理器项目<br> 创建 | api.github.com <br>raw.githubusercontent.com <br>go.microsoft.com<br><br>pypi.org <br> pypi.python.org | https | 443<br> | 用于从我们建议的源和 github 存储库发现联机模板 <br><br>用于从 cookiecutter 模板创建一个项目，要求从 Python 包索引 (PyPI) 一次性按需安装 cookiecutter Python 包 |
| Python 包 <br>发现<br><br>Python 包 <br>管理<br><br>新建 <br>Python <br> 项目 <br>模板 | pypi.org<br> <br>pypi.python.org <br>bootstrap.pypa.io<br><br>go.microsoft.com | https | 443 | 提供搜索 pip 包的能力<br><br>用于自动安装 pip（如缺失） <br><br>用于将以下 Python 项目模板解析为 cookiecutter 模板 URL：<br> - 分类器项目<br>- 聚类分析项目 <br> - 回归项目 <br> - 使用 PyKinect 的 PyGame <br> - Pyvot 项目 |
| Office Web <br>Add-in — 外接程序 <br> file:/// <br>确认 <br>服务 | verificationservice.osi.office.net | https | 443 | 用于验证 Office Web 外接程序的清单 |
| SharePoint 和 <br>Office 外接程序 | sharepoint.com | https | 443 | 用于将 SharePoint 和 Office 外接程序发布到 SharePoint Online 并对其进行测试 |
| 工作流管理器 <br>测试服务<br> 主机 | | http | 12292 | 自动创建的防火墙规则，用于测试带工作流的 SharePoint 外接程序 |
| 自动收集 <br>可靠性统计信息 <br>和其他 <br>客户体验 <br>改善计划 (CEIP)<br> 面向 Azure SDK 和 <br>面向 SQL 工具 <br><br> | vortex.data.microsoft.com<br> <br>dc.services.visualstudio.com | https | 443 | 用于将可靠性统计信息（故障/挂起数据）从用户发送到 Microsoft。 在启用 Windows 错误报告的情况下，仍将上传实际故障/挂起转储；只会禁止统计信息； <br>用于向 Visual Studio 显示 Azure Tools SDK 扩展的匿名使用模式，并向 Visual Studio 显示 SQL 工具的使用模式 |
| Visual Studio <br> 客户体验 <br>改善计划 (CEIP) <br><br>PerfWatson.exe | vortex.data.microsoft.com<br>dc.services.visualstudio.com<br>visualstudio-devdiv-c2s.msedge.net<br>az667904.vo.msecnd.net <br>scus-breeziest-in.cloudapp.net<br> | https | 443 | 用于收集匿名使用模式和错误日志 <br><br>用于跟踪 UI 冻结问题 |
| 创建和<br>管理 <br>Azure 资源 | management.azure.com <br>management.core.windows.net | https | 443 | 用于创建 Azure 网站或其他资源，以支持 Web 应用、Azure Functions 或 WebJobs 的发布 |
| 更新的 Web 发布工具 <br>检查和扩展 <br>建议 | marketplace.visualstudio.com | https | 443 | 用于检查已更新发布工具的可用性。 如果禁用，则可能不会显示用于 Web 发布的潜在建议扩展 |
| 更新的 Azure 资源 <br>创建终结点信息 | \*.blob.core.windows.net | https | 443 | 用于更新在为某些 Azure 服务创建 Azure 资源时使用的终结点。 如果禁用，则改为使用在终结点位置中最后一次下载或生成的资源 |
| 远程调试和 <br>远程分析 <br>Azure 网站 | &#42;.cloudapp.net <br> &#42;.azurewebsites.net | | 4022 | 用于将远程调试器附加到 Azure 网站。 如果禁用，将远程调试器附加到 Azure 网站将不起作用 |
| Active Directory <br>Graph | graph.windows.net | https | 443 | 用于预配新的 Azure Active Directory 应用程序。 也由 Office 365 MSGraph - 已连接的服务提供程序使用 |
| Azure Functions <br>CLI 更新 <br>检查 | functionscdn.azureedge.net | https | 443 | 用于检查 Azure Functions CLI 的更新版本。 如果禁用，将改为使用 CLI 的缓存副本（或 Azure Functions 组件提供的副本） |
| Cordova | npmjs.org<br>gradle.org | http/s | 80/443 | HTTP 用于在生成期间下载 Gradle；HTTP 用于包含项目中的 Cordova 插件 |
| Cloud Explorer | 1. &#60;clusterendpoint&#62; <br>Service Fabric <br>2. &#60;management endpoint&#62;<br>常规 Cloud Exp <br>3. &#60;graph endpoint&#62;<br>常规 Cloud Exp<br>4. &#60;storage account endpoint&#62;<br>存储节点 <br>5. &#60;Azure portal URLs&#62;<br>常规 Cloud Exp <br>6. &#60;key vault endpoints&#62; <br>Azure 资源管理器 VM 节点<br>7. &#60;PublicIPAddressOfCluster&#62;<br>Service Fabric 远程调试和 ETW 跟踪 | <br>1. https<br>2. https<br>3. https<br>4. https<br>5. https<br>6. https<br>7: tcp | 1. 19080<br>2. 443 <br>3. 443 <br>4. 443 <br>5. 443 <br>6. 443 <br>7. 动态 | 1.示例：test12.eastus.cloudapp.com<br>2.检索订阅并检索/管理 Azure 资源<br>3.检索 Azure Stack 订阅<br>4.管理存储资源（示例：mystorageaccount.blob.core.windows.net）<br>5.“在门户中打开”上下文菜单选项（在 Azure 门户中打开资源）<br>6.创建并使用 Key Vault 进行 VM 调试（示例：myvault.vault.azure.net） <br><br>7.基于群集中的节点数和可用端口动态分配端口块。 <br><br>一个端口块将尝试获取至少 10 个端口的 3 倍数量的节点。<br><br>对于流式处理跟踪，将尝试从 810 获取端口块。 如果任何端口块都已被使用，则尝试获取下一个端口块，依次类推。 （如果负载均衡器为空，则很可能使用来自 810 的端口） <br><br>对于调试是同样道理，将保留四个端口块集： <br>- connectorPort:30398, <br>- forwarderPort:31398, <br>- forwarderPortx86:31399,<br>- fileUploadPort:32398<br> |
| 云服务 | 1.RDP<br><br>2. core.windows.net <br><br>3.  management.azure.com<br> management.core.windows.net <br><br>4. &#42;.blob.core.windows.net <br>&#42;.queue.core.windows.net<br>&#42;.table.core.windows.net <br><br>5. portal.azure.com <br><br>6. &#60;user's cloud service&#62;.cloudapp.net <br> &#60;user's VM&#62;.&#60;region&#62;.azure.com | 1. rdp <br><br> 2. https <br><br> 3. https <br><br> 4. https <br><br> 5. https <br><br>6. tcp | 1. 3389 <br><br> 2. 443 <br><br> 3. 443 <br><br>4. 443 <br><br>5. 443 <br><br> 6. a) 30398 <br> 6. b) 30400 <br> 6. c) 31398 <br> 6. d) 31400 <br> 6. e) 32398 <br> 6. f) 32400 | 1.云服务 VM 的远程桌面 <br><br> 2.专用诊断配置的存储帐户组件 <br><br> 3.Azure 门户 <br><br> 4.服务器资源管理器 - Azure 存储  &#42; 为客户命名的存储帐户  <br><br> 5.用于打开门户的链接 &#47;下载订阅证书 &#47;发布设置文件 <br><br>6. a)  用于云服务和 VM 远程调试的连接器本地端口<br> 6. b)  用于云服务和 VM 远程调试的连接器公用端口 <br> 6. c)  用于云服务和 VM 远程调试的转发器本地端口 <br> 6. d) 用于云服务和 VM 远程调试的转发器公用端口  <br> 6. e) 用于云服务和 VM 远程调试的文件上传程序本地端口 <br> 6. f) 用于云服务和 VM 远程调试的文件上传程序公用端口 |
| Service Fabric | 1. <br>ocs.Microsoft.com<br>aka.ms <br>go.microsoft.com <br><br>2. <br>vssftools.blob.core.windows.net <br>Vault.azure.com <br>Portal.azure.com <br><br> 3. &#42; vault.azure.net<br><br> 4. <br>app.vsaex.visualstudio.com<br>&#42; .vsspsext.visualstudio.com<br>clouds.vsrm.visualstudio.com <br>clouds.visualstudio.com<br>app.vssps.visualstudio.com <br>&#42; .visualstudio.com | https | 443 | 1.文档 <br><br> 2.创建群集功能 <br><br>3.&#42; 为 Azure Key Vault 名称（示例：test11220180112110108.vault.azure.net）  <br><br>  4.&#42; 为动态（示例：vsspsextprodch1su1.vsspsext.visualstudio.com） |
| 快照 <br>调试器 | 1. go.microsoft.com <br>2. management.azure.com <br> 3. &#42;azurewebsites.net <br> 4. &#42;scm.azurewebsites.net<br>5. api.nuget.org/v3/index.json <br>6. msvsmon | 1. https <br>2. https  <br>3. http <br>4. https <br>5. https <br>6.Concord <br> | 1. 443<br> 2. 443<br>3. 80  <br>4. 443<br> 5. 443<br> 6. 4022（Visual Studio 从属版本） | 1.查询 .json 文件的应用服务 SKU 大小 <br>2.各种 Azure RM 调用 <br>3.站点预热调用渠道  <br>4.客户的目标应用服务 Kudu 终结点 <br>5.查询 nuget.org 中发布的站点扩展版本 <br>6.远程调试通道 |
| Azure 流分析 <br><br>HDInsight | Management.azure.com | https | 443 | 用于查看、提交、运行和管理 ASA 作业 <br><br> 用于浏览 HDI 群集，以及提交、诊断和调试 HDI 作业 |
| Azure Data Lake | &#42;.azuredatalakestore.net <br>&#42;.azuredatalakeanalytics.net | https | 443 | 用于编译、提交、查看、诊断和调试作业；用于浏览 ADLS 文件；用于上传和下载文件 |
| 打包服务 | [account].visualstudio.com <br/> [account].\*.visualstudio.com <br/> \*.blob.core.windows.net <br/> registry.npmjs.org </br> nodejs.org <br/> dist.nuget.org <br/> nuget.org | https | 443 | 仅特定生成任务方案（例如：NuGet 工具安装程序、节点工具安装程序）或者打算将公共上游与源结合使用时才需使用 \*.npmjs.org、\*.nuget.org 和 \*.nodejs.org。 要使用打包服务的核心功能，还需具备其他三个域。 |
| Azure DevOps Services | \*.vsassets.io <br/> static2.sharepointonline.com <br/> dev.azure.com | | | 用于连接 Azure DevOps Services |
| | | | | |

## <a name="troubleshoot-network-related-errors"></a>与网络相关错误的疑难解答

有时，当你在防火墙或代理服务器后安装或使用 Visual Studio 时，可能会遇到与网络或代理相关的错误。 有关此类错误消息的解决方案的详细信息，请参阅[安装或使用 Visual Studio 时与网络相关错误的疑难解答](troubleshooting-network-related-errors-in-visual-studio.md)页面。

## <a name="get-support"></a>获取支持

对于安装相关问题，我们提供[实时聊天  ](https://visualstudio.microsoft.com/vs/support/#talktous)（仅限英语）支持选项。

下面是另外几个支持选项：

* 通过[报告问题](../ide/how-to-report-a-problem-with-visual-studio.md)工具（会出现在 Visual Studio 安装程序和 Visual Studio IDE 中）向我们报告产品问题。
* 在 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/)中，可提出功能建议、跟踪产品问题，并能找到答案。
* 使用你的 [GitHub](https://github.com/) 帐户，通过 [Gitter 社区的 Visual Studio 对话](https://gitter.im/Microsoft/VisualStudio)与我们和其他 Visual Studio 开发人员进行交流。

## <a name="see-also"></a>请参阅

* [Live Share 连接性要求](/visualstudio/liveshare/reference/connectivity/)
* [创建 Visual Studio 的网络安装](create-a-network-installation-of-visual-studio.md)
* [对 Visual Studio 中与网络相关错误的故障排除](troubleshooting-network-related-errors-in-visual-studio.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [在防火墙或代理服务器后安装 (Visual Studio for Mac)](/visualstudio/mac/install-behind-a-firewall-or-proxy-server)
