---
title: 性能会话属性 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,properties
- property pages,Profiling Tools
- performance tools, performance session properties
ms.assetid: c3a86913-172b-488f-a31a-cea01a71b2ea
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: af214f6a29e12dcdf2fe8bd2de75e05283894922
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74290115"
---
# <a name="performance-session-properties"></a>性能会话属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过**性能会话**可以配置用于确定如何分析应用程序的设置。 它还存储为分析会话生成的报告。  
  
 **惠?**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]中， [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]中， [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  可通过运行**性能向导**或通过手动创建会话来创建**性能会话**。 **性能会话**创建之后，**性能会话**会显示在“性能资源管理器”中。  
  
  若要查看**性能会话**属性，请在“性能资源管理器”中选择会话名，右键单击它，然后选择“属性”。  
  
  性能会话具有以下属性页：  
  
## <a name="general"></a>常规  
 这些设置使您能够选择分析方法、添加 .NET 对象集合和生存期数据，以及指定默认报告位置和命名约定。  
  
 有关详细信息，请参见:  
  
 [如何：选择收集方法](../profiling/how-to-choose-collection-methods.md)  
  
 [收集 .NET 内存分配数据和生存期数据](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)  
  
 [如何：设置性能数据文件名选项](../profiling/how-to-set-performance-data-file-name-options.md)  
  
## <a name="launch"></a>启动  
 通过这些设置可以从二进制文件列表进行选择并指定二进制文件的启动顺序。  
  
 有关详细信息，请参阅[如何：指定要启动的二进制文件](../profiling/how-to-specify-the-binary-to-start.md)  
  
## <a name="sampling"></a>采样  
 通过这些设置可以选择在将采样用作分析方法时的样本事件和采样间隔。 样本事件用于按指定间隔收集分析数据。 例如，如果样本事件是时钟周期数并且采样间隔设置为 10,000,000，则会在每 1 千万个时钟周期之后收集采样数据。 提供了以下四种类型的样本事件：  
  
- 时钟周期数 - 用于占用大量 CPU 的问题  
  
- 页面错误 - 用于内存相关问题  
  
- 系统调用数 - 用于 I/O 相关问题  
  
- 性能计数器 - 用于低级别性能问题  
  
- 可以基于可用性能计数器指定其他样本事件  
  
  有关详细信息，请参阅[如何：选择采样事件](../profiling/how-to-choose-sampling-events.md)  
  
## <a name="binary"></a>二进制  
 通过这些设置可以指定是否要将检测的二进制文件重新定位到另一个位置。 例如，如果在分析 My.DLL 并且未选择重新定位检测的二进制文件，则会创建名为 My.Orig.DLL 的 My.DLL 备份副本。 随后，会通过插入探测以收集数据来修改 My.DLL。 如果决定重新定位检测的二进制文件，则原始二进制文件不会重命名，并且检测的二进制文件会复制到指定位置以供在检测过程中使用。  
  
 有关详细信息，请参阅[如何：指定要启动的二进制文件](../profiling/how-to-specify-the-binary-to-start.md)  
  
## <a name="tier-interactions"></a>层交互  
 有关详细信息，请参阅[收集层交互数据](../profiling/collecting-tier-interaction-data.md)  
  
## <a name="instrumentation"></a>检测  
 通过这些设置可以收集为 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 网页中的 JScript 代码收集性能数据，并指定要在检测过程之前或之后发生的任何**检测前**和**检测后**事件。  
  
 有关详细信息，请参见:  
  
 [如何：分析网页中的 JavaScript 代码](../profiling/how-to-profile-javascript-code-in-web-pages.md)  
  
 [如何：指定检测前和检测后命令](../profiling/how-to-specify-pre-and-post-instrument-commands.md)  
  
## <a name="cpu-counters"></a>CPU 计数器  
 通过这些设置可以在使用检测分析方法时收集有关 CPU 性能计数器的数据。 可移植性能计数器可在不考虑 CPU 设计或制造商的情况下使用。 平台事件特定于 CPU 设计和制造商。 有关芯片性能计数器的详细信息，请参阅特定处理器文档。  
  
 有关详细信息，请参阅[如何：收集 CPU 计数器数据](../profiling/how-to-collect-cpu-counter-data.md)  
  
## <a name="windows-events"></a>Windows 事件  
 在分析过程中，可以从事件跟踪提供程序收集数据。 可以使用 VSPerfReport.exe 命令行工具 `/calltrace` 选项查看数据。 有关 Windows 事件跟踪 (ETW) 的详细信息，请参阅[关于事件跟踪](https://go.microsoft.com/fwlink/?linkid=90752)。  
  
 有关详细信息，请参见:  
  
 [如何：收集 Windows 事件跟踪 (ETW) 数据](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)  
  
 [VSPerfReport](../profiling/vsperfreport.md)。  
  
## <a name="windows-counters"></a>Windows 计数器  
 通过此选项可以从 Windows 性能监视器计数器收集数据。 若要收集此数据，请选中标记为“收集 Windows 性能计数器”的复选框。 收集间隔可以在“收集间隔”框中设置。 还可以使用“计数器类别”和“实例”。 提供了一些默认 Windows 性能监视器计数器。  
  
 有关详细信息，请参阅[如何：收集 Windows 计数器数据](../profiling/how-to-collect-windows-counter-data.md)。  
  
## <a name="advanced"></a>高级  
 通过这些设置可以指定 [VSInstr](../profiling/vsinstr.md) 命令行分析工具的一个或多个选项，从而将选项添加到检测过程。 应用程序使用多个版本时，还可以指定要分析的公共运行时版本。  
  
 有关详细信息，请参见:  
  
 [如何：指定 .NET Framework 运行时](../profiling/how-to-specify-the-dotnet-framework-runtime.md)  
  
 [如何：指定其他检测选项](../profiling/how-to-specify-additional-instrumentation-options.md)  
  
## <a name="see-also"></a>请参阅  
 [概述](../profiling/overviews-performance-tools.md)   
 [配置性能会话](../profiling/configuring-performance-sessions.md)   
 [控制数据收集](../profiling/controlling-data-collection.md)
