---
title: 使用跟踪点记录信息 | Microsoft Docs
ms.date: 10/28/2019
ms.topic: conceptual
helpviewer_keywords:
- tracepoints, about tracepoints
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: fcc9f01315d3783af1a1f124785cd74fafb215bf
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73187311"
---
# <a name="log-info-to-the-output-window-using-tracepoints-in-visual-studio"></a>在 Visual Studio 中使用跟踪点将信息记录到“输出”窗口中

借助跟踪点，你可以在可配置的条件下将信息记录到“输出”窗口，而无需修改或停止运行代码。 托管语言（C#、Visual Basic、F#）和本机代码以及 JavaScript 和 Python 等语言均支持此功能。

## <a name="let39s-take-an-example"></a>我们来举例说明

下面的示例程序是一个简单的 `for` 循环，其中包含一个计数器变量，每当循环运行另一个迭代时，该变量都会增加一。

![计数器示例](../debugger/media/counterexample.png "计数器示例")

## <a name="set-tracepoints-in-source-code"></a>在源代码中设置跟踪点

可以通过在“断点设置”窗口的“操作”复选框下指定输出字符串来设置跟踪点 。

1. 要初始化跟踪点，请首先单击要设置跟踪点的行号左侧的装订线。

   ![断点初始化](../debugger/media/breakpointinitialization.png "断点初始化")

2. 将鼠标悬停在红色圆圈上，然后单击齿轮图标。
3. 这将打开“断点设置”窗口。

   ![断点窗口](../debugger/media/breakpointwindow.png "断点窗口")

4. 选择“操作”复选框。

   ![已选中“操作”框](../debugger/media/checkedactionsbox.png "已选中“操作”框")

   请注意红色圆圈变为菱形，表示已从断点切换为跟踪点。

5. 在“在输出窗口中显示消息”文本框中输入要记录的消息（有关详细信息，请参阅本文后面的相关部分）。

   现已设置跟踪点。 如果你只想将一些信息记录到输出窗口中，请点击“关闭”按钮&quot;&quot;。

6. 如果要添加确定是否显示消息的条件，请选择“条件”复选框。

   ![已选中“条件”框](../debugger/media/checkedconditionsbox.png "已选中“条件”框")

   有三个条件选项：“条件表达式”、“筛选器”和“命中次数”  。

## <a name="actions-menu"></a>“操作”菜单

使用此菜单可将消息记录到“输出”窗口。 在消息框中键入要输出的字符串（无需引号）。 如果要显示变量的值，请确保将其括在大括号中。

例如，如果要在输出控制台中显示 `counter` 变量的值，请在消息文本框中键入 {counter}。

![计数器输出消息](../debugger/media/counteroutputmessage.png "计数器输出消息")

如果单击“关闭”，然后调试程序 (F5)，你会在“输出”窗口中看到以下输出 。

![“输出”窗口中的操作消息](../debugger/media/actionsmessageinoutputwindow.png "“输出”窗口中的操作消息")

此外，还可以使用特殊关键字来显示更多特定信息。 完全按照以下所示输入关键字（在每个关键字前面使用“$”，并且关键字本身全部大写）。

| 关键字 | 显示内容 |
| --- | --- |
| $ADDRESS | 当前指令 |
| $CALLER | 调用函数名 |
| $CALLSTACK | “调用堆栈” |
| $FUNCTION | 当前函数名 |
| $PID | 进程 ID |
| $PNAME | 进程名 |
| $TID | 线程 ID |
| $TNAME   | 线程名 |
| $TICK | 滴答计数（来自 Windows GetTickCount） |

## <a name="conditions-menu"></a>“条件”菜单

使用条件可以筛选输出消息，以便仅在某些情况下显示它们。 有三种主要条件可供使用。

### <a name="conditional-expression"></a>条件表达式
对于条件表达式，仅在满足某些条件时才显示输出消息。

对于条件表达式，可以将跟踪点设置为在特定条件得到满足或发生变化时输出消息。 例如，如果只想在 `for` 循环的偶数次迭代期间显示计数器的值，可以选择“为 true”选项，然后在消息文本框中键入 `i%2 == 0`。

![条件表达式为 True](../debugger/media/conditionalexpressionistrue.png "条件表达式为 True")

如果要在 `for` 循环的迭代更改时打印计数器的值，请选择“更改时”选项，然后在消息文本框中键入 `i`。

![条件表达式更改时](../debugger/media/conditionalexpressionwhenchanged.png "条件表达式更改时")

不同编程语言中“更改时”选项的行为不同。

- 对于本机代码，调试器不会将条件的第一次计算当作一次更改，所以第一次计算时不会命中跟踪点。
- 对于托管代码，当选择了“更改时”，调试器将在之后的第一次计算时命中跟踪点。

有关在设置条件时可以使用的有效表达式的更全面的信息，请参阅[调试器中的表达式](expressions-in-the-debugger.md)。

### <a name="hit-count"></a>命中次数
使用命中次数条件，可以在设置了跟踪点的代码行执行了指定的次数之后才发送输出。

对于命中次数，可以选择在设置了跟踪点的代码行的执行次数等于、大于或等于指定命中次数值以及是该值的倍数时输出一条消息。 选择最能满足你需求的选项，然后在改字段中键入一个整数值（例如 5），表示你想要设置的迭代次数。

![条件表达式命中次数](../debugger/media/conditionalexpressionhitcount.png "条件表达式命中次数")

### <a name="filter"></a>筛选器
对于筛选条件，请指定显示哪些设备、进程或线程的输出。

![条件表达式筛选器](../debugger/media/conditionalexpressionfilter.png "条件表达式筛选器")

筛选表达式列表：

- MachineName = "name"
- ProcessId = value
- ProcessName = "name"
- ThreadId = value
- ThreadName = "name"

将字符串（例如名称）用双引号引起来。 输入值时可以不带引号。 可以使用 `&` (`AND`)、`||` (`OR`)、`!` (`NOT`) 和括号合并子句。

## <a name="considerations"></a>注意事项

虽然跟踪点旨在使调试体验更加简洁、流畅，但是在使用跟踪点时应注意一些问题。

有时，当检查对象的属性或特性时，其值可能会更改。 如果值在检查过程中发生变化，这并不是跟踪点功能本身导致的 bug。 但是，使用跟踪点检查对象并不能避免这些意外修改。

“操作”消息框的表达式计算方式可能与你当前用于开发的语言不同。 例如，要输出字符串，无需将消息用引号引起来，即使在使用 `Debug.WriteLine()` 或 `console.log()` 时通常会这样做。 此外，用于输出表达式的大括号语法 (`{ }`) 也可能与以开发语言输出值的约定不同。 （但是，大括号 (`{ }`) 中的内容仍应使用开发语言的语法来编写）。

如果尝试调试实时应用程序并查找类似的功能，请查看 Snapshot Debugger 中的记录点功能。 快照调试器是用于调查生产应用程序中问题的工具。 借助记录点，还可以将消息发送到“输出”窗口，而无需修改源代码，并且不会影响正在运行的应用程序。 有关详细信息，请参阅[调试实时 Azure 应用程序](../debugger/debug-live-azure-applications.md)。

## <a name="see-also"></a>请参阅

- [什么是调试？](../debugger/what-is-debugging.md)
- [使用 Visual Studio 编写更好的 C# 代码](../debugger/write-better-code-with-visual-studio.md)
- [初探调试](../debugger/debugger-feature-tour.md)
- [调试器中的表达式](expressions-in-the-debugger.md)
- [使用断点](../debugger/using-breakpoints.md)
- [调试实时 Azure 应用程序](../debugger/debug-live-azure-applications.md)
