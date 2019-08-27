---
title: 在 Visual Studio 中诊断扩展 UI 延迟 |Microsoft Docs
ms.date: 01/26/2018
ms.topic: conceptual
author: PooyaZv
ms.author: pozandev
manager: jillfra
ms.workload: multiple
ms.openlocfilehash: 00266fd8fbc881707652247e08b093ca4b15a88d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911984"
---
# <a name="how-to-diagnose-ui-delays-caused-by-extensions"></a>如何：诊断由扩展引起的 UI 延迟

当 UI 无响应时，Visual Studio 将检查 UI 线程的调用堆栈开头叶和构建基础映像使用。 如果 Visual Studio 确定调用堆栈帧所属是已安装和启用扩展的一部分的模块，它将显示一条通知。

![UI 延迟 （无响应） 通知](media/ui-delay-notification-in-vs.png)

此通知告诉用户 UI 延迟 （即，在 UI 中无响应） 可能已从扩展的代码的结果。 它还提供选项来禁用扩展或以后的通知，该扩展的用户。

本文档介绍如何诊断在扩展代码中什么原因导致 UI 延迟通知。

> [!NOTE]
> 不使用 Visual Studio 实验实例来诊断 UI 延迟。 使用实验实例中，这意味着可能不会显示 UI 延迟通知时，调用堆栈分析所需的 UI 延迟通知中的某些部分将关闭。

诊断过程的概述如下所示：
1. 确定触发器方案。
2. 使用活动日志记录重启 VS。
3. 开始 ETW 跟踪。
4. 触发该通知再次出现。
5. 停止 ETW 跟踪。
6. 检查活动日志，以获取延迟 id。
7. 分析 ETW 跟踪使用延迟步骤 6 中的 ID。

在以下部分中，我们会完成这些步骤的更多详细信息。

## <a name="identify-the-trigger-scenario"></a>确定触发器方案

若要执行诊断 UI 延迟，首先需要确定哪些 （序列的操作） 将导致 Visual Studio 以显示通知。 这是为您到能够更高版本启用日志记录的触发该通知的顺序。

## <a name="restart-vs-with-activity-logging-on"></a>使用活动日志记录重启 VS

Visual Studio 可以生成"活动日志"时调试问题提供有帮助的信息。 若要打开 Visual Studio 中的日志记录的活动，请打开 Visual Studio 中使用`/log`命令行选项。 Visual Studio 启动后，活动日志存储在以下位置：

```DOS
%APPDATA%\Microsoft\VisualStudio\<vs_instance_id>\ActivityLog.xml
```

若要了解更多有关如何查找您 VS 实例 ID，请参阅[工具用于检测和管理 Visual Studio 实例](../install/tools-for-managing-visual-studio-instances.md)。 我们将更高版本使用此活动日志以了解有关用户界面的延迟和相关的通知的详细信息。

## <a name="starting-etw-tracing"></a>启动 ETW 跟踪

可以使用[PerfView](https://github.com/Microsoft/perfview/)收集 ETW 跟踪。 PerfView 提供了一个易于使用的界面，用于收集 ETW 跟踪并分析它。 使用以下命令来收集跟踪：

```DOS
Perfview.exe collect C:\trace.etl /BufferSizeMB=1024 -CircularMB:2048 -Merge:true -Providers:*Microsoft-VisualStudio:@StacksEnabled=true -NoV2Rundown /kernelEvents=default+FileIOInit+ContextSwitch+Dispatcher
```

这样，是 Visual Studio 将使用与 UI 延迟通知相关的事件的提供程序的"Microsoft visual Studio"提供程序。 它还可以使用 PerfView 来生成内核提供程序指定关键字**线程时堆栈**视图。

## <a name="trigger-the-notification-to-appear-again"></a>触发该通知再次出现

跟踪集合启动 PerfView 后，可以使用触发器操作的顺序 （从步骤 1） 的通知再次出现。 通知显示后，可以停止跟踪 PerfView 处理并生成输出跟踪文件的集合。

## <a name="stop-etw-tracing"></a>停止 ETW 跟踪

若要停止跟踪集合，只需使用**停止收集**PerfView 窗口上的按钮。 停止跟踪集合后，PerfView 将自动处理 ETW 事件，并生成输出跟踪文件。

## <a name="examine-the-activity-log-to-get-the-delay-id"></a>检查活动日志，以获取延迟 ID

前面曾提到，可以找到在活动日志 *%APPDATA%\Microsoft\VisualStudio\<vs_instance_id > \ActivityLog.xml*。 每次 Visual Studio 检测到的扩展 UI 延迟，它将节点写入到活动日志`UIDelayNotifications`作为源。 此节点包含四个部分的 UI 延迟有关的信息：

- UI 延迟 ID，一个顺序号与会话中唯一标识 UI 延迟
- 从开始到关闭唯一标识你的 Visual Studio 会话的会话 ID
- 通知是否显示为 UI 延迟
- 该扩展可能导致 UI 延迟

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
> 并非所有的 UI 延迟导致发出通知。 因此，应始终检查**所示的通知？** 值以正确地标识正确的 UI 延迟。

在活动日志中找到正确的 UI 延迟后，记下的节点中指定的 UI 延迟 ID。 将使用此 ID 来查找下一步中相应的 ETW 事件。

## <a name="analyze-the-etw-trace"></a>分析 ETW 跟踪

接下来，打开跟踪文件。 您可以执行此操作使用 PerfView 的或通过启动新实例并设置当前的文件夹路径中左上方的窗口中的跟踪文件位置的相同实例。

![在 Perfview 中设置的文件夹路径](media/perfview-set-path.png)

然后，在左窗格中选择的跟踪文件并打开它，请选择**打开**右键菜单或上下文菜单。

> [!NOTE]
> 默认情况下 PerfView 输出 Zip 存档。 当打开*trace.zip*，它会自动解压缩存档，并打开跟踪。 您可以通过取消选中跳过此**Zip**跟踪回收期间的框。 但是，如果您计划传输，并在不同计算机之间使用跟踪，我们强烈建议不要取消选中**Zip**框。 如果不使用此选项，Ngen 程序集的所需的 Pdb 将不带跟踪并因此从 Ngen 程序集的符号将解析目标计算机上。 (请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/creating-ngen-pdbs-for-profiling-reports/)的 Pdb Ngen 的程序集的详细信息。)

可能需要几分钟时间 PerfView 来处理和打开的跟踪。 打开跟踪后，在其下出现的各种"视图"列表。

![PerfView 跟踪摘要视图](media/perfview-summary-view-events-selected.png)

首先，我们将使用**事件**视图以获取 UI 延迟时间范围：

1. 打开**事件**视图中的选择`Events`节点下跟踪，然后选择**打开**右键菜单或上下文菜单。
2. 选择"`Microsoft-VisualStudio/ExtensionUIUnresponsiveness`"的左窗格中。
3. 按 Enter

应用所选内容和全部`ExtensionUIUnresponsiveness`事件显示在右窗格中。

![在事件视图中选择事件](media/perfview-event-selection.png)

在右窗格中的每一行对应于 UI 延迟。 事件都包含一个"延迟 ID"值，该值应与步骤 6 中的活动日志中的延迟 ID 相匹配。 由于`ExtensionUIUnresponsiveness`触发末尾的 UI 延迟，该事件的时间戳 （大致） 标记的 UI 延迟的结束时间。 该事件还包含延迟的持续时间。 我们可以从用于 UI 延迟启动时获取的时间戳的最终时间戳的持续时间中减去。

![计算 UI 延迟时间范围](media/ui-delay-time-range.png)

例如，在上面的屏幕截图中事件的时间戳是 12,125.679 和延迟持续时间是 6,143.085 （毫秒）。 因此，
* 延迟开始是 12,125.679 6,143.085 = 5,982.594。
* UI 延迟时间范围为 5,982.594 到 12,125.679。

时间范围后，我们可以关闭共**事件**查看和打开**线程的时间 （与 StartStop 活动） 堆栈**视图。 此视图是尤为方便，因为通常会阻止 UI 线程的扩展插件只等待其他线程或 I/O 绑定的操作。 因此， **CPU 堆栈**视图中，这是在大多数情况下的转到选项，可能不会捕获线程所用阻塞，因为它不在此期间使用 CPU 的时间。 **线程时堆栈**按正确显示阻止时间可解决此问题。

![PerfView 摘要视图中的线程 （与 StartStop 活动） 时堆栈节点](media/perfview-thread-time-with-startstop-activities-stacks.png)

在打开时**线程时堆栈**视图中，选择**devenv**过程以启动分析。

![线程 UI 延迟分析时间堆栈的视图](media/ui-delay-thread-time-stacks.png)

在中**线程时堆栈**视图中，在页面左上方，您可以设置时间范围为计算得出的值中的上一步和按**Enter**使堆栈调整为该时间范围。

> [!NOTE]
> 确定哪个线程 UI （启动） 线程可跟踪集合已启动后 Visual Studio 已打开的情况下不够直观。 但是，UI （启动） 线程的堆栈上的第一个元素是最有可能始终操作系统 Dll (*ntdll.dll*并*kernel32.dll*) 后跟`devenv!?`，然后`msenv!?`. 此序列有助于识别 UI 线程。

 ![标识启动线程](media/ui-delay-startup-thread.png)

通过仅，其中包括包含包中的模块的堆栈，可以还可以进一步筛选此视图。

* 设置**GroupPats**为空文本，以便删除默认情况下添加任何分组。
* 设置**IncPats**包含你除了现有的进程筛选器的程序集名称的部分。 在这种情况下，它应为**devenv;UIDelayR2**。

![在线程时间堆栈视图中设置 GroupPath 和 IncPath](media/perfview-tts-group-path-inc-path.png)

PerfView 提供详细指导下的**帮助**菜单可用于确定在代码中的性能瓶颈。 此外，以下链接提供有关如何使用线程处理 Api，以优化您的代码的 Visual Studio 的详细信息：

* [https://aka.ms/vsthreading](https://aka.ms/vsthreading)
* [https://aka.ms/vsthreadingcookbook](https://aka.ms/vsthreadingcookbook)

此外可以使用新的 Visual Studio 静态分析器扩展 (NuGet 包[此处](https://www.nuget.org/packages/microsoft.visualstudio.sdk.analyzers))，这样为编写高效扩展的最佳实践提供指导。 查看一系列[VS SDK 分析器](https://github.com/Microsoft/VSSDK-Analyzers/blob/master/doc/index.md)并[线程处理分析器](https://github.com/Microsoft/vs-threading/blob/master/doc/analyzers/index.md)。

> [!NOTE]
> 如果无法解决由于存在依赖关系无响应您不能控制通过 （例如，如果您的扩展插件必须在 UI 线程上调用同步与服务），我们想要了解它。 如果你是我们的 Visual Studio 合作伙伴计划的成员，可以通过将开发人员支持请求提交请联系我们。 否则，使用报告问题工具来提交反馈，并包括`"Extension UI Delay Notifications"`标题中。 请还包括您的分析的详细的说明。
