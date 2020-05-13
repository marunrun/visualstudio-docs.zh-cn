---
title: 调试器中的提示和技巧
description: 了解 Visual Studio 调试器支持的一些鲜为人知的功能
ms.custom: seodec18
ms.date: 06/15/2018
ms.topic: conceptual
helpviewer_keywords:
- stepping
- debugging [Visual Studio], execution control
- execution, controlling in debugger
ms.assetid: 5262d8b1-2648-429e-85d5-90fcaadfb362
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bf8d6df020694bb10fe4f3f051551056549d5673
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301175"
---
# <a name="learn-productivity-tips-and-tricks-for-the-debugger-in-visual-studio"></a>了解 Visual Studio 调试器在工作效率方面的提示和技巧

通过阅读本主题，了解 Visual Studio 调试器在工作效率方面的一些提示和技巧。 有关调试器的基本功能，请参阅[首先查看调试器](../debugger/debugger-feature-tour.md)。 在本主题中，我们将了解功能介绍中没有涉及的一些领域。

## <a name="pin-data-tips"></a>固定数据提示

如果你在调试时，经常将鼠标悬停在数据提示上，就可能想固定变量的数据提示，方便自己随时查看。 即使在重新启动后，固定的变量也能保持不动。 要固定数据提示，请在鼠标悬停其上时单击固定图标。 你可以固定多个变量。

![固定数据提示](../debugger/media/dbg-tips-data-tips-pinned.png "固定数据提示")

## <a name="edit-your-code-and-continue-debugging-c-vb-c"></a>编辑代码并继续调试（C#、VB、C++）

在 Visual Studio 支持的大多数语言中，你都可以在调试会话的过程中编辑代码，然后继续调试。 要使用此功能，请先在调试器中暂停，用鼠标点击进入代码，进行编辑，然后按 **F5**、**F10** 或 **F11** 键继续调试。

![编辑并继续调试](../debugger/media/dbg-tips-edit-and-continue.gif "EditAndContinue")

有关功能使用和功能限制的详细信息，请参阅[编辑并继续](../debugger/edit-and-continue.md)。

## <a name="edit-xaml-code-and-continue-debugging"></a>编辑 XAML 代码并继续调试

若要在调试会话期间修改 XAML 代码，请参阅[使用 XAML 热重载编写和调试正在运行的 XAML 代码](../xaml-tools/xaml-hot-reload.md)。

## <a name="debug-issues-that-are-hard-to-reproduce"></a>难以重现的调试问题

如果在应用中重新实现特定状态很困难或很费时，可以考虑使用条件断点。 你可以使用[条件断点](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)并对其加以筛选，以免破坏应用代码，直到应用进入所需的状态（例如，变量正在存储错误数据的状态）。 你可以使用表达式、筛选器、命中次数等来设置条件。

#### <a name="to-create-a-conditional-breakpoint"></a>创建条件断点

1. 右键单击断点图标（红色球）并选择 **"条件**"。

2. 在**断点设置**窗口中，键入一个表达式。

    ![条件断点](../debugger/media/dbg-multithreaded-conditional-breakpoint.png "条件断点")

3. 如果你对另一种类型的条件感兴趣，请在**断点设置**对话框中选择**筛选器**，而不是**条件表达式**，然后按照筛选器的提示操作。

## <a name="configure-the-data-to-show-in-the-debugger"></a>配置要在调试器中显示的数据

对于 C#、Visual Basic 和C++（仅限C++/CLI 代码），您可以使用[DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md)属性告诉调试器要显示哪些信息。 对于C++代码，您可以使用[Natvis 可视化进行相同的操作](create-custom-views-of-native-objects.md)。

## <a name="change-the-execution-flow"></a>更改执行流

让调试器暂停在某行代码上，用鼠标抓住左侧的黄色箭头指针。 将黄色箭头指针移动到代码执行路径中的其他点上。 然后通过 F5 键或步骤命令继续运行应用。

![移动执行指针](../debugger/media/dbg-tour-move-the-execution-pointer.gif "移动执行指针")

通过更改执行流，你可以进行测试不同代码执行路径或重新运行代码等操作，而无需重启调试器。

> [!WARNING]
> 通常你需要小心使用此功能，工具提示中会出现警告。 你也可能会看到其他警告。 移动指针无法将应用还原到较早的应用程序状态。

## <a name="track-an-out-of-scope-object-c-visual-basic"></a>跟踪范围外对象（C#，可视基本）

使用调试器窗口（如**Watch**窗口）轻松查看变量。 但是，当变量超出 **"监视"** 窗口中的范围时，您可能会注意到该变量已灰显。在某些应用方案中，即使变量已出范围，变量的值也可能更改，您可能需要密切监视它（例如，变量可能会收集垃圾）。 您可以通过在 **"监视"** 窗口中为其创建对象 ID 来跟踪该变量。

#### <a name="to-create-an-object-id"></a>创建对象 ID

1. 在要跟踪的变量附近设置一个断点。

2. 启动调试器 （**F5**）， 并在断点停止。

3. 在 **"局部变量"** 窗口中查找变量（**调试> Windows >局部变量**），右键单击该变量，然后选择 **"使对象 ID**"。

    ![创建对象 ID](../debugger/media/dbg-tips-watch-create-object-id.png "CreateObjectID")

4. 您应该在**$****"局部变量"** 窗口中看到加号。 此变量是对象 ID。

5. 右键单击对象 ID 变量并选择 **"添加监视**"。

有关详细信息，请参阅[创建对象 ID](../debugger/watch-and-quickwatch-windows.md#bkmk_objectIds)。

## <a name="view-return-values-for-functions"></a>查看函数的返回值

要查看函数的返回值，请查看在单步执行代码时显示在 **"自动"** 窗口中的函数。 要查看函数的返回值，请确保感兴趣的函数已执行（如果当前在函数调用时已停止，请按**F10）。** 如果窗口已关闭，请使用**调试> Windows >自动**"打开 **"自动"** 窗口。

![自动窗口](../debugger/media/dbg-tips-autos-window.png "自动窗口")

此外，您可以在 **"立即"** 窗口中输入函数以查看返回值。 （使用**调试> Windows > 立即**打开它。

![即时窗口](../debugger/media/dbg-tips-immediate-window.png "即时窗口")

此外，还可以在**监视**和**即时**窗口中使用[伪变量](../debugger/pseudovariables.md)，如 `$ReturnValue`。

## <a name="inspect-strings-in-a-visualizer"></a><a name="string_visualizer"></a>检查可视化工具中的字符串

在使用字符串时，如果能看到完整的、带格式的字符串会很有帮助。 要查看纯文本、XML、HTML 或 JSON 字符串，请单击放大镜图标![VisualizerIcon，](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")同时悬停在包含字符串值的变量上。

![打开字符串可视化工具](../debugger/media/dbg-tips-string-visualizers.png "OpenString可视化器")

字符串可视化工具可以帮你确定字符串的格式是否正确，具体取决于字符串的类型。 例如，如果**值**字段为空，表明可视化工具类型未识别出该字符串。 有关详细信息，请参阅[字符串可视化器对话框](../debugger/string-visualizer-dialog-box.md)。

![JSON 字符串可视化器](../debugger/media/dbg-tips-string-visualizer-json.png "JSONString可视化器")

对于在调试器窗口中显示的一些其他类型的类型（如 DataSet 和 DataTable 对象），您还可以打开内置可视化工具。

## <a name="break-into-code-on-handled-exceptions"></a>在已处理的异常处中断代码

调试器会侵入未处理的异常代码。 但是，处理的异常（如`try/catch`块内发生的异常）也可以是 Bug 的来源，您可能需要在它们发生时进行调查。 通过将调试器配置为分解处理的异常的代码，还可以通过在 **"例外设置"** 对话框中配置选项来设置调试器。 通过选择 **"调试> Windows >异常设置**"来打开此对话框。

通过**异常设置**对话框，你可以让调试器在特定异常处中断代码。 在下图中，调试器会在发生 `System.NullReferenceException` 时中断代码。 有关详细信息，请参阅[管理异常](../debugger/managing-exceptions-with-the-debugger.md)。

![例外设置对话框](../debugger/media/dbg-tips-exception-settings.png "例外设置对话框")

## <a name="debug-deadlocks-and-race-conditions"></a>调试死锁和争用条件

如果需要调试的问题对于多线程应用程序很常见，在调试时查看线程的位置，通常会有所帮助。 可使用**源中显示线程**按钮轻松完成此操作。

#### <a name="to-show-threads-in-your-source-code"></a>在源代码中显示线程

1. 调试时，单击"**源"中的"显示线程****"按钮"在调试**工具栏![中显示源中的线程](../debugger/media/dbg-multithreaded-show-threads.png "线程标记")"。

2. 查看窗口左侧的滚动条槽。 在这条线上，您会看到类似于两个布螺纹的*螺纹标记*图标![线程标记](../debugger/media/dbg-thread-marker.png "线程标记")。 线程标记指示线程在此位置停止。

    注意，线程标记可能被断点不完全遮挡。

3. 将指针悬停在线程标记上。 屏幕上显示数据提示。 数据提示将告诉您每个已停止线程的名称和线程 ID 号。

    您还可以在["并行堆栈"窗口中](../debugger/get-started-debugging-multithreaded-apps.md)查看线程的位置。

::: moniker range="vs-2017"
## <a name="examine-payloads-for-web-services-and-network-resources-uwp"></a>检查 Web 服务和网络资源 （UWP） 的有效负载

在 UWP 应用中，您可以分析使用`Windows.Web.Http`API 执行的网络操作。 您可以使用此工具来帮助调试 Web 服务和网络资源。 要使用该工具，请选择 **"调试>性能探查器**"。 选择 **"网络**"，然后选择 **"开始**"。 在应用中，浏览使用 `Windows.Web.Http` 的应用场景，然后选择“停止收集”**** 生成报表。

![网络使用情况分析工具](../profiling/media/prof-tour-network-usage.png "网络使用工具")

选择摘要视图中的操作以查看更多详细信息。

![网络使用情况工具中的详细信息](../profiling/media/prof-tour-network-usage-details.png "详细查看网络使用情况")

有关详细信息，请参阅[网络使用情况](../profiling/network-usage.md)。
::: moniker-end

## <a name="get-more-familiar-with-how-the-debugger-attaches-to-your-app-c-c-visual-basic-f"></a><a name="modules_window"></a>更熟悉调试器如何附加到应用（C#、C++、可视化基本、F#）

若要附加到正在运行的应用，调试器将加载为想要调试的应用的相同内部版本生成的符号 (.pdb) 文件。 在某些情况下，了解符号文件的一些知识非常有用。 你可在**模块**窗口中检查 Visual Studio 如何加载符号文件。

通过选择**Modules****"调试> Windows > 模块，** 在调试时打开模块窗口。 **"模块"** 窗口可以告诉您调试器将哪些模块视为用户代码，或[*"我的代码*](../debugger/just-my-code.md)"，以及模块的符号加载状态。 在大多数情况下，调试器会自动查找用户代码的符号文件，但如果要进入（或调试）.NET代码、系统代码或第三方库代码，需要额外的步骤才能获取正确的符号文件。

![在"模块"窗口中查看符号信息](../debugger/media/dbg-tips-modules-window.png "查看符号信息")

你可以直接在**模块**窗口中右键单击并选择**加载符号**来加载符号信息。

有时，应用开发人员发布的应用不包含匹配的符号文件 （为了减少占用的空间），但会为内部版本保留一份匹配的符号文件，用于以后调试发布版本。

了解如何调试器如何区分用户代码，请参阅[仅我的代码](../debugger/just-my-code.md)。 要了解有关符号文件的更多内容，请参阅[在 Visual Studio 调试器中指定符号 （.pdb） 和源文件](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

## <a name="learn-more"></a>了解详细信息

有关其他提示和技巧以及更多详细信息，请参阅以下博客文章：

- [使用 Visual Studio 调试时，7个简单的已知技巧](https://devblogs.microsoft.com/visualstudio/7-lesser-known-hacks-for-debugging-in-visual-studio/)
- [Visual Studio 中 7 个隐藏的 gem](https://devblogs.microsoft.com/visualstudio/7-hidden-gems-in-visual-studio-2017/)

## <a name="see-also"></a>另请参阅

[键盘快捷键](../ide/productivity-shortcuts.md)
