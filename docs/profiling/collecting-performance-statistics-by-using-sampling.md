---
title: 使用采样收集性能统计信息 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,sampling
- sampling profiling method
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 97644776f4197e2f3286d29cbd3f746f7ecd0b15
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62809647"
---
# <a name="collect-performance-statistics-by-using-sampling"></a>通过采样收集性能统计信息

默认情况下，Visual Studio 分析工具采样法收集每 10,000,000 个处理器周期（近似为 1 GHz 计算机上的每百分之一秒）的分析信息。 采样方法可用于查找处理器利用率问题，也是启动最多性能调查时建议采用的方法。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

可以使用以下步骤之一来指定采样方法：

- 在分析向导的第一页，单击“CPU 采样(建议)”。
- 在“性能资源管理器”工具栏的“方法”列表中，单击“采样”。
- 在性能会话的属性对话框的“常规”页上，选择“采样”。

## <a name="common-tasks"></a>常见任务

可以指定 _性能会话_ 对话框中的附加选项。 若要打开此对话框：

- 在“性能资源管理器” 中，右键单击性能会话名称，然后单击“属性” 。

  下表中的任务描述了在使用采样方法进行分析时，可以在“性能会话属性”对话框中指定的选项。

|任务|相关内容|
|----------|---------------------|
|在“常规”页上，添加 .NET 内存分配和生存时间数据集合，并为生成的分析数据 (.vsp) 文件指定命名详细信息。|- [收集 .NET 内存分配数据和生存期数据](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />- [如何：设置性能数据文件名选项](../profiling/how-to-set-performance-data-file-name-options.md)|
|在“采样”页上，更改抽样率、将采样事件从处理器时钟周期更改为另一个处理器性能计数器，或同时进行两项更改...|- [如何：选择采样事件](../profiling/how-to-choose-sampling-events.md)|
|在“启动”页上，如果代码解决方案中具有多个 .exe 项目，请指定要启动的应用程序及其启动顺序。|- [收集层交互数据](../profiling/collecting-tier-interaction-data.md)|
|在“层交互”页上，将 ADO.NET 调用信息添加到分析运行期间收集的数据中。|- [收集层交互数据](../profiling/collecting-tier-interaction-data.md)|
|在“Windows 事件”页上，指定一个或多个与采样数据一同收集的“Windows 事件跟踪 (ETW)”事件。|- [如何：收集 Windows 事件跟踪 (ETW) 数据](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)|
|在“Windows 计数器”  页上，指定要作为标记添加到分析数据的一个或多个操作系统性能计数器。|- [如何：收集 Windows 计数器数据](../profiling/how-to-collect-windows-counter-data.md)|
|如果应用程序模块使用多个版本，请在**高级**页上指定要分析的 .NET Framework 运行时的版本。 默认情况下会分析加载的第一个版本。|- [如何：指定 .NET Framework 运行时](../profiling/how-to-specify-the-dotnet-framework-runtime.md)|