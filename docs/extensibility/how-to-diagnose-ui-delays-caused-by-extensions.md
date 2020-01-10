---
title: 诊断 Visual Studio 中的扩展 UI 延迟 |Microsoft Docs
ms.date: 01/26/2018
ms.topic: conceptual
author: PooyaZv
ms.author: pozandev
manager: jillfra
ms.workload: multiple
ms.openlocfilehash: e8b35a566eb0f2457d6eb8ae3a33235df2a64cd3
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75849145"
---
# <a name="how-to-diagnose-ui-delays-caused-by-extensions"></a>如何：诊断由扩展引起的 UI 延迟

当 UI 无响应时，Visual Studio 将检查 UI 线程的调用堆栈，从叶开始，到基础。 如果 Visual Studio 确定调用堆栈帧所属的模块属于已安装和已启用的扩展的一部分，则它将显示一个通知。

![UI 延迟（无响应）通知](media/ui-delay-notification-in-vs.png)

通知告知用户 UI 延迟（即 UI 中的无响应）可能是来自扩展的代码的结果。 它还为用户提供了用于禁用该扩展插件或该扩展的未来通知的选项。

本文档介绍如何诊断扩展代码中导致 UI 延迟通知的原因。

> [!NOTE]
> 不要使用 Visual Studio 实验实例来诊断 UI 延迟。 使用实验实例时，UI 延迟通知所需的调用堆栈分析的某些部分会关闭，这意味着可能不会显示 UI 延迟通知。

诊断过程概述如下：
1. 确定触发器方案。
2. 重新启动 VS with 上的活动日志记录。
3. 启动 ETW 跟踪。
4. 触发通知再次出现。
5. 停止 ETW 跟踪。
6. 检查活动日志以获取延迟 ID。
7. 使用步骤6中的延迟 ID 分析 ETW 跟踪。

在以下部分中，我们将更详细地介绍这些步骤。

## <a name="identify-the-trigger-scenario"></a>确定触发器方案

若要诊断 UI 延迟，您首先需要确定哪些（操作序列）会使 Visual Studio 显示通知。 这是为了让你能够在以后启用日志记录时触发通知。

## <a name="restart-vs-with-activity-logging-on"></a>重新启动 VS with 活动日志记录

Visual Studio 可以生成 "活动日志"，它可提供在调试问题时有用的信息。 若要在 Visual Studio 中启用活动日志记录，请打开带有 `/log` 命令行选项的 Visual Studio。 Visual Studio 启动后，活动日志存储在下列位置：

```DOS
%APPDATA%\Microsoft\VisualStudio\<vs_instance_id>\ActivityLog.xml
```

若要详细了解如何查找你的 VS 实例 ID，请参阅[用于检测和管理 Visual Studio 实例的工具](../install/tools-for-managing-visual-studio-instances.md)。 稍后我们将使用此活动日志来了解有关 UI 延迟和相关通知的详细信息。

## <a name="starting-etw-tracing"></a>开始 ETW 跟踪

您可以使用[PerfView](https://github.com/Microsoft/perfview/)来收集 ETW 跟踪。 PerfView 提供了一个易于使用的界面，用于收集 ETW 跟踪和分析 ETW 跟踪。 使用以下命令收集跟踪：

```DOS
Perfview.exe collect C:\trace.etl /BufferSizeMB=1024 -CircularMB:2048 -Merge:true -Providers:*Microsoft-VisualStudio:@StacksEnabled=true -NoV2Rundown /kernelEvents=default+FileIOInit+ContextSwitch+Dispatcher
```

这将启用 "VisualStudio" 提供程序，该提供程序是 Visual Studio 提供的用于与 UI 延迟通知相关的事件的。 它还为 PerfView 可用于生成 "**线程时间堆栈**" 视图的内核提供程序指定关键字。

## <a name="trigger-the-notification-to-appear-again"></a>触发通知再次出现

PerfView 启动跟踪集合后，您可以使用触发器操作序列（来自步骤1），通知再次出现。 显示通知后，可以停止 PerfView 的跟踪收集来处理并生成输出跟踪文件。

## <a name="stop-etw-tracing"></a>停止 ETW 跟踪

若要停止跟踪收集，只需使用 PerfView 窗口中的 "**停止收集**" 按钮。 停止跟踪收集后，PerfView 会自动处理 ETW 事件，并生成输出跟踪文件。

## <a name="examine-the-activity-log-to-get-the-delay-id"></a>检查活动日志以获取延迟 ID

如前文所述，可以在 *%APPDATA%\Microsoft\VisualStudio\<vs_instance_id > \ActivityLog.xml*中找到活动日志。 每次 Visual Studio 检测到扩展 UI 延迟时，都会将节点作为源写入到活动 `UIDelayNotifications` 日志中。 此节点包含有关 UI 延迟的四个信息片段：

- UI 延迟 ID，是在 VS 会话中唯一标识 UI 延迟的序列号
- 会话 ID，它从开始到关闭唯一标识你的 Visual Studio 会话
- UI 延迟是否显示了通知
- 可能导致 UI 延迟的扩展

```xml
<entry>
  <record>271</record>
  <time>2018/02/03 12:02:52.867</time>
  <type>Information</type>
  <source>UIDelayNotifications</source>
  <description>A UI delay (Delay ID = 0) has been detected. (Session ID=16e49d4b-26c2-4247-ad1c-488edeb185e0; Blamed extension="UIDelayR2"; Notification shown? Yes.)</description>
</entry>
```

> [!NOTE]
> 并非所有 UI 延迟都会导致通知。 因此，您应该始终检查**显示的通知？** 值，以正确地标识正确的 UI 延迟。

在活动日志中找到正确的 UI 延迟后，记下在节点中指定的 UI 延迟 ID。 在下一步中，你将使用该 ID 查找相应的 ETW 事件。

## <a name="analyze-the-etw-trace"></a>分析 ETW 跟踪

接下来，打开跟踪文件。 为此，可以使用相同的 PerfView 实例，也可以启动新的实例，并将窗口左上角的当前文件夹路径设置为跟踪文件的位置。

![在 Perfview 中设置文件夹路径](media/perfview-set-path.png)

然后，在左窗格中选择跟踪文件，并通过从右键单击或上下文菜单中选择 "**打开**" 来打开它。

> [!NOTE]
> 默认情况下，PerfView 将输出 Zip 存档。 打开*trace .zip*后，它会自动解压缩存档并打开跟踪。 您可以通过在跟踪收集过程中取消选中**Zip**框来跳过此过程。 但是，如果您打算在不同的计算机之间传输和使用跟踪，则强烈建议不要取消选中**Zip**框。 如果没有此选项，则 Ngen 程序集所需的 Pdb 不会伴随跟踪，因而 Ngen 程序集中的符号将不会在目标计算机上解析。 （请参阅[此博客文章](https://devblogs.microsoft.com/devops/creating-ngen-pdbs-for-profiling-reports/)，了解有关适用于 Ngen 的 pdb 程序集的详细信息。）

PerfView 处理并打开跟踪可能需要几分钟时间。 打开跟踪后，会在其下显示不同的 "视图" 列表。

![PerfView 跟踪摘要视图](media/perfview-summary-view-events-selected.png)

首先，我们将使用**事件**视图来获取 UI 延迟的时间范围：

1. 通过从右键单击或上下文菜单中选择 "打开"，然后选择 "**打开**"，打开 "**事件**" 视图 `Events` "节点"。
2. 在左窗格中选择 "`Microsoft-VisualStudio/ExtensionUIUnresponsiveness`"。
3. 按 Enter

将应用选择，并在右窗格中显示所有 `ExtensionUIUnresponsiveness` 事件。

![在事件视图中选择事件](media/perfview-event-selection.png)

右窗格中的每一行对应于 UI 延迟。 事件包含一个 "延迟 ID" 值，该值应与步骤6中的活动日志中的延迟 ID 匹配。 由于 `ExtensionUIUnresponsiveness` 在 UI 延迟结束时激发，事件的时间戳（大致）标记 UI 延迟的结束时间。 事件还包含延迟持续时间。 我们可以从结束时间戳中减去持续时间，以获取 UI 延迟启动时间的时间戳。

![计算 UI 延迟时间范围](media/ui-delay-time-range.png)

例如，在前面的屏幕截图中，事件的时间戳为12125.679，延迟持续时间为6143.085 （毫秒）。 因此，
* 延迟开始时间为 12125.679-6143.085 = 5982.594。
* UI 延迟时间范围为5982.594 到12125.679。

有了时间范围后，可以关闭 "**事件**" 视图，并打开 "**线程时间（with StartStop 活动）堆栈**" 视图。 此视图尤其方便，因为阻止 UI 线程的扩展通常只是等待其他线程或 i/o 绑定的操作。 因此，在大多数情况下， **CPU 堆栈**视图（对于大多数情况下为 "执行" 选项）可能无法捕获线程阻塞的时间，因为在该时间段内未使用 cpu。 **线程时间堆栈**通过正确显示阻塞时间来解决此问题。

![PerfView 摘要视图中的线程时间（with StartStop 活动）堆栈节点](media/perfview-thread-time-with-startstop-activities-stacks.png)

打开 "**线程时间堆栈**" 视图时，选择**devenv**进程开始分析。

![UI 延迟分析的线程时间堆栈视图](media/ui-delay-thread-time-stacks.png)

在页面左上角的 "**线程时间堆栈**" 视图中，可以将时间范围设置为在上一步中计算的值，然后按**enter** ，以便将堆栈调整到该时间范围。

> [!NOTE]
> 如果在 Visual Studio 已打开之后启动跟踪收集，则确定 UI （启动）线程是哪个线程可以不够直观。 但是，UI （启动）线程堆栈上的第一个元素最可能始终是操作系统 Dll （*ntdll.dll*和*kernel32.dll*），然后 `devenv!?` 然后 `msenv!?`。 此顺序可帮助识别 UI 线程。

 ![标识启动线程](media/ui-delay-startup-thread.png)

还可以通过仅包括包中包含模块的堆栈，进一步筛选此视图。

* 将**GroupPats**设置为空文本可以删除默认添加的所有分组。
* 除了现有的进程筛选器外，还可以将**IncPats**设置为包含部分程序集名称。 在这种情况下，它应为**devenv;UIDelayR2**。

![在线程时间堆栈视图中设置 GroupPath 和 IncPath](media/perfview-tts-group-path-inc-path.png)

PerfView 提供了 "**帮助**" 菜单下的详细指导，可用于标识代码中的性能瓶颈。 此外，以下链接提供了有关如何使用 Visual Studio 线程 Api 优化代码的详细信息：

* [https://github.com/Microsoft/vs-threading/blob/master/doc/index.md](https://github.com/Microsoft/vs-threading/blob/master/doc/index.md)
* [https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md](https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md)

你还可以使用新的 Visual Studio 静态分析器 for extensions （[此处](https://www.nuget.org/packages/microsoft.visualstudio.sdk.analyzers)为 NuGet 包），提供有关编写有效扩展的最佳实践的指导。 请参阅[VS SDK 分析器](https://github.com/Microsoft/VSSDK-Analyzers/blob/master/doc/index.md)和[线程分析器](https://github.com/Microsoft/vs-threading/blob/master/doc/analyzers/index.md)列表。

> [!NOTE]
> 如果无法解决无响应，因为您无法控制您的依赖项（例如，如果您的扩展插件必须在 UI 线程上调用同步 VS 服务），我们希望了解这一点。 如果你是 Visual Studio 合作伙伴计划的成员，则可以通过提交开发人员支持请求与我们联系。 否则，请使用 "报告问题" 工具提交反馈，并在标题中包含 `"Extension UI Delay Notifications"`。 还应包括分析的详细说明。
