---
title: 在调试器中使用跟踪点 |Microsoft Docs
ms.date: 9/17/2019
ms.topic: conceptual
helpviewer_keywords:
- tracepoints, about tracepoints
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 7680b305fad6f8ea1d7961ec5a70ddafd578c77d
ms.sourcegitcommit: 6993bcb0d2b0067b1b7b7899bfba52c31c70b7e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2019
ms.locfileid: "71095253"
---
# <a name="use-tracepoints-in-the-visual-studio-debugger"></a>在 Visual Studio 调试器中使用跟踪点

跟踪点允许您在可配置条件下将信息记录到 "输出" 窗口中，而无需修改或停止您的代码。 托管代码和本机代码都支持此功能，同时还支持多种语言（例如 JavaScript 和C#）。

## <a name="let39s-take-an-example"></a>让&#39;我们举个例子

下面的示例程序是一个简单`for`的循环，其中包含一个计数器变量，每次循环运行另一个迭代时都会增加一个。

![计数器示例](../debugger/media/counterexample.png "计数器示例")

## <a name="set-tracepoints-in-source-code"></a>在源代码中设置跟踪点

您可以通过在 "**断点设置**" 窗口中的 "**操作**" 复选框下指定输出字符串来设置跟踪点。

1. 若要初始化跟踪点，请首先单击要设置跟踪点的行号左侧的装订线。

   ![断点初始化](../debugger/media/breakpointinitialization.png "断点初始化")

2. 将鼠标悬停在红色圆圈上，并单击齿轮图标。
3. 这将打开 "**断点设置**" 窗口。

   ![断点窗口](../debugger/media/breakpointwindow.png "断点窗口")

4. 选中 "**操作**" 复选框。

   ![选中的操作框](../debugger/media/checkedactionsbox.png "选中的操作框")

   请注意红圈如何变成菱形，指示已将断点转换为跟踪点。

5. 在 **"输出窗口**" 文本框中输入要登录的消息（有关详细信息，请参阅本文后面的部分）。

   现在已设置了跟踪点。 &quot;如果只想要做的就是将一些&quot;信息记录到输出窗口。

6. 如果要添加确定是否显示消息的条件，请选中 "**条件**" 复选框。

   ![选中条件框](../debugger/media/checkedconditionsbox.png "选中条件框")

   有三个条件选项：**条件表达式**、**筛选器**和**命中次数**。

## <a name="actions-menu"></a>操作菜单

使用此菜单可以将消息记录到 "输出" 窗口。 键入要输出到消息框中的字符串（不需要引号）。 如果要显示变量的值，请确保将其括在大括号中。

例如，如果要在输出控制台中显示变量的值`counter` ，请在 "消息" 文本框中键入 "{counter}"。

![计数器输出消息](../debugger/media/counteroutputmessage.png "计数器输出消息")

如果单击 "**关闭**"，然后调试程序（**F5**），将在 "输出" 窗口中看到以下输出。

![输出窗口中的操作消息](../debugger/media/actionsmessageinoutputwindow.png "输出窗口中的操作消息")

你还可以使用特殊关键字来显示更具体的信息。 按如下所示原样输入关键字（在每个关键字的前面使用 "$" 和关键字本身的全部大写）。

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

## <a name="conditions-menu"></a>条件菜单

条件允许你筛选输出消息，使其仅在某些情况下显示。 有三种主要的条件可供您使用。

### <a name="conditional-expression"></a>条件表达式
对于条件表达式，只在满足某些条件时才显示输出消息。

对于条件表达式，你可以将跟踪点设置为在特定条件为 true 或更改时输出消息。 例如，如果只想在`for`循环迭代期间显示计数器的值，则可以选择 "**为 true** " 选项，然后在 "消息" 文本框中`i%2 == 0`键入。

![条件表达式为 True](../debugger/media/conditionalexpressionistrue.png "条件表达式为 True")

如果要在`for`循环迭代发生更改时打印计数器的值，请选择 "**更改时**" 选项，并在 " `i`消息" 文本框中键入。

![更改时的条件表达式](../debugger/media/conditionalexpressionwhenchanged.png "更改时的条件表达式")

不同编程语言的 "**更改时**" 选项的行为不同。

- 对于本机代码，调试器不会将条件的第一次计算视为一次更改，因此不会命中第一次计算中的跟踪点。
- 对于托管代码，在选择 "**更改**后，调试器会命中第一个计算的跟踪点"。

有关设置条件时可使用的有效表达式的详细信息，请参阅[调试器中的表达式](expressions-in-the-debugger.md)

### <a name="hit-count"></a>命中计数
命中次数条件允许您仅在设置了跟踪点的代码行执行指定的次数后发送输出。

对于 "命中次数"，您可以选择在设置了跟踪点的代码行执行了多个等于、为多个或大于或等于指定的命中计数值时输出一条消息。 选择最适合你的需求的选项，并在字段中键入一个整数值（例如5），表示该相关迭代。

![条件表达式命中计数](../debugger/media/conditionalexpressionhitcount.png "条件表达式命中计数")

### <a name="filter"></a>筛选器
对于筛选条件，请指定显示的设备、进程或线程的输出。

![条件表达式筛选器](../debugger/media/conditionalexpressionfilter.png "条件表达式筛选器")

筛选器表达式的列表：

- MachineName = "name"
- ProcessId = value
- ProcessName = "name"
- ThreadId = value
- ThreadName = "name"

用双引号将字符串（如名称）括起来。 输入的值不带引号。 `&`您可以使用（`AND`）、 `||` （`OR`）、 `!` （`NOT`）和括号组合子句。

## <a name="considerations"></a>注意事项

尽管跟踪点旨在使调试更加简洁、更流畅，但在使用时应注意一些注意事项。

有时，当您检查对象的属性或属性时，它的值可能会更改。 这不是由跟踪点功能引起的 bug，但值得一提的是，使用跟踪点来检查对象并不能避免这些意外修改。

在 "**操作**消息" 框中计算表达式的方式可能不同于当前用于开发的语言。 例如，若要输出字符串，你无需将消息包装在引号中，即使你通常在使用`Debug.WriteLine()`或`console.log()`时也是如此。 此外，对于输出表达式，大`{ }`括号语法（）也可能不同于在开发语言中输出值的约定。 （但是，大括号（`{ }`）内的内容仍应使用开发语言的语法编写）。

## <a name="see-also"></a>请参阅

- [什么是调试？](../debugger/what-is-debugging.md)
- [使用 Visual C# Studio 编写更好的代码](../debugger/write-better-code-with-visual-studio.md)
- [首先查看调试](../debugger/debugger-feature-tour.md)
- [调试器中的表达式](expressions-in-the-debugger.md)
- [使用断点](../debugger/using-breakpoints.md)
