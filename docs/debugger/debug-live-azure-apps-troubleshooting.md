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
ms.openlocfilehash: 16d55c4e729a39f46b4b038490e92f7cb43bf98d
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84182867"
---
# <a name="troubleshooting-and-known-issues-for-snapshot-debugging-in-visual-studio"></a>Visual Studio 中的快照调试疑难解答和已知问题

如果本文中所述的步骤不能解决问题，请在[开发者社区](https://developercommunity.visualstudio.com/spaces/8/index.html)中搜索相应问题，或者通过在 Visual Studio 中选择“帮助” > “发送反馈” > “报告问题”来报告新问题  。

## <a name="issue-attach-snapshot-debugger-encounters-an-http-status-code-error"></a>问题：“附加 Snapshot Debugger”遇到 HTTP 状态代码错误

如果尝试附加时在“输出”窗口中看到以下错误，则可能是由下面列出的已知问题导致的。 请尝试建议的解决方案，如果问题仍然存在，请联系之前的别名。

`[TIMESTAMP] Error --- Unable to Start Snapshot Debugger - Attach Snapshot Debugger failed: System.Net.WebException: The remote server returned an error: (###) XXXXXX`

### <a name="401-unauthorized"></a>(401) 未经授权

此错误表示 Visual Studio 向 Azure 发出的 REST 调用使用了无效的凭据。 

执行以下步骤：

* 确保 Visual Studio 个性化帐户对 Azure 订阅和要附加的资源具有相应权限。 一种快速确定方法是检查该资源是否出现在“调试” > “附加 Snapshot Debugger…” > “Azure 资源” > “选择现有资源”的对话框或 Cloud Explorer 中   。
* 如果此错误仍然存在，请使用本文开头所述的任一反馈渠道进行反馈。

如果已在应用服务上启用身份验证/授权 (EasyAuth)，则可能会遇到 401 错误，并且调用堆栈错误消息中会显示 LaunchAgentAsync。 请确保在 Azure 门户中将“请求未通过身份验证时采取的操作”设置为“允许匿名请求(不执行任何操作)”，并改为在 D:\Home\sites\wwwroot 中提供包含以下内容的 authorization.json 。 

```
{
  "routes": [
    {
      "path_prefix": "/",
      "policies": {
        "unauthenticated_action": "RedirectToLoginPage"
      }
    },
    {
      "http_methods": [ "POST" ],
      "path_prefix": "/41C07CED-2E08-4609-9D9F-882468261608/api/agent",
      "policies": {
        "unauthenticated_action": "AllowAnonymous"
      }
    }
  ]
}
```

第一种途径类似于“使用 [IdentityProvider] 登录”，它能够有效地保护你的应用域。 第二种途径在身份验证之外公开 SnapshotDebugger AgentLaunch 终结点，它只有在应用服务启用了 SnapshotDebugger 预安装站点扩展的情况下，才会执行启动 SnapshotDebugger 诊断代理的预定义操作。 有关 authorization.json 配置的更多详细信息，请参阅 [URL 授权规则](https://azure.github.io/AppService/2016/11/17/URL-Authorization-Rules.html)。

### <a name="403-forbidden"></a>(403) 禁止

此错误表示权限被拒绝。 这可能是由许多不同的问题导致的。

执行以下步骤：

* 验证 Visual Studio 帐户是否具有有效的 Azure 订阅，并对该资源具有必要的基于角色的访问控制 (RBAC) 权限。 对于 AppService，请检查是否有权[查询](/rest/api/appservice/appserviceplans/get)托管应用的应用服务计划。
* 验证客户端计算机的时间戳是否是正确且最新的。 如果服务器的时间戳与请求时间戳相差 15 分钟以上，则通常会产生此错误。
* 如果此错误仍然存在，请使用本文开头所述的任一反馈渠道进行反馈。

### <a name="404-not-found"></a>(404) 未找到

此错误表示在服务器上找不到该网站。

执行以下步骤：

* 验证是否已在要附加的应用服务资源上部署并运行网站。
* 验证该站点在 https://\<resource\>.azurewebsites.net 上是否可用
* 验证在访问 https://\<resource\>.azurewebsites.net 时，正常运行的自定义 Web 应用是否不会返回状态码 404
* 如果此错误仍然存在，请使用本文开头所述的任一反馈渠道进行反馈。

### <a name="406-not-acceptable"></a>(406) 不可接受

此错误表示服务器无法响应请求的“接受”标头中设置的类型。

执行以下步骤：

* 验证你的站点在 https://\<resource\>.azurewebsites.net 上是否可用
* 验证站点是否尚未迁移到新实例。 Snapshot Debugger 采用 ARRAffinity 的概念，将请求路由到特定实例，这可能会间歇性地产生此错误。
* 如果此错误仍然存在，请使用本文开头所述的任一反馈渠道进行反馈。

### <a name="409-conflict"></a>(409) 冲突

此错误表示请求与当前服务器状态冲突。

这是一个已知问题，在用户尝试将 Snapshot Debugger 附加到已启用 ApplicationInsights 的 AppService 时会发生。 ApplicationInsights 使用与 Visual Studio 不同的大小写设置 AppSettings，从而导致此问题。

::: moniker range=">= vs-2019"
我们已在 Visual Studio 2019 中解决了此问题。
::: moniker-end

执行以下步骤：

::: moniker range="vs-2017"

* 在 Azure 门户中验证 SnapshotDebugger (SNAPSHOTDEBUGGER_EXTENSION_VERSION) 和 InstrumentationEngine (INSTRUMENTATIONENGINE_EXTENSION_VERSION) 的 AppSettings 是否为大写。 如果不是，请手动更新这些设置，这会强制重启站点。
::: moniker-end
* 如果此错误仍然存在，请使用本文开头所述的任一反馈渠道进行反馈。

### <a name="500-internal-server-error"></a>(500) 内部服务器错误

此错误表示站点已完全关闭或服务器无法处理请求。 Snapshot Debugger 仅在正在运行的应用程序上运行。 [Application Insights Snapshot Debugger](/azure/azure-monitor/app/snapshot-debugger) 可提供有关异常的快照，并且可能是满足需求的最佳工具。

### <a name="502-bad-gateway"></a>(502) 错误的网关

此错误表示服务器端网络出现问题，可能是暂时性的。

执行以下步骤：

* 请尝试等待几分钟，然后再次附加 Snapshot Debugger。
* 如果此错误仍然存在，请使用本文开头所述的任一反馈渠道进行反馈。

## <a name="issue-snappoint-does-not-turn-on"></a>问题：快照点未启用

如果快照点带有警告图标 ![快照点警告图标](../debugger/media/snapshot-troubleshooting-snappoint-warning-icon.png "快照点警告图标")，而不是常规快照点图标，则表示快照点未启用。

![快照点未启用](../debugger/media/snapshot-troubleshooting-dont-turn-on.png "快照点未启用")

执行以下步骤：

1. 确保生成和部署应用时使用的是相同版本的源代码。 确保为你的部署加载了正确的符号。 为此，请在快照调试时查看“模块”窗口并验证“符号文件”列是否显示为调试的模块加载的 .pdb 文件。 Snapshot Debugger 将尝试自动下载符号并将其用于你的部署。

## <a name="issue-symbols-do-not-load-when-i-open-a-snapshot"></a>问题：打开快照时未加载符号

如果你看到以下窗口，则表示符号未加载。

![未加载符号](../debugger/media/snapshot-troubleshooting-symbols-wont-load.png "未加载符号")

执行以下步骤：

- 单击此页上的“更改符号设置...” 链接。 在“调试”>“符号”设置中，添加符号缓存目录。 设置符号路径后，重启快照调试。

   项目中可用的符号或 .pdb 文件必须与应用服务部署匹配。 大多数部署（通过 Visual Studio、使用 Azure Pipelines 的 CI/CD 或 Kudu 等进行的部署）会将你的符号文件一起发布到应用服务。 通过设置符号缓存目录，Visual Studio 可以使用这些符号。

   ![符号设置](../debugger/media/snapshot-troubleshooting-symbol-settings.png "符号设置")

- 或者，如果你的组织使用符号服务器或将符号置于不同的路径，请使用符号设置为你的部署加载正确的符号。

## <a name="issue-i-cannot-see-the-attach-snapshot-debugger-option-in-the-cloud-explorer"></a>问题：在 Cloud Explorer 中看不到“附加 Snapshot Debugger”选项

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

## <a name="issue-i-only-see-throttled-snapshots-in-the-diagnostic-tools"></a>问题：在诊断工具中只能看到已阻止的快照

![已阻止的快照点](../debugger/media/snapshot-troubleshooting-throttled-snapshots.png "已阻止的快照点")

执行以下步骤：

- 快照占用很少的内存，但确实存在内存使用。 如果 Snapshot Debugger 检测到服务器的内存负载过大，则不会创建快照。 可以通过停止 Snapshot Debugger 会话来删除已捕获的快照，然后重试。

::: moniker range=">= vs-2019"
## <a name="issue-snapshot-debugging-with-multiple-versions-of-the-visual-studio-gives-me-errors"></a>问题：使用多个版本的 Visual Studio 调试快照时出错

Visual Studio 2019 需要在 Azure 应用服务上使用更新版本的 Snapshot Debugger 站点扩展。  此版本与 Visual Studio 2017 所用的旧版 Snapshot Debugger 站点扩展不兼容。  如果尝试将 Visual Studio 2019 中的 Snapshot Debugger 附加到之前已由 Visual Studio 2017 中的 Snapshot Debugger 进行调试的 Azure 应用服务，会收到以下错误：

![不兼容的 Snapshot Debugger 站点扩展 Visual Studio 2019](../debugger/media/snapshot-troubleshooting-incompatible-vs2019.png "不兼容的 Snapshot Debugger 站点扩展 Visual Studio 2019")

相反，如果使用 Visual Studio 2017 将 Snapshot Debugger 附加到之前已由 Visual Studio 2019 中的 Snapshot Debugger 进行调试的 Azure 应用服务，则会收到以下错误：

![不兼容的 Snapshot Debugger 站点扩展 Visual Studio 2017](../debugger/media/snapshot-troubleshooting-incompatible-vs2017.png "不兼容的 Snapshot Debugger 站点扩展 Visual Studio 2017")

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
  - 代理日志存储在以下目录：D:\home\LogFiles\SiteExtensions\DiagnosticsAgentLogs\
- VM/VMSS：
  - 登录到 VM，代理日志存储在以下位置：C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<Version>\SnapshotDebuggerAgent_*.txt
- AKS
  - 导航到以下目录：/tmp/diag/AgentLogs/*

### <a name="enable-profilerinstrumentation-logs"></a>启用 Profiler/检测日志

可以在以下位置找到检测日志：

- 应用服务：
  - 错误日志记录将自动发送到 D:\Home\LogFiles\eventlog.xml，事件标记为 `<Provider Name="Instrumentation Engine" />` 或“生产断点”
- VM/VMSS：
  - 登录到 VM 并打开事件查看器。
  - 打开以下视图：“Windows 日志”>“应用程序”。
  - 使用生产断点或检测引擎按事件源 筛选当前日志。
- AKS
  - 检测引擎日志记录路径如下：/tmp/diag/log.txt（在 DockerFile 中设置 MicrosoftInstrumentationEngine_FileLogPath）
  - 生产断点日志记录路径如下：/tmp/diag/shLog.txt

## <a name="known-issues"></a>已知问题

- 当前不支持使用多个 Visual Studio 客户端对同一个应用服务进行快照调试。
- ASP.NET Core 项目不完全支持 Roslyn IL 优化。 对于部分 ASP.NET Core 项目，你可能无法看到某些变量，或者无法在条件语句中使用某些变量。
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
- [使用 Snapshot Debugger 调试实时 ASP.NET Azure 虚拟机或虚拟机规模集](../debugger/debug-live-azure-virtual-machines.md)
- [使用 Snapshot Debugger 调试实时 ASP.NET Azure Kubernetes](../debugger/debug-live-azure-kubernetes.md)
- [快照调试常见问题解答](../debugger/debug-live-azure-apps-faq.md)
