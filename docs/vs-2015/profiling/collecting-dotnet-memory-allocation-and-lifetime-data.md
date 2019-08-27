---
title: 收集 .NET 内存分配数据和生存期数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- .NET memory profiling method
- Profiling Tools,.NET memory method
ms.assetid: 62a6dd5f-db66-4456-9d57-f8913dbfe4d5
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 68decc73e14f8748d8434e05e50d6d3b48612d40
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436772"
---
# <a name="collecting-net-memory-allocation-and-lifetime-data"></a>收集 .NET 内存分配数据和生存期数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具支持收集 .NET 内存分配和对象生存期数据，此数据有助于检测应用程序中与内存相关的性能问题。  
  
- 有关 .NET 内存分配的数据包括所分配的 .NET Framework 内存对象的大小和数量。  
  
- 对象生存期数据包括三代垃圾回收所回收的 .NET Framework 内存对象大小的和数目。  
  
  **要求**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 Windows 应用商店应用程序也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。  
  
 可通过使用采样或检测分析方法收集数据。  
  
- 使用采样方法时，探查器将跟踪由已启动或已附加到的进程生成的所有 .NET 内存分配和对象。  
  
- 使用检测方法时，探测器将仅跟踪由检测模块生成的 .NET 内存分配和对象。  
  
> [!IMPORTANT]
> 如果正在使用采样方法收集 .NET 内存数据（分配和/或对象生存期），将忽略所有用户指定的采样事件，并使用相应的内存分配事件收集数据。  
  
 如果启用了对 .NET 内存分配的分析，同时也将启用“分配”视图。 如果启用了对 .NET 生存期数据的分析，同时也将启用“对象生存期”视图。 有关详细信息，请参阅[“分配”视图](../profiling/dotnet-memory-allocations-view.md)和[“对象生存期”视图](../profiling/object-lifetime-view.md)。  
  
 有关如何使用分析工具命令行工具收集 .NET 内存数据的信息，请参阅[使用命令行中的分析方法](../profiling/using-profiling-methods-to-collect-performance-data-from-the-command-line.md)中的“使用 .NET 内存方法收集内存分配数据和对象生存期数据”。  
  
### <a name="to-collect-net-memory-data"></a>收集 .NET 内存数据  
  
1. 在“性能资源管理器”  中，右键单击性能会话，然后单击“属性”  。  
  
2. 在“性能会话属性页”   对话框上，单击“常规”  选项卡，并选中“收集 .NET 对象分配信息”  复选框。  
  
3. 若要收集 .NET 对象生存期数据，请选择“同时收集 .NET 对象生存期信息”  复选框。  
  
## <a name="common-tasks"></a>常规任务  
 可以指定 _性能会话_  对话框中的附加选项。 若要打开此对话框：  
  
- 在“性能资源管理器”  中，右键单击性能会话名称，然后单击“属性”  。  
  
  下表中的任务说明了在收集 .NET 内存数据时，可以在“性能会话属性页”   对话框中指定的选项。  
  
|任务|相关内容|  
|----------|---------------------|  
|在“常规”  页上，为生成的分析数据 (.vsp) 文件指定命名详细信息。|-   [收集 .NET 内存分配数据和生存期数据](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />-   [如何：设置性能数据文件名选项](../profiling/how-to-set-performance-data-file-name-options.md)|  
|在“启动”  页上，如果代码解决方案中具有多个 .exe 项目，则选择要启动的应用程序。|-   [收集层交互数据](../profiling/collecting-tier-interaction-data.md)|  
|在“层交互”  页上，将 ADO.NET 调用数据添加到分析运行中。|-   [收集层交互数据](../profiling/collecting-tier-interaction-data.md)|  
|在“Windows 事件”  页上，指定一个或多个与采样数据一同收集的“Windows 事件跟踪 (ETW)”事件。|-   [如何：收集 Windows 事件跟踪 (ETW) 数据](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)|  
|在“Windows 计数器”  页上，指定要作为标记添加到分析数据的一个或多个操作系统性能计数器。|-   [如何：收集 Windows 计数器数据](../profiling/how-to-collect-windows-counter-data.md)|  
|如果应用程序模块使用多个版本，请在**高级**页上指定要分析的 .NET Framework 运行时的版本。 默认情况下会分析加载的第一个版本。|-   [如何：指定 .NET Framework 运行时](../profiling/how-to-specify-the-dotnet-framework-runtime.md)|  
  
## <a name="instrumentation-tasks"></a>检测任务  
 下表中的任务是特定于使用检测方法进行分析的“属性页”  对话框中的选项。  
  
|任务|相关内容|  
|----------|---------------------|  
|在“二进制文件”  页上，为检测的模块副本指定位置。 默认情况下，原始二进制文件会被移动到备份文件夹中。|-   [如何：重定位已检测的二进制文件](../profiling/how-to-relocate-instrumented-binaries.md)|  
|在“检测”  页上，从分析中排除小函数以减少分析开销，在 ASP.NET Web 页中分析 JavaScript 代码，并指定要在检测过程之前和之后在命令提示符处运行的命令。|-   [如何：在检测中排除或添加短函数](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)<br />-   [如何：分析网页中的 JavaScript 代码](../profiling/how-to-profile-javascript-code-in-web-pages.md)<br />-   [如何：指定检测前和检测后命令](../profiling/how-to-specify-pre-and-post-instrument-commands.md)|  
|在“CPU 计数器”  页上，指定要添加到分析数据的一个或多个处理器性能计数器。|-   [如何：收集 CPU 计数器数据](../profiling/how-to-collect-cpu-counter-data.md)|  
|在“高级”  页上，指定所需的任何其他 VSInstr 选项，例如用于包含或排除特定函数的选项。 有关 VSInstr 选项的详细信息，请参阅 [VSInstr](../profiling/vsinstr.md)|-   [如何：指定其他检测选项](../profiling/how-to-specify-additional-instrumentation-options.md)<br />-   [如何：将检测限定为特定函数](../profiling/how-to-limit-instrumentation-to-specific-functions.md)|  
  
## <a name="see-also"></a>请参阅  
 [配置性能会话](../profiling/configuring-performance-sessions.md)   
 [如何：选择收集方法](../profiling/how-to-choose-collection-methods.md)   
 [性能会话属性](../profiling/performance-session-properties.md)
