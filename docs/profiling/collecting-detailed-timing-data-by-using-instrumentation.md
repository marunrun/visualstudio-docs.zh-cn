---
title: 使用检测收集详细计时数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,instrumentation method
- instrumentation profiling method
ms.assetid: e9deb370-c459-45ac-84d3-14d646590d05
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: bfd22edc9bd672a8d82c94a705b523ce7d836169
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779618"
---
# <a name="collect-detailed-timing-data-by-using-instrumentation"></a>通过检测收集详细计时数据
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具检测方法将分析代码注入到模块的副本中。 该代码记录分析运行期间模块中函数的每次进入、退出和函数调用。 在收集有关你的代码的某一部分的详细计时信息，以及了解输入和输出操作对应用程序性能的影响时，该检测方法会十分有用。

 你可以使用以下步骤之一来指定检测方法：

- 在分析向导的第一页，选择“检测”  。

- 在“性能资源管理器”  工具栏的“方法”  列表中，单击“检测”  。

- 在性能会话的属性对话框的“常规”  页上，选择“检测”  。

## <a name="common-tasks"></a>常见任务
 可以指定 _性能会话_  对话框中的附加选项。 若要打开此对话框：

- 在“性能资源管理器”  中，右键单击性能会话名称，然后单击“属性”  。

  下表中的任务描述了在使用检测方法进行分析时，你可以在 _性能会话_  对话框中指定的选项。

|任务|相关内容|
|----------|---------------------|
|在“常规”  页上，添加 .NET 内存分配和生存时间数据，并为生成的分析数据 (.vsp) 文件指定命名详细信息。|-   [收集 .NET 内存分配和生存期数据](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />-   [如何：设置性能数据文件名选项](../profiling/how-to-set-performance-data-file-name-options.md)|
|在“启动”  页上，如果解决方案中具有多个 .exe 项目，指定要启动的应用程序及其启动顺序。|-   [如何：指定要启动的二进制文件](../profiling/how-to-specify-the-binary-to-start.md)|
|在“二进制文件”  页上，为检测的模块副本指定位置。 默认情况下，原始二进制文件会被移动到备份文件夹中。|-   [如何：重新指定检测后的二进制文件的位置](../profiling/how-to-relocate-instrumented-binaries.md)|
|在“层交互”  页上，将 ADO.NET 调用数据添加到分析运行中。|-   [收集层交互数据](../profiling/collecting-tier-interaction-data.md)|
|在“检测”  页上，从分析中排除小函数以减少分析开销，在 ASP.NET Web 页中分析 JavaScript 代码，并指定要在检测过程之前和之后在命令提示符处运行的命令。|-   [如何：在检测中排除或添加短函数](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)<br />-   [如何：分析网页中的 JavaScript 代码](../profiling/how-to-profile-javascript-code-in-web-pages.md)<br />-   [如何：指定检测前和检测后命令](../profiling/how-to-specify-pre-and-post-instrument-commands.md)|
|在“CPU 计数器”  页上，指定要添加到分析数据的一个或多个处理器性能计数器。|-   [如何：收集 CPU 计数器数据](../profiling/how-to-collect-cpu-counter-data.md)|
|在“Windows 事件”  页上，选择一个或多个与采样数据一同收集的“Windows 事件跟踪 (ETW)”事件。|-   [如何：收集 Windows 事件跟踪 (ETW) 数据](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)|
|在“Windows 计数器”  页上，指定要作为标记添加到分析数据的一个或多个操作系统性能计数器。|-   [如何：收集 Windows 计数器数据](../profiling/how-to-collect-windows-counter-data.md)|
|在“高级”  页上，指定你想要传递给 VSInstr 检测程序的任何其他选项，例如，用于包含或排除特定函数的选项。|-   [如何：指定其他检测选项](../profiling/how-to-specify-additional-instrumentation-options.md)<br />-   [如何：将检测限定为特定函数](../profiling/how-to-limit-instrumentation-to-specific-functions.md)<br />-   [VSInstr](../profiling/vsinstr.md)|
