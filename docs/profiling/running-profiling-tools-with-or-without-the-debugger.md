---
title: 运行带或不带调试器的分析工具 | Microsoft Docs
ms.date: 11/04/2018
ms.topic: conceptual
ms.assetid: 3fcdccad-c1bd-4c67-bcec-bf33a8fb5d63
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 273dc6770f2928ed65d6a473b7f1986bc353687e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62999480"
---
# <a name="run-profiling-tools-with-or-without-the-debugger"></a>运行带/不带调试器的分析工具

Visual Studio 提供了性能测量值和分析工具选择。 某些工具（如“CPU 使用情况”和“内存使用情况”）可以在带或不带调试器的情况下运行，也可以在发布版本或调试版本配置上运行   。 “应用程序时间线”等“性能探查器”工具可以在发布版本或调试版本上运行   。 调试器集成工具（如“诊断工具窗口”和“事件”选项卡）仅在调试会话期间运行   。

>[!NOTE]
>可以在 Windows 7 及更高版本中使用非调试器性能工具。 运行调试器集成分析工具需要 Windows 8 或更高版本。

非调试器“性能探查器”和调试器集成“诊断工具”提供不同的信息和体验   。 调试器集成工具显示断点和变量值。 非调试器工具提供更接近最终用户体验的结果。

帮助确定要使用的工具和结果，请考虑以下几点：

- 外部性能问题（如文件 I/O 或网络响应能力问题）在调试器或非调试器工具中看起来并没有太大差异。
- 对于 CPU 密集型调用引起的问题，发布版本和调试版本之间可能存在相当大的性能差异。 检查发布版本中是否存在该问题。
- 如果仅在调试版本期间出现此问题，则可能不需要运行非调试器工具。 对于发布版本问题，请确定调试器工具是否有助于进一步调查。
- 发布版本提供的优化包括：内联函数调用和常量、修剪未使用的代码路径及以调试器无法使用的方式存储变量。 调试器集成工具中的性能数字不太准确，因为调试版本缺乏这些优化。
- 调试器本身会更改性能时间，因为它会执行截获异常和模块加载事件等必要的调试操作。
- “性能探查器”工具中的发布版本性能数字是最精准的  。 调试器集成的工具结果对于与其他调试相关的度量值进行比较非常有用。

## <a name="collect-profiling-data-while-debugging"></a><a name="BKMK_Quick_start__Collect_diagnostic_data"></a> 在调试期间收集分析数据

通过选择“调试” > “开始调试”或按 F5 在 Visual Studio 中开始调试时，默认情况下会出现“诊断工具”窗口     。 要手动打开该窗口，请选择“调试” > “Windows” > “显示诊断工具”    。 “诊断工具”窗口显示有关事件、进程内存和 CPU 使用情况的信息  。

![诊断工具](../profiling/media/diagnostictools-update1.png "诊断工具")

- 使用工具栏中的“设置”图标以选择是否要查看“内存使用情况”、“UI 分析”以及“CPU 使用情况”     。

- 在“设置”下拉列表中选择“设置”，打开“诊断工具属性页”，其中包含更多选项    。

- 如果运行的是 Visual Studio Enterprise，则可以在 Visual Studio“工具” > “选项” > “IntelliTrace”下启用或禁用 IntelliTrace    。

当停止调试时，诊断会话结束。

此外，还可查看“诊断工具”以获取远程调试目标  。 对于远程调试和分析，必须在远程目标上安装并运行 Visual Studio 远程调试程序。
- 有关远程调试和分析桌面应用程序项目的信息，请参阅[远程调试](../debugger/remote-debugging.md)。
- 有关远程调试和分析 UWP 应用的信息，请参阅[在远程计算机上调试 UWP 应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)。

### <a name="the-events-tab"></a>“事件”选项卡

在调试会话期间，“诊断工具”窗口的“事件”选项卡列出了所发生的诊断事件   。 类别前缀：“断点”、“文件”及其他，可以快速扫描列表以查找类别或跳过不关心的类别   。

使用“筛选器”下拉列表以通过选择或取消选择择特定事件类别来筛选视图内外的事件。 

![诊断事件筛选器](../profiling/media/diagnosticeventfilter.png "诊断事件筛选器")

使用搜索框在事件列表中查找特定字符串。 以下是搜索匹配四个事件的字符串“name”的结果：

![诊断事件搜索](../profiling/media/diagnosticseventsearch.png "诊断事件搜索")

有关详细信息，请参阅 [搜索和筛选“诊断工具”窗口中的“事件”选项卡](https://devblogs.microsoft.com/devops/searching-and-filtering-the-events-tab-of-the-diagnostic-tools-window/)。

## <a name="collect-profiling-data-without-debugging"></a>在不进行调试的情况下收集分析数据

要在不进行调试的情况下收集性能数据，可以运行“性能探查器”工具  。 某些分析工具需要管理员权限才能运行。 启动诊断会话时，你可以以管理员身份打开 Visual Studio，也可以以管理员身份运行工具。

1. 在 Visual Studio 中打开项目后，选择“调试” > “性能探查器”，或按 Alt+F2     。

1. 在诊断启动页面上，选择一个或多个要运行的工具。 将仅显示适用于项目类型、操作系统和编程语言的工具。 选择“显示所有工具”也可查看此诊断会话禁用的工具  。 对于 C# UWP 应用，选项设置如下：

   ![选择诊断工具](../profiling/media/diag_selecttool.png "DIAG_SelectTool")

1. 要启动诊断会话，请选择“开始”  。

   会话运行时，一些工具会在诊断工具页面上显示实时数据图。

    ![在“性能和诊断中心”上收集数据](../profiling/media/pdhub_collectdata.png "中心收集数据")

1. 要结束诊断会话，请选择“停止收集”  。

   分析的数据显示在“报表”页上  。

可以保存报表，并从诊断工具启动页面上的“最近打开的会话”列表中将其打开  。

![打开保存的诊断会话文件](../profiling/media/pdhub_openexistingdiagsession.png "PDHUB_OpenExistingDiagSession")

### <a name="the-profiling-report"></a>分析报告
 ![诊断工具报告](../profiling/media/diag_report.png "DIAG_Report")

|||
|-|-|
|![步骤 1](../profiling/media/procguid_1.png "ProcGuid_1")|时间线显示分析会话的长度、应用程序生命周期激活事件以及用户标记。|
|![步骤 2](../profiling/media/procguid_2.png "ProcGuid_2")|你可以通过拖动蓝色条选择时间线的一个区域，将报告限制到这一部分时间线内。|
|![步骤 3](../profiling/media/procguid_3.png "ProcGuid_3")|每个诊断工具显示一个或多个主图。 如果诊断会话有多个工具，则将显示其所有主图。|
|![步骤 4](../profiling/media/procguid_4.png "ProcGuid_4")|可以折叠和展开每个工具的各个图形。|
|![步骤 5](../profiling/media/procguid_6.png "ProcGuid_6")|数据包含多个工具时，工具详细信息将在选项卡下收集。|
|![步骤 6](../profiling/media/procguid_6a.png "ProcGuid_6a")|报表的下半部分显示了每个工具的一个或多个详细信息视图。 可以通过选择时间线的区域来筛选视图。|

## <a name="run-diagnostic-sessions-on-installed-or-running-apps"></a>在已安装或正在运行的应用上运行诊断会话

 除了从 Visual Studio 项目启动应用以外，还可以在备用目标上运行诊断会话。 例如，你可能需要诊断有关从 Windows 应用商店安装的应用的性能问题。

 ![选择诊断工具分析目标](../profiling/media/pdhub_chooseanalysistarget.png "PDHUB_ChooseAnalysisTarget")

 可以启动已安装的应用，也可以将诊断工具附加到已在运行的应用和进程。 选择“正在运行的应用”或“已安装的应用”时，可以从发现指定部署目标上的应用的列表中选择应用   。 此目标可以是本地或远程计算机。

 ![选择要诊断的正在运行或已安装的应用](../profiling/media/pdhub_selectrunningapp.png "PDHUB_SelectRunningApp")

## <a name="see-also"></a>请参阅

以下是诊断开发团队的博客文章和 MSDN 文章：
- [MSDN 杂志：在 Visual Studio 2015 中进行调试的同时分析性能](https://msdn.microsoft.com/magazine/dn973013.aspx)

- [MSDN 杂志：使用 IntelliTrace 更快地诊断问题](https://msdn.microsoft.com/magazine/dn973014.aspx)

- [博客文章：使用 Visual Studio 2015 中的内存使用率工具诊断事件处理程序漏洞](https://devblogs.microsoft.com/devops/diagnosing-event-handler-leaks-with-the-memory-usage-tool-in-visual-studio-2015/)

- [视频：使用 Microsoft Visual Studio Ultimate 2015 中的 IntelliTrace 进行历史记录调试](https://channel9.msdn.com/Events/Ignite/2015/BRK3716)

- [视频：使用 Visual Studio 2015 调试性能问题](https://channel9.msdn.com/Events/Build/2015/3-731)

- [性能提示：使用 Visual Studio 调试时快速查看性能信息](https://devblogs.microsoft.com/devops/perftips-performance-information-at-a-glance-while-debugging-with-visual-studio/)

- [Visual Studio 2015 中的“诊断工具”调试器窗口](https://devblogs.microsoft.com/devops/diagnostic-tools-debugger-window-in-visual-studio-2015/)

- [Visual Studio Enterprise 2015 中的 IntelliTrace](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-ultimate-2015/)
