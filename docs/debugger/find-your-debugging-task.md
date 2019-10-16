---
title: 查找调试任务
description: 确定可帮助你调试应用的调试器功能
ms.custom: ''
ms.date: 10/01/2019
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], find your feature
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a4667fc630d86691d95e9dc9cd205b29f7b0f525
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72349709"
---
# <a name="find-your-debugging-task-in-visual-studio"></a>在 Visual Studio 中查找调试任务

如果需要帮助将调试任务映射到相关的 Visual Studio 调试器的正确功能，请使用本文中提供的链接。 此处的任务列表包括常见任务，如暂停代码调试、检查变量以及将消息发送到 "**输出**" 窗口。 如果需要调试器功能的概述，请参阅[首先查看调试器](debugger-feature-tour.md)。

## <a name="pause-running-code"></a>暂停正在运行的代码

### <a name="pause-running-code-to-inspect-a-line-of-code-that-may-contain-a-bug"></a>暂停运行代码以检查可能包含 bug 的代码行

设置断点。 有关详细信息，请参阅[使用断点](using-breakpoints.md)。

### <a name="pause-and-inspect-your-app-when-it-reaches-a-specific-state"></a>当应用达到特定状态时暂停并检查应用

尝试通过使用条件逻辑来控制断点的激活位置和时间。 有关详细信息，请参阅[断点条件](using-breakpoints.md#breakpoint-conditions)。

### <a name="pause-code-only-when-a-specific-objects-property-or-value-changes"></a>仅当特定对象的属性或值更改时暂停代码

对于C++，请设置[数据断点](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus)。 
::: moniker range=">= vs-2019"
对于使用 .NET Core 3 的应用，还可以设置[数据断点](using-breakpoints.md#BKMK_set_a_data_breakpoint_managed)。
::: moniker-end

否则，仅C#对于F#和，你可以[使用条件断点跟踪对象 ID](using-breakpoints.md#using-object-ids-in-breakpoint-conditions-c-and-f)。

### <a name="pause-code-inside-a-loop-at-a-certain-iteration"></a>在某个迭代内暂停循环内的代码

将 "**命中次数**" 设置为 "条件"。 有关详细信息，请参阅[命中次数](using-breakpoints.md#hit-count)。

### <a name="pause-code-at-the-start-of-a-function-when-you-know-the-function-name-but-not-its-location"></a>知道函数名称而不是其位置时，在函数开头暂停代码

您可以使用函数断点执行此操作。 有关详细信息，请参阅[设置函数断点](using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)。

### <a name="manage-and-keep-track-of-your-breakpoints"></a>管理和跟踪断点

使用 "**断点**" 窗口。 有关详细信息，请参阅[管理断点](using-breakpoints.md#BKMK_Specify_advanced_properties_of_a_breakpoint_)。

### <a name="pause-code-and-debug-when-a-specific-handled-or-unhandled-exception-is-thrown"></a>引发特定的处理或未处理的异常时暂停代码和调试

尽管异常帮助程序向你显示错误发生的位置，但如果你想要暂停和调试特定的错误，则可以[通知调试器在引发异常时中断](managing-exceptions-with-the-debugger.md#tell-the-debugger-to-break-when-an-exception-is-thrown)。

### <a name="set-a-breakpoint-from-the-call-stack"></a>从调用堆栈设置断点

如果要在检查执行流或在**调用堆栈**窗口中查看函数时暂停和调试代码，请参阅在["调用堆栈" 窗口中设置断点](using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)。

### <a name="pause-code-at-a-specific-assembly-instruction"></a>在特定程序集指令处暂停代码

可以通过[在 "反汇编" 窗口中设置断点](using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)来实现此目的。

## <a name="execute-code"></a>执行代码

### <a name="learn-the-commands-to-step-through-your-code-while-debugging"></a>了解在调试时逐句通过代码的命令

有关详细信息，请参阅[在调试器中导航代码](navigating-through-code-with-the-debugger.md)。

## <a name="inspect-data"></a>检查数据

### <a name="check-the-value-of-variables-while-running-your-app"></a>在运行应用程序时检查变量的值

使用[数据提示](view-data-values-in-data-tips-in-the-code-editor.md)将鼠标悬停在变量上[，或在 "自动" 和 "局部变量" 窗口中检查变量](autos-and-locals-windows.md)。

### <a name="observe-the-changing-value-of-a-specific-variable"></a>观察特定变量的变化值

对变量设置 watch。 有关详细信息，请参阅[设置监视变量](watch-and-quickwatch-windows.md)。

### <a name="view-strings-that-are-too-long-for-the-debugger-window"></a>查看对于调试器窗口过长的字符串

调试时打开内置的[字符串可视化工具](view-strings-visualizer.md)。

## <a name="configure-debugging"></a>配置调试

### <a name="customize-information-shown-in-the-debugger"></a>自定义调试器中显示的信息

您可能想要在不同的调试器窗口中显示对象类型以外的信息。 对于C#、Visual Basic、 F#和C++/cli 代码，请使用[DebuggerDisplay](using-the-debuggerdisplay-attribute.md)属性。 对于更高级的选项，还可以通过创建[自定义可视化工具](create-custom-visualizers-of-data.md)来自定义 UI。

对于 native C++，请使用[NatVis 框架](create-custom-views-of-native-objects.md)。

### <a name="configure-debugger-settings"></a>配置调试器设置

若要配置调试器选项和调试器项目设置，请参阅[调试器设置和准备](debugger-settings-and-preparation.md)。

## <a name="additional-tasks"></a>其他任务

### <a name="edit-code-during-a-debugging-session"></a>在调试会话期间编辑代码

使用 "[编辑并继续](edit-and-continue.md)"。 对于 XAML，请使用[Xaml 热重载](xaml-hot-reload.md)。

### <a name="send-messages-to-the-output-window-without-modifying-code"></a>将消息发送到 "输出" 窗口而不修改代码

设置跟踪点。 有关详细信息，请参阅[使用跟踪点](using-tracepoints.md)。

### <a name="debug-on-remote-machines"></a>在远程计算机上调试

请参阅[远程调试](remote-debugging.md)。

### <a name="debug-an-app-that-is-already-running"></a>调试已经在运行的应用

请参阅[附加到正在运行的进程](attach-to-running-processes-with-the-visual-studio-debugger.md)。

### <a name="debug-multithreaded-applications"></a>调试多线程应用程序

请参阅[调试多线程应用程序](debug-multithreaded-applications-in-visual-studio.md)。