---
title: 从命令行创建基本分析报告 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 6d73e21e-c04e-48ea-91cc-e517a5f2cd3f
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5f13921dea810ab2185e626cc2889f339d9d174f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62537175"
---
# <a name="creating-basic-profiling-reports-from-the-command-line"></a>从命令行创建基本分析报告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍从 .vsp 或 .vsps 分析数据文件生成逗号分隔值 (.csv) 报告的基本 VSPerfReport 命令。 有关所有报告选项的介绍，请参阅 [VSPerfReport](../profiling/vsperfreport.md)。  
  
## <a name="report-commands"></a>报表命令  
 使用以下命令之一可为指定的分析数据文件创建报告。  
  
 **VSPerfReport** `VSPFile` **/Summary:All**  
 生成所有适用于 .vsp 或 .vsps 文件的报告。  
  
 **VSPerfReport** `VSPFile` **/Summary:**`ReportType`[,`ReportType`...]  
 生成指定的报告类型。  
  
 **VSPerfReport** `VSPFile` **/CallTrace**  
 生成列出每个数据收集事件的报告。 仅限检测。  
  
## <a name="summary-report-type-parameters"></a>报告类型参数摘要  
 下表介绍了指定报告类型选项所生成的报告。 报告的列取决于用于收集数据的分析方法。  
  
|参数摘要|报告说明|报告引用|  
|-----------------------|------------------------|----------------------|  
|**CallerCallee**|表示函数间的父/子关系。|-   [采样数据](../profiling/caller-callee-view-sampling-data.md)<br />-   [检测数据](../profiling/caller-callee-view-instrumentation-data.md)<br />-   [.NET 内存采样数据](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)<br />-   [.NET 内存检测数据](../profiling/caller-callee-view-net-memory-instrumentation-data.md)<br />-   [争用数据](../profiling/caller-callee-view-contention-data.md)|  
|**Function**|按函数列出分析数据。|-   [采样数据](../profiling/functions-view-sampling-data.md)<br />-   [检测数据](../profiling/functions-view-instrumentation-data.md)<br />-   [.NET 内存采样数据](../profiling/functions-view-dotnet-memory-sampling-data.md)<br />-   [.NET 内存检测数据](../profiling/functions-view-dotnet-memory-instrumentation-data.md)<br />-   [争用数据](../profiling/functions-view-contention-data.md)|  
|**CallTree**|表示分析运行期间函数的执行路径和分析数据。|-   [检测数据](../profiling/call-tree-view-instrumentation-data.md)<br />-   [采样数据](../profiling/call-tree-view-sampling-data.md)<br />-   [.NET 内存采样数据](../profiling/call-tree-view-dotnet-memory-sampling-data.md)<br />-   [.NET 内存检测数据](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)<br />-   [争用数据](../profiling/call-tree-view-contention-data.md)|  
|**计数器**|列出分析运行期间所收集的分析标记和 Windows 性能计数器值。|-   [标记视图](../profiling/marks-view.md)|  
|**Ip**|按说明列出分析数据。|-   [采样数据](../profiling/instruction-pointers-ips-view-sampling-data.md)<br />-   [.NET 内存采样数据](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)<br />-   [争用数据](../profiling/instruction-pointers-ips-view-contention-data.md)|  
|**Life**|列出所分配对象的生存期。|-   [“对象生存期”视图](../profiling/object-lifetime-view.md)|  
|**Line**|按源代码行列出分析数据。|-   [采样数据](../profiling/lines-view-sampling-data.md)<br />-   [.NET 内存采样数据](../profiling/lines-view-dotnet-memory-sampling-data.md)<br />-   [争用数据](../profiling/lines-view-contention-data.md)|  
|**Header**|分析数据文件标头信息。|特定于文件。|  
|**标记**|分析运行期间收集的分析标记。|-   [标记视图](../profiling/marks-view.md)|  
|**模块**|列出模块的分析数据。|-   [采样数据](../profiling/modules-view-sampling-data.md)<br />-   [检测数据](../profiling/modules-view-instrumentation-data.md)<br />-   [.NET 内存采样数据](../profiling/modules-view-dotnet-memory-sampling-data.md)<br />-   [.NET 内存检测数据](../profiling/modules-view-dotnet-memory-instrumentation-data.md)<br />-   [争用数据](../profiling/modules-view-contention-data.md)|  
|**Process**|列出进程的分析数据。|-   [“进程”视图](../profiling/process-view.md)<br />-   [争用数据](../profiling/process-view-contention-data.md)|  
|**线程**|列出线程的分析数据。|-   [“进程”视图](../profiling/process-view.md)|  
|**Type**|按类型列出分配分析数据。|-   [“分配”视图](../profiling/dotnet-memory-allocations-view.md)|  
|**Contention**|资源争用。|-   [资源争用](../profiling/resource-contentions-view-contention-data.md)|  
|**RuleWarnings**|列出性能规则问题。|-   列出规则问题的 CheckId、描述和源代码位置。|  
|**ETW**|列出分析运行期间收集的 Windows 事件跟踪 (ETW) 事件。|-   [ETW 报告](../profiling/event-tracing-for-windows-etw-report.md)|
