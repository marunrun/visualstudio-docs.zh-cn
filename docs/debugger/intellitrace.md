---
title: IntelliTrace | Microsoft Docs
ms.date: 09/19/2018
ms.topic: conceptual
f1_keywords:
- vs.historicaldebug.overview
helpviewer_keywords:
- debugger, recording execution history
- debugging, recording execution history
- IntelliTrace [Visual Studio ALM]
- IntelliTrace, debugging applications
- debugger, (See also IntelliTrace [Visual Studio ALM])
- debugging, (See also IntelliTrace [Visual Studio ALM])
- IntelliTrace
- IntelliTrace, debugging after a crash
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4cbe14e1bf8c3a5e010e3c9e887a208b7e045b4c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536508"
---
# <a name="intellitrace-for-visual-studio-enterprise-c-visual-basic-c"></a>用于 Visual Studio Enterprise 的 IntelliTrace（C#、Visual Basic、C++）

使用 IntelliTrace 记录和跟踪代码的执行历史记录时，可缩短调试应用程序所用的时间。 你可以更轻松地发现 Bug，因为 IntelliTrace 让你能够：

- 记录特定事件

- 检查相关代码、调试程序事件期间“局部变量”窗口中显示的数据以及函数调用信息

- 调试难以重现或在部署中出现的错误

可以在 Visual Studio 企业版（但不可在专业版或社区版）中使用 IntelliTrace。

## <a name="what-do-you-want-to-do"></a>你希望做什么？

|方案|Title|
|-|-|
|**使用 IntelliTrace 调试应用程序：**<br /><br /> - 我想查看以前的事件。<br />- 我想查看以前事件的调用信息。<br />- 保存我的 IntelliTrace 会话。<br />- 控制 IntelliTrace 收集的数据。|- [使用 IntelliTrace 检查上一应用状态](../debugger/view-historical-application-state.md)<br />- [演练：使用 IntelliTrace](../debugger/walkthrough-using-intellitrace.md)<br />- [IntelliTrace 功能](../debugger/intellitrace-features.md)<br />- [历史调试](../debugger/historical-debugging.md)|
|**从已部署的应用程序中收集 IntelliTrace 数据**|- [使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)|
|**从 IntelliTrace 日志文件（.iTrace 文件）中开始调试。**|- [使用保存的 IntelliTrace 数据](../debugger/using-saved-intellitrace-data.md)|

## <a name="what-apps-can-i-debug-with-intellitrace"></a><a name="IntelliTraceSupport"></a>哪些应用程序可以使用 IntelliTrace 进行调试？

| 支持级别| 应用程序类型 |
|---------------------| - |
| 完全支持 | - 使用 .NET Framework 2.0 或更高版本的 Visual Basic 和 Visual C# 应用程序。<br/>你可以调试大多数应用程序，包括 ASP.NET、Microsoft Azure、Windows 窗体、WCF、WPF、Windows 工作流、SharePoint 2010、SharePoint 2013 和 64 位应用。<br/>若要使用 IntelliTrace 对 SharePoint 应用程序进行调试，请参见[演练：使用 IntelliTrace 调试 SharePoint 应用程序](../sharepoint/walkthrough-debugging-a-sharepoint-application-by-using-intellitrace.md)。<br/> 若要使用 IntelliTrace 调试 Microsoft Azure 应用，请参阅[使用 IntelliTrace 和 Visual Studio 调试已发布的云服务](../azure/vs-azure-tools-intellitrace-debug-published-cloud-services.md)。 |
| **有限支持** | - 面向 Windows 的 C++ 应用支持使用 IntelliTrace 后退查看快照。 仅支持调试器和异常事件。<br />- .NET Core 和 ASP.NET Core 应用仅支持本地调试中的某些事件（MVC 控制器、ADO.NET 和 HTTPClient 事件）。 .NET Core 或 ASP.NET Core 应用不支持独立收集器。<br />- 实验证明的 F# 应用<br />- 仅支持事件的 UWP 应用 |
| **不支持** | - 其他语言和脚本<br />- Windows 服务、Silverlight、Xbox 或 Windows Mobile 应用 |

> [!NOTE]
> 如果要调试已经在运行的进程，则只能收集 IntelliTrace 事件（无调用信息）。 只能附加到本地计算机上的 32 位或 64 位进程。 不会收集附加到进程之前发生的事件。

## <a name="why-debug-with-intellitrace"></a><a name="IntelliTraceVSTraditional"></a>为何使用 IntelliTrace 进行调试？

传统或实时调试仅显示应用程序的当前状态以及有关过去事件的有限数据。 要么必须根据应用程序的当前状态推断这些事件，要么必须通过重新运行应用程序以重新生成这些事件。

IntelliTrace 通过记录特定事件和这些时间点的数据，扩展此传统调试体验。 这让你能够不重启应用程序即可查看应用程序中发生了什么，特别是在单步执行到 Bug 处时。 IntelliTrace 在传统调试期间会默认启用，并以不可见的方式自动收集数据。 这样，你即可轻松地在传统调试和 IntelliTrace 调试之间进行切换来查看该记录信息。 请参阅 [IntelliTrace 功能](../debugger/intellitrace-features.md)和 [IntelliTrace 收集哪些数据？](#WhatData)

IntelliTrace 还可帮助你调试难以重现或在部署时出现的错误。 可以收集 IntelliTrace 数据并将其保存为 IntelliTrace 日志文件（.iTrace 文件）。 .iTrace 文件包含有关异常、性能事件、Web 请求、测试数据、线程、模块和其他系统信息的详细信息。 可以在 Visual Studio Enterprise 中打开此文件、选择一个项，然后使用 IntelliTrace 开始调试。 这让你能够转到文件中的任何事件并查看该时间点上有关应用程序的特定详细信息。

你可以从这些源中保存 IntelliTrace 数据：

- Visual Studio 2015 Enterprise 或更新版本，或以前版本的 Visual Studio Ultimate 中的 IntelliTrace 会话。

- IIS 上托管的 ASP.NET Web 应用程序，或使用 Microsoft Monitoring Agent（单独使用或与 System Center 2012 一起使用）时在部署中运行的 SharePoint 2010 和 SharePoint 2013 应用程序。 请参阅[使用 IntelliTrace 独立配置收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)和[使用 Microsoft Monitoring Agent 进行监视](https://technet.microsoft.com/library/dn465153.aspx)。

下面是一些示例，说明 IntelliTrace 如何帮助你进行调试：

- 你的应用程序损坏了一个数据文件，但是你不知道此事件的发生位置。

  如果不使用 IntelliTrace，则必须浏览代码以查找所有可能的文件访问，在这些访问上放置断点，并重新运行应用程序以查找出现问题的位置。 如果使用 IntelliTrace，则在每个事件发生时，可以查看收集的所有文件访问事件和有关应用程序的特定详细信息。

- 发生异常。

  如果不使用 IntelliTrace，你会获得有关异常的消息，但不会获得有关导致异常的事件的大量信息。 可以检查调用堆栈，以查看导致异常的调用链，但不能查看这些调用过程中发生的事件序列。 如果使用 IntelliTrace，你可以检查在异常之前发生的事件。

- 在已部署的应用程序中发生 Bug 或崩溃。

  对于基于 Microsoft Azure 的应用，在发布应用程序之前，可以配置 IntelliTrace 数据收集。 应用程序运行时，IntelliTrace 会将数据保存到 .iTrace 文件。 请参阅[使用 IntelliTrace 和 Visual Studio 调试已发布的云服务](../azure/vs-azure-tools-intellitrace-debug-published-cloud-services.md)。

  对于 IIS 7.0、7.5 和 8.0 上托管的 ASP.NET Web 应用程序，以及 SharePoint 2010 或 SharePoint 2013 应用程序，请使用 Microsoft Monitoring Agent（单独使用或与 System Center 2012 一起使用），以备将 IntelliTrace 数据保存到 .iTrace 文件中。

  当你需要诊断部署中的应用程序的问题时，这会很有用。 请参阅[使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)。

## <a name="what-data-does-intellitrace-collect"></a><a name="WhatData"></a>IntelliTrace 收集哪些数据？

**收集事件信息**

默认情况下，IntelliTrace 仅记录 IntelliTrace 事件：调试程序事件、异常、.NET Framework 事件以及可帮助进行调试的其他系统事件。 你可以选择想要收集的 IntelliTrace 事件的类型（始终收集的调试器事件和异常除外）。 请参阅 [IntelliTrace 功能](../debugger/intellitrace-features.md)。

- **调试器事件**

  IntelliTrace 始终记录 Visual Studio 调试器中发生的事件。 例如，启动应用程序是一个调试程序事件。 其他调试程序事件包括会导致应用程序中断执行的停止事件。 例如，你的程序命中断点、命中跟踪点或执行“步骤”命令。

  默认情况下，为了帮助提高性能，IntelliTrace 不记录调试器事件的每个可能的值。 而是记录以下值：

  - “局部变量”窗口中的值。 请将“局部变量”窗口保持打开状态以查看这些值。

  - “自动”窗口中的值（仅当“自动”窗口处于打开状态时）

  - 在将鼠标指针移到源窗口中的变量的上方以查看其值时显示的数据提示中的值。 IntelliTrace 不收集固定数据提示中的值。

    启用“IntelliTrace 事件”和“快照”模式后，IntelliTrace 将在每个调试器“断点”和“步骤”事件中拍摄应用程序进程的快照 。 这会在“局部变量”、“自动”和“监视”窗口中记录值，无论这些窗口是否打开  。 还会收集任何固定数据提示中的值。

- **异常**

  IntelliTrace 会记录异常类型和以下各类异常的消息：

  - 已处理的异常（已引发并捕获异常）

  - 未经处理的异常

- **.NET Framework 事件**

  默认情况下，IntelliTrace 记录最常见的 .NET Framework 事件。 例如，对于 <xref:System.Windows.Forms.CheckBox.CheckedChanged?displayProperty=nameWithType> 事件，IntelliTrace 收集复选框状态和文本。

- **SharePoint 2010 和 SharePoint 2013 应用程序事件**

  你可以为在 Visual Studio 外运行的 SharePoint 2010 和 2013 应用程序记录用户配置文件事件以及一部分统一日志记录系统 (ULS) 事件。 你可以将这些事件保存到 .iTrace 文件中。 需要 Visual Studio Enterprise 2015 或更高版本、以前版本的 Visual Studio Ultimate，或在“跟踪”模式下运行的 [Microsoft Monitoring Agent](https://www.microsoft.com/download/details.aspx?id=40316)。

  打开 .iTrace 文件时，输入 SharePoint 相关 ID 以查找其匹配的 Web 请求，查看记录事件，并从特定事件开始调试。 如果文件包含未经处理的异常，可以选择相关 ID，开始调试异常。

  请参阅：

  - [使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)

  - [使用保存的 IntelliTrace 数据](../debugger/using-saved-intellitrace-data.md)

  - [演练：使用 IntelliTrace 调试 SharePoint 应用程序](../sharepoint/walkthrough-debugging-a-sharepoint-application-by-using-intellitrace.md)

**捕获快照**

可以配置 IntelliTrace 以捕获每个断点和调试器步骤事件的快照。 IntelliTrace 记录每个快照的完整应用程序状态，这让你能够查看复杂变量并计算表达式。

> [!NOTE]
> [IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)不支持捕获快照。

请参阅[使用 IntelliTrace 检查上一应用状态](../debugger/view-historical-application-state.md)。

**收集函数调用信息**

可以配置 IntelliTrace 以收集函数的调用信息。 此信息使你可以查看调用堆栈历史记录，并能在代码中向后移动和向前移动调用。 对于每个函数调用，IntelliTrace 将记录此数据：

- 功能名称
- 在函数入口点作为参数传递并在函数退出点返回的基元数据类型的值
- 读取或更改自动属性时该属性的值
- 指向第一级子对象的指针，而不是它们的值，除非它们为 null

> [!NOTE]
> IntelliTrace 仅收集数组中的头 256 个对象和字符串的头 256 个字符。

请参阅[使用历史调试检查应用](../debugger/historical-debugging-inspect-app.md)。

**收集模块信息**

若要控制 IntelliTrace 收集的调用信息量，请仅指定你关注的模块。 这有助于在收集期间提高应用程序的性能。 请参阅 IntelliTrace 功能中的[控制 IntelliTrace 收集的信息量](../debugger/intellitrace-features.md#ControlCallData)部分。

## <a name="will-intellitrace-slow-down-my-application"></a><a name="AffectPerformance"></a>IntelliTrace 会让我的应用程序速度变慢吗？

默认情况下，IntelliTrace 仅收集所选 IntelliTrace 事件的数据。 这可能会让应用程序的速度变慢，也可能不会，具体取决于代码的结构和组织。 例如，如果 IntelliTrace 经常记录某个事件，则这可能会让应用程序的速度变慢。 它还可能会让你考虑重构应用程序。

收集调用信息可能会让应用程序的速度显著变慢。 它还可能增加您保存到磁盘的任何 IntelliTrace 日志文件（.iTrace 文件）的大小。 若要尽可能减少这些影响，请仅收集你关注的模块的调用信息。  若要更改 .iTrace 文件的最大大小，请转到“工具”、“选项”、IntelliTrace、“高级”。

### <a name="blogs"></a>博客

[Microsoft DevOps](https://devblogs.microsoft.com/devops/)

### <a name="forums"></a>论坛

[Visual Studio 诊断](https://social.msdn.microsoft.com/Forums/en-US/home)
