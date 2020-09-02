---
title: 分析工具 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.diagnosticshub.overview
ms.assetid: 0fb6cd5d-e16a-4526-84a5-19e63c625bc5
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bcb230532da4a0b84ea0102d86534c28afe35558
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686271"
---
# <a name="profiling-tools"></a>分析工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

分析和诊断工具有助于诊断内存和 CPU 使用率以及其他应用程序级别问题。 这些工具可用于累积一段时间内在调试器中运行应用程序的数据（例如变量值、函数调用和事件）。 可以查看代码执行期间不同点的应用程序状态。  
  
 查看底部的摘要，了解项目类型（例如，桌面、UWP、ASP.NET）可以使用的工具。  
  
 可以通过使用“调试”/“Windows”/“显示诊断工具” **** 访问分析工具以在调试会话期间使用这些工具，或通过使用“调试”/“性能探查器…” **** 执行重点性能分析。  请参阅 [Running Profiling Tools With or Without the Debugger](../profiling/running-profiling-tools-with-or-without-the-debugger.md) 了解不同方法的详细信息。  
  
 ![DebugDiagnosticsToolsMenu](../profiling/media/debugdiagnosticstoolsmenu.png "DebugDiagnosticsToolsMenu")  
  
 有关此版本中的新增功能，请参阅[分析工具中的新增功能](../profiling/what-s-new-in-profiling-tools.md)。  
  
 以下各节介绍了可以在 Visual Studio 中使用的不同性能工具。  
  
## <a name="memory-usage"></a>内存使用率  
 ![DiagMemorySmall](../profiling/media/diagmemorysmall.png "DiagMemorySmall")  
  
 使用 " **内存使用率** " 工具进行调试时查找内存泄漏和低效内存。 该工具可以拍摄托管和本机内存堆的快照。 此工具可用于桌面应用、Windows 通用应用和 ASP.NET 应用。 在调试 (**调试/窗口/显示诊断工具**) 或外部 (**调试/性能探查器 ...**) 时，可以从 "**诊断工具**" 窗口中运行 "**内存使用率**" 工具。有关详细信息，请参阅[内存使用](../profiling/memory-usage.md)情况和[内存使用情况（不调试](https://msdn.microsoft.com/library/8883bc5f-df86-4f84-aa2b-a21150f499b0)）。  
  
## <a name="cpu-usage"></a>CPU 使用率  
 ![DiagCPUSmall](../profiling/media/diagcpusmall.png "DiagCPUSmall")  
  
 **CPU 使用率** 工具可为你显示 CPU 耗用时间执行 C + +、C# / VB 和 JavaScript 代码的位置。  此工具可用于桌面应用和 Windows 通用应用以及 Azure App Services 应用。 在调试 (**调试/窗口/显示诊断工具**) 或外部 (**调试/性能探查器 ...**) 时，可以从 "**诊断工具**" 窗口运行 " **CPU 使用率**" 工具。有关详细信息，请参阅[CPU 使用率](../profiling/cpu-usage.md)。  
  
## <a name="performance-explorer"></a>性能资源管理器  
 ![PerfTools](../profiling/media/perftools.png "PerfTools")  
  
 “性能资源管理器” **** （“调试”/“探查器”/“性能资源管理器”****）允许使用各种不同的工具，例如“CPU 采样” ****、“检测”  ****、“.NET 内存分配” **** 和“资源争用” ****。 性能资源管理器工具可用于桌面应用和 ASP.NET 应用，但不可用于 Windows 通用应用。 有关更多信息，请参见 [性能资源管理器](../profiling/performance-explorer.md)。  
  
## <a name="gpu-usage"></a>GPU 使用情况  
 ![DiagGPUUsage](../profiling/media/diaggpuusage.png "DiagGPUUsage")  
  
 使用 [GPU Usage](../debugger/gpu-usage.md) 工具可以更好地理解 Direct3D 应用的高级硬件利用率。 此工具可用于桌面和 Windows 通用应用，但不可用于 ASP.NET 应用。 “GPU 使用率” **** 工具可以在调试时从“诊断工具” **** 窗口运行（“调试”/“显示诊断工具”****），也可以在调试器外部运行（“调试”/“性能探查器...”****）。  
  
## <a name="application-timeline"></a>应用程序时间线  
 ![DiagAppTimeline](../profiling/media/diagapptimeline.png "DiagAppTimeline")  
  
 [Application Timeline](../profiling/application-timeline.md) 工具提供应用程序资源使用情况的详细视图，可帮助提高 XAML 应用程序的性能。 “应用程序时间线” **** 工具可用于桌面和 Windows 通用应用，但不可用于 ASP.NET 应用。 **** “应用程序时间线”工具可以从“诊断工具” **** 窗口（“调试”/“性能探查器…”****）运行。  
  
## <a name="perftips"></a>性能提示  
 ![DiagPerfTips](../profiling/media/diagperftips.png "DiagPerfTips")  
  
 调试器在断点或单步执行操作中停止执行时，中断与上一个断点之间经过的时间会显示为在编辑器窗口中的提示。 这些 [PerfTips](../profiling/perftips.md) 有助于在调试期间监视和分析应用的性能。 可以在桌面应用、Windows 通用应用和 ASP.NET 应用中查看“性能提示” **** 。  
  
## <a name="javascript-memory"></a>JavaScript 内存  
 ![DiagJSMemory](../profiling/media/diagjsmemory.png "DiagJSMemory")  
  
 通过收集进入和退出应用中各功能的计时信息，[JavaScript 内存](../profiling/javascript-memory.md)工具可用于测量、评估和解决代码中的性能相关问题。 此工具可用于 Windows 通用 HTML 应用。 **** “JavaScript 函数计时”工具可以从“诊断工具” **** 窗口（“调试”/“性能探查器…”****）运行。  
  
## <a name="html-ui-responsiveness"></a>HTML UI 响应能力  
 ![DiagHTMLResp](../profiling/media/diaghtmlresp.png "DiagHTMLResp")  
  
 [HTML UI responsiveness](../profiling/html-ui-responsiveness.md) 工具有助于隔离应用中的性能问题，包括响应能力不足、加载时间缓慢以及视觉对象更新频率小于预期。 此工具可用于 Windows 通用 HTML 应用。 **** “HTML UI 响应能力”工具可以从“诊断工具” **** 窗口（“调试”/“性能探查器…”****）运行。  
  
## <a name="intellitrace"></a>IntelliTrace  
 ![DiagIntelliTrace](../profiling/media/diagintellitrace.png "DiagIntelliTrace")  
  
 [IntelliTrace](../debugger/intellitrace.md) 可以记录特定事件、检查调试器事件和函数调用期间“局部变量” **** 窗口中的数据以及调试难以再现的问题。  IntelliTrace 主要是一个调试工具，但它还可以提供可用于性能调查的信息。 此工具仅可在 Visual Studio Enterprise 中与桌面应用、Windows 通用应用和 C# ASP.NET 应用结合使用。 调试时可以在“诊断工具” **** 窗口找到 IntelliTrace（“调试”/“Windows”/“显示诊断工具”****）。  
  
## <a name="profiling-in-production"></a>在生产中分析  
 在生产中进行分析的推荐方法是从 [使用 vsperf.exe 的命令行](../profiling/using-the-profiling-tools-from-the-command-line.md) 分析，以收集 CPU 配置文件。 有关 Azure App Service 中的远程分析支持，请参阅 [服务器资源管理器或 Kudu 门户](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service/)。  
  
## <a name="which-tool-should-i-use"></a>应使用哪一种工具？  
 下表列出了 Visual Studio 提供的不同工具以及适用的不同项目类型：  
  
|性能工具|Windows 桌面|Windows 通用/应用商店|ASP.NET|  
|----------------------|---------------------|------------------------------|-------------|  
|[内存使用率](../profiling/memory-usage.md)|是|是|否|  
|[CPU 使用率](../profiling/cpu-usage.md)|是|是|仅限 Azure App Service|  
|[GPU 使用情况](../debugger/gpu-usage.md)|是|是|否|  
|[应用程序时间线](../profiling/application-timeline.md)|是|是|否|  
|[性能提示](../profiling/perftips.md)|是|XAML 适用，HTML 不适用|否|  
|[性能资源管理器](../profiling/performance-explorer.md)|是|否|是|  
|[IntelliTrace](../debugger/intellitrace.md)|仅限 .NET Enterprise|仅限 .NET Enterprise|仅限 .NET Enterprise|  
|[HTML UI responsiveness](../profiling/html-ui-responsiveness.md)|否|HTML 适用，XAML 不适用|否|  
|[JavaScript 内存](../profiling/javascript-memory.md)|否|HTML 适用，XAML 不适用|否|  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio IDE](../ide/visual-studio-ide.md)
