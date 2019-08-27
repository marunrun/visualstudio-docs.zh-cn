---
title: CPU 和 Windows 计数器 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.counters
helpviewer_keywords:
- Windows counters in Profiling Tools
- CPU counters in Profiling Tools
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 37025177c026d0b6578644ca5765a6878be984ea
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62552992"
---
# <a name="cpu-and-windows-counters"></a>CPU 和 Windows 计数器

利用 Visual Studio 探查器，可以收集操作系统（Windows 计数器）生成的性能数据和处理器单元（CPU 计数器）生成的性能数据。

> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 UWP 应用也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。

## <a name="windows-counters"></a>Windows 计数器

Windows 计数器是 Windows 诊断基础结构的一部分，该结构提供关于操作系统、应用程序、服务或驱动器性能的信息。 Windows 计数器取决于当前计算机的配置，并且可能无法在其他计算机上使用。 Windows 性能计数器以分析标记的形式收集在分析数据文件中，然后可将其用于筛选视图和报表。

## <a name="cpu-counters"></a>CPU 计数器

CPU 计数器是计算机的 CPU 的一项功能，可存储硬件相关事件的计数。 使用检测分析方法收集 CPU 计数器数据时，数据将被追加到函数和模块的数据中。 可以使用检测方法收集多个 CPU 计数器。 使用采样方法时，选择一个计数器用作要被采样的事件。

性能计数器特定于 CPU。 CPU 的不同模型和版本可使用明显不同的配置设置来启用相同的性能计数器。 [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] 探查器可移植事件将某些常用的性能计数器从特定的处理器中解耦出来，并使你可以收集或采样通用的性能事件。

如果希望使用探查器时对特定事件进行计数，例如，L2 缓存未命中数，则可围绕该事件发送方生成性能会话。 可以在具有 L2 缓存的任何 CPU 上执行此操作。 性能会话可在未进行修改的情况下从平台移动到平台。

Visual Studio 探查器继续支持特定平台的特定事件。 例如，Pentium 4 平台上的开发者可能需要对特定于 NetBurst 体系结构的事件进行计数。 此事件不可移植，但开发者仍可将其用于特定平台上的特定性能会话。

## <a name="portable-and-platform-events"></a>可移植事件和平台事件

可移植事件是一组非特定于某个特定处理器的 CPU 计数器。 所有其他的 CPU 计数器称为平台事件，并且在各种平台上可能不受支持。

 可移植事件和平台事件的计数器在 .xml 文件中定义，其中提供了与计数器相关的特定值。 有多个适用于不同 CPU 的文件，因为适用于 Intel 和 AMD CPU 的数据不同。 [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] 探查器使用此信息向用户展现用于性能测量的相应的计数器（可移植和平台）。

### <a name="portable-events"></a>可移植事件

可移植事件包含以下事件：

**常规事件**

|事件名称|事件说明|
|----------------|-----------------------|
|Instructions Retired|指示事件完成之前执行的指令数。|
|Non Halted Cycles|仅指示处理器在其中未停止（如正在等待 I/O）的周期。|

**前端事件**

|事件名称|事件说明|
|----------------|-----------------------|
|ITLB Misses|指示导致未命中的指令转换旁视缓冲的数量。|

**分支事件**

|事件名称|事件说明|
|----------------|-----------------------|
|Branches Retired|指示事件完成之前已执行的分支指令数。|
|Mis-predicted Branches|指示由于处理器预测了不正确的路径发生的误报的分支。 误报的分支会影响性能，因为处理器必须放弃已完成的所有工作，然后在正确的路径上重新开始。|

**内存事件：**

|事件名称|事件说明|
|----------------|-----------------------|
|L2 Cache Read Misses|指示二级缓存读取未命中的数量。|
|L2 Cache Read References|指示二级缓存读取引用的数量。 它包括加载未命中和读取所有权 (RFO) 未命中和命中。|

## <a name="view-available-counters"></a>查看可用的计数器

可以在命令提示符窗口中列出 Visual Studio IDE 中的可用 CPU 计数器。

### <a name="visual-studio-ui"></a>Visual Studio UI

若要列出 Visual Studio IDE 中计算机上的可用计数器，必须在性能浏览器中打开探查器性能会话。

#### <a name="to-view-a-list-of-a-list-of-all-cpu-counters-that-are-supported-on-the-current-platform"></a>查看当前平台上支持的所有 CPU 计数器列表的列表

1. 在“性能资源管理器”中，右键单击性能会话，然后单击“属性”。

2. 执行下列操作之一：

   - 单击“采样”，然后从“采样”事件列表中选择“性能计数器”。 CPU 计数器列在“可用的性能计数器”中。

      **请注意**：单击“取消”可返回到上一个采样配置。

     或

   - 选择“CPU 计数器”，然后选择“收集 CPU 计数器”。 CPU 计数器列在“可用的计数器”中。

      **请注意**：单击“取消”可返回到上一个计数器收集配置。

#### <a name="to-view-a-list-of-a-list-of-window-counters-that-are-supported-on-the-current-platform"></a>查看当前平台上支持的 Windows 计数器列表的列表

1. 在“性能资源管理器”中，右键单击性能会话，然后单击“属性”。

2. 单击“Windows 计数器”。

3. 选择“收集 Windows 计数器”。

4. 从“计数器类别”列表中，选择一个计数器组。 该组的 Windows 计数器将显示在列表框中。

     **注意：** 单击“取消”可返回到上一个计数器收集配置。

### <a name="command-line"></a>命令行

通过使用 [VSPerfCmd](../profiling/vsperfcmd.md) 命令行工具，可以从命令行中列出计算机上可用的 CPU 计数器。

#### <a name="to-list-of-cpu-counters-that-are-supported-on-the-current-platform"></a>查看当前平台上支持的 CPU 计数器的列表

1. 打开命令提示符窗口。

2. 类型

     **\<Visual Studio Performance Tools Directory>\VSPerfCmd /querycounters**

     其中 *\<Visual Studio Performance Tools Directory>* 是 Visual Studio 安装的性能工具目录的路径。 若要获取性能工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。

## <a name="see-also"></a>请参阅

[概述](../profiling/overviews-performance-tools.md)
[如何：选择采样事件](../profiling/how-to-choose-sampling-events.md)
[如何：收集 CPU 计数器数据](../profiling/how-to-collect-cpu-counter-data.md)
[如何：收集 Windows 计数器数据](../profiling/how-to-collect-windows-counter-data.md)