---
title: 快照调试疑难解答 | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2019
ms.topic: troubleshooting
helpviewer_keywords:
- debugger
ms.assetid: 511a0697-c68a-4988-9e29-8d0166ca044a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 27df4c097d829a4d28a77b9b1ad96eb389f4096c
ms.sourcegitcommit: dc12a7cb66124596089f01d3e939027ae562ede9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71962933"
---
# <a name="troubleshooting-and-known-issues-for-snapshot-debugging-in-visual-studio"></a>Visual Studio 中的快照调试疑难解答和已知问题

如果本文中所述的步骤不能解决问题，请在[开发人员社区](https://developercommunity.visualstudio.com/spaces/8/index.html)中搜索问题，或通过选择 "**帮助**"  > **发送反馈**@no__t**来报告新**问题。

## <a name="issue-attach-snapshot-debugger-encounters-an-http-status-code-error"></a>问题："附加 Snapshot Debugger" 遇到 HTTP 状态代码错误

如果尝试附加期间在 "**输出**" 窗口中看到以下错误，则可能是下面列出的已知问题。 尝试建议的解决方案，如果此问题仍然存在，请联系上一个别名。

`[TIMESTAMP] Error --- Unable to Start Snapshot Debugger - Attach Snapshot Debugger failed: System.Net.WebException: The remote server returned an error: (###) XXXXXX`

### <a name="401-unauthorized"></a>（401）未授权

此错误表示 Visual Studio 向 Azure 发出的 REST 调用使用无效的凭据。 具有 Azure Active Directory Easy OAuth 模块的已知 bug 可能会产生此错误。

执行以下步骤：

* 确保你的 Visual Studio 个性化帐户有权访问你要附加到的 Azure 订阅和资源。 若要确定这一点，一种方法是检查资源是否在 "**调试** > **附加 Snapshot Debugger** " 对话框中可用。@no__t 的**Azure 资源** > **选择现有**，或在 Cloud Explorer 中。
* 如果此错误仍然存在，请使用本文开头所述的反馈通道之一。

### <a name="403-forbidden"></a>（403）禁止访问

此错误表示权限被拒绝。 这可能是由许多不同的问题导致的。

执行以下步骤：

* 验证你的 Visual Studio 帐户是否具有有效的 Azure 订阅，以及该资源所需的基于角色的访问控制（RBAC）权限。 对于 AppService，请检查你是否有权[查询](https://docs.microsoft.com/rest/api/appservice/appserviceplans/get)托管应用的应用服务计划。
* 验证客户端计算机的时间戳是否正确并处于最新状态。 时间戳超过15分钟的请求时间戳的服务器通常会产生此错误。
* 如果此错误仍然存在，请使用本文开头所述的反馈通道之一。

### <a name="404-not-found"></a>（404）找不到

此错误表示无法在服务器上找到网站。

执行以下步骤：

* 验证是否已在要附加到的应用服务资源上部署并运行网站。
* 验证站点是否在 https://\<resource\>.azurewebsites.net 上可用。
* 当在 https://\<resource\>.azurewebsites.net 中访问时，验证正确运行的自定义 web 应用程序未返回状态代码404
* 如果此错误仍然存在，请使用本文开头所述的反馈通道之一。

### <a name="406-not-acceptable"></a>（406）不可接受

此错误表示服务器无法响应请求的 Accept 标头中的类型集。

执行以下步骤：

* 验证你的站点在 https://\<resource\>.azurewebsites.net 可用。
* 验证你的站点是否尚未迁移到新实例。 Snapshot Debugger 使用 ARRAffinity 的概念将请求路由到特定实例，这可能会导致此错误。
* 如果此错误仍然存在，请使用本文开头所述的反馈通道之一。

### <a name="409-conflict"></a>（409）冲突

此错误表示请求与当前服务器状态冲突。

这是一个已知问题，当用户尝试将 Snapshot Debugger 附加到已启用 Applicationinsights.config 的 AppService 时，会出现此问题。 Applicationinsights.config 将 AppSettings 设置为与 Visual Studio 的大小写不同，从而导致此问题。

::: moniker range=">= vs-2019"
我们已在 Visual Studio 2019 中解决了此情况。
::: moniker-end

执行以下步骤：

::: moniker range="vs-2017"

* 在 Azure 门户中验证 SnapshotDebugger （SNAPSHOTDEBUGGER_EXTENSION_VERSION）和 InstrumentationEngine （INSTRUMENTATIONENGINE_EXTENSION_VERSION）的 AppSettings 是否为大写字母。 如果没有，请手动更新设置，这会强制重新启动站点。
::: moniker-end
* 如果此错误仍然存在，请使用本文开头所述的反馈通道之一。

### <a name="500-internal-server-error"></a>（500）内部服务器错误

此错误表示站点完全关闭，或者服务器无法处理该请求。 仅 Snapshot Debugger 运行的应用程序的功能。 [Application Insights Snapshot Debugger](https://docs.microsoft.com/azure/azure-monitor/app/snapshot-debugger)提供有关异常的快照，可能是满足你的需求的最佳工具。

### <a name="502-bad-gateway"></a>（502）错误的网关

此错误表示服务器端网络问题，可能是暂时性的。

执行以下步骤：

* 请尝试等待几分钟，然后再次附加 Snapshot Debugger。
* 如果此错误仍然存在，请使用本文开头所述的反馈通道之一。

## <a name="issue-snappoint-does-not-turn-on"></a>问题：吸附点未启用

如果你的快照点带有警告图标 ![快照点警告图标](../debugger/media/snapshot-troubleshooting-snappoint-warning-icon.png "快照点警告图标")，而不是常规快照点图标，则表示快照点未启用。

![快照点未启用](../debugger/media/snapshot-troubleshooting-dont-turn-on.png "快照点未开启")

执行以下步骤：

1. 请确保具有用于生成和部署应用的相同版本的源代码。 确保为你的部署加载了正确的符号。 为此，请在快照调试时查看“模块”窗口并验证“符号文件”列是否显示为调试的模块加载的 .pdb 文件。 Snapshot Debugger 将尝试自动下载符号并将其用于你的部署。

## <a name="issue-symbols-do-not-load-when-i-open-a-snapshot"></a>问题：打开快照时未加载符号

如果你看到以下窗口，则表示符号未加载。

![未加载符号](../debugger/media/snapshot-troubleshooting-symbols-wont-load.png "未加载符号")

执行以下步骤：

- 单击此页上的“更改符号设置...” 链接。 在“调试”>“符号”设置中，添加符号缓存目录。 设置符号路径后，重启快照调试。

   项目中可用的符号或 .pdb 文件必须与应用服务部署匹配。 大多数部署（通过 Visual Studio、使用 Azure Pipelines 的 CI/CD 或 Kudu 等进行的部署）会将你的符号文件一起发布到应用服务。 通过设置符号缓存目录，Visual Studio 可以使用这些符号。

   ![符号设置](../debugger/media/snapshot-troubleshooting-symbol-settings.png "符号设置")

- 或者，如果你的组织使用符号服务器或将符号置于不同的路径，请使用符号设置为你的部署加载正确的符号。

## <a name="issue-i-cannot-see-the-attach-snapshot-debugger-option-in-the-cloud-explorer"></a>问题：我看不到 Cloud Explorer 中的 "附加 Snapshot Debugger" 选项

执行以下步骤：

- 确保安装了 Snapshot Debugger 组件。 打开 Visual Studio 安装程序，然后选中 Azure 工作负载中的“Snapshot Debugger”组件。
::: moniker range="< vs-2019"
- 确保你的应用受支持。 目前，仅支持部署到 Azure 应用服务的 ASP.NET（4.6.1 及更高版本）和 ASP.NET Core（2.0及更高版本）应用。
::: moniker-end
::: moniker range=">= vs-2019"
- 确保你的应用受支持：
  - Azure 应用服务 - 在 .NET Framework 4.6.1 或更高版本上运行的 ASP.NET 应用程序。
  - Azure 应用服务 - 在 Windows 中的 .Net Core 2.0 或更高版本上运行的 ASP.NET Core 应用程序。
  - Azure 虚拟机（以及虚拟机规模集）- 在 .NET Framework 4.6.1 或更高版本上运行的 ASP.NET 应用程序。
  - Azure 虚拟机（以及虚拟机规模集）- 在 Windows 中的 .Net Core 2.0 或更高版本上运行的 ASP.NET Core 应用程序。
  - Azure Kubernetes 服务 - 在 Debian 9 中的 .Net Core 2.2 或更高版本上运行的 ASP.NET Core 应用程序。
  - Azure Kubernetes 服务 - 在 Alpine 3.8 中的 .Net Core 2.2 或更高版本上运行的 ASP.NET Core 应用程序。
  - Azure Kubernetes 服务 - 在 Ubuntu 18.04 中的 .Net Core 2.2 或更高版本上运行的 ASP.NET Core 应用程序。
::: moniker-end

## <a name="issue-i-only-see-throttled-snapshots-in-the-diagnostic-tools"></a>问题：仅在诊断工具中看到限制的快照

![已阻止的快照点](../debugger/media/snapshot-troubleshooting-throttled-snapshots.png "已阻止的快照点")

执行以下步骤：

- 快照占用很少的内存，但确实存在内存使用。 如果 Snapshot Debugger 检测到服务器的内存负载过大，则不会创建快照。 可以通过停止 Snapshot Debugger 会话来删除已捕获的快照，然后重试。

::: moniker range=">= vs-2019"
## <a name="issue-snapshot-debugging-with-multiple-versions-of-the-visual-studio-gives-me-errors"></a>问题：具有多个版本的 Visual Studio 的快照调试给出了错误

Visual Studio 2019 需要 Azure App Service 上的 Snapshot Debugger 站点扩展的较新版本。  此版本与 Visual Studio 2017 使用的 Snapshot Debugger 站点扩展的旧版本不兼容。  如果尝试将 Visual Studio 2019 中的 Snapshot Debugger 附加到之前已由 Visual Studio 2017 中的 Snapshot Debugger 调试的 Azure App Service，则将收到以下错误：

![不兼容 Snapshot Debugger 站点扩展 Visual studio 2019](../debugger/media/snapshot-troubleshooting-incompatible-vs2019.png "不兼容 Snapshot Debugger 站点扩展 visual studio 2019")

相反，如果使用 Visual Studio 2017 将 Snapshot Debugger 附加到之前已由 Visual Studio 2019 中的 Snapshot Debugger 调试的 Azure App Service，则将收到以下错误：

![不兼容 Snapshot Debugger 站点扩展 Visual studio 2017](../debugger/media/snapshot-troubleshooting-incompatible-vs2017.png "不兼容 Snapshot Debugger 站点扩展 visual studio 2017")

若要解决此问题，请在 Azure 门户中删除以下应用设置，并再次附加 Snapshot Debugger：

- INSTRUMENTATIONENGINE_EXTENSION_VERSION
- SNAPSHOTDEBUGGER_EXTENSION_VERSION
::: moniker-end

## <a name="issue-i-am-having-problems-snapshot-debugging-and-i-need-to-enable-more-logging"></a>问题：快照调试出现问题，需要启用更多日志记录

### <a name="enable-agent-logs"></a>启用代理日志

若要启用和禁用代理日志记录，请打开 Visual Studio 并导航到“工具”>“选项”>“Snapshot Debugger”>“启用代理日志记录”。 请注意，如果同时还启用了“在会话启动时删除旧的代理日志”，则每次成功的 Visual Studio 附加都会删除以前的代理日志。

可以在以下位置找到代理日志：

- 应用服务：
  - 导航到应用服务的 Kudu 站点（即，yourappservice.scm.azurewebsites.net）并导航到调试控制台。
  - 代理日志存储在以下目录中：D:\home\LogFiles\SiteExtensions\DiagnosticsAgentLogs\
- VM/VMSS：
  - 登录到 VM，代理日志按如下方式存储：C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<Version>\SnapshotDebuggerAgent_*.txt
- AKS
  - 导航到以下目录：/tmp/diag/AgentLogs/*

### <a name="enable-profilerinstrumentation-logs"></a>启用 Profiler/检测日志

可以在以下位置找到检测日志：

- 应用服务：
  - 错误日志记录自动发送到 D:\Home\LogFiles\eventlog.xml，事件标有 @no__t 0 或 "生产断点"。
- VM/VMSS：
  - 登录到 VM 并打开事件查看器。
  - 打开以下视图：*Windows 日志 > 应用程序*。
  - 使用生产断点或检测引擎按事件源筛选当前日志。
- AKS
  - 检测引擎日志记录路径如下：/tmp/diag/log.txt（在 DockerFile 中设置 MicrosoftInstrumentationEngine_FileLogPath）
  - 生产断点日志记录路径如下：/tmp/diag/shLog.txt

## <a name="known-issues"></a>已知问题

- 当前不支持使用多个 Visual Studio 客户端对同一个应用服务进行快照调试。
- ASP.NET Core 项目不完全支持 Roslyn IL 优化。 对于某些 ASP.NET Core 项目，你可能无法看到某些变量或条件语句中使用某些变量。
- 无法在 ASP.NET Core 项目的条件语句或记录点中计算特殊变量（如 $FUNCTION 或 $CALLER）。
- 快照调试不适用于已启用[本地缓存](/azure/app-service/app-service-local-cache)的应用服务。
- 目前不支持快照调试 API 应用。

## <a name="site-extension-upgrade"></a>站点扩展升级

快照调试和 Application Insights 依赖于 ICorProfiler，该工具会加载到站点过程并在升级过程中导致文件锁定问题。 我们建议使用此过程来确保生产站点不会出现任何停机时间。

- 在应用服务中创建[部署槽位](/azure/app-service/web-sites-staged-publishing)并将你的站点部署到槽。
- 从 Visual Studio 中的 Cloud Explorer 或从 Azure 门户交换生产槽。
- 停止槽站点。 这将需要几秒钟来终止所有实例的站点 w3wp.exe 进程。
- 从 Kudu 站点或 Azure 门户升级槽站点扩展（“应用服务边栏选项卡”>“开发工具”>“扩展”>“更新”）。
- 启动槽站点。 建议访问该站点以再次将其预热。
- 交换生产槽。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.yml)
- [使用快照调试器调试实时 ASP.NET 应用](../debugger/debug-live-azure-applications.md)
- [使用 Snapshot Debugger 调试实时 ASP.NET Azure Virtual Machines\Virtual 计算机规模集](../debugger/debug-live-azure-virtual-machines.md)
- [使用 Snapshot Debugger 调试实时 ASP.NET Azure Kubernetes](../debugger/debug-live-azure-kubernetes.md)
- [快照调试常见问题解答](../debugger/debug-live-azure-apps-faq.md)
