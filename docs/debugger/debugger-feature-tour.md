---
title: 初探调试器
description: 开始使用 Visual Studio 调试器调试应用程序
ms.custom: ''
ms.date: 04/08/2019
ms.topic: tutorial
helpviewer_keywords:
- debugger
ms.assetid: c763d706-3213-494f-b4d2-990b6e1ec456
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 93973322c40ca62396414317c2ad8875e9b94854
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578956"
---
# <a name="first-look-at-the-visual-studio-debugger"></a>初步了解 Visual Studio 调试器

本主题介绍 Visual Studio 提供的调试器工具。 在 Visual Studio 上下文中，当调试应用时，这通常意味着你在附加了调试器的情况下（即在调试器模式下）运行应用程序。 执行此操作时，调试器在运行过程中可提供许多方法让你查看代码的情况。 你可以逐步执行代码、查看变量中存储的值、设置对变量的监视以查看值何时改变、检查代码的执行路径等。如果这是你第一次尝试调试代码，建议在学习本主题之前阅读[零基础调试](../debugger/debugging-absolute-beginners.md)。

此处所述的功能适用于 C#、C++、Visual Basic、JavaScript 和 Visual Studio 支持的其他语言（除非另有说明）。

## <a name="set-a-breakpoint-and-start-the-debugger"></a>设置断点并启动调试器

要进行调试，需要在调试器附加到应用进程的情况下启动应用。 F5（“调试”>“开始调试”）是执行该操作最常见的方法。 但是，现在你可能没有设置任何断点来检查应用代码，因此我们首先设置断点再开始调试。 断点是可靠调试的最基本和最重要的功能。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码，以使你可以查看变量的值或内存的行为，或确定代码的分支是否运行。

若代码编辑器中打开了文件，则可通过单击代码行左侧的边缘来设置断点。

![设置断点](../debugger/media/dbg-tour-set-a-breakpoint.gif "设置断点")

按 F5（“调试”>“开始调试”）或调试工具栏中的“开始调试”按钮 ![开始调试](../debugger/media/dbg-tour-start-debugging.png "开始调试")，调试器将运行至它遇到的第一个断点。 如果应用尚未运行，则按 F5 会启动调试器并在第一个断点处停止。

当你知道要详细检查的代码行或代码段时，断点功能非常有用。

## <a name="navigate"></a> 使用单步执行命令在调试器中移动浏览代码

我们为大多数命令提供键盘快捷键，便于你更快地移动浏览应用代码。 （括号中显示了等效命令，如菜单命令。）

要在附加了调试器的情况下启动应用，请按 F11（“调试”>“单步执行”）。 F11 是“单步执行”命令，每按一次，应用就执行下一个语句。 使用 F11 启动应用时，调试器会在执行的第一个语句上中断。

![F11 单步执行](../debugger/media/dbg-tour-f11.png "F11 单步执行")

黄色箭头表示调试器暂停处的语句，它还在同一点上暂停应用执行（此语句尚未执行）。

F11 是一种以最详尽方式检查执行流的好方法。 （为了更快地浏览代码，我们还向你展示了一些其他选项。）默认情况下，调试器会跳过非用户代码（如果需要更多详细信息，请参阅[仅我的代码](../debugger/just-my-code.md)）。

>[!NOTE]
> 在托管代码中将看到一个对话框，询问你是否希望在自动跳过属性和运算符时收到通知（默认行为）。 若稍后想更改设置，请在“调试”下的“工具”>“选项”菜单中禁用“单步跳过属性和运算符”设置。

## <a name="step-over-code-to-skip-functions"></a>单步跳过代码以跳过函数

如果所在的代码行是函数或方法调用，则可以按 F10（“调试”>“单步跳过”）而不是 F11。

按 F10 将使调试器前进，但不会单步执行应用代码中的函数或方法（代码仍将执行）。 按 F10 可跳过你不感兴趣的代码。 这样就可以快速转到更感兴趣的代码。

## <a name="step-into-a-property"></a>单步执行属性

如前所述在默认情况下，调试器会跳过托管属性和字段，但通过“单步执行特定内容”命令可替代此行为。

右键单击属性或字段，选择“单步执行特定内容”，然后选择一个可用选项。

![单步执行特定内容](../debugger/media/dbg-tour-step-into-specific.png "单步执行特定内容")

在此示例中，通过“单步执行特定内容”将转到 `Path.set` 的代码。

![单步执行特定内容](../debugger/media/dbg-tour-step-into-specific-2.png "单步执行特定内容")

## <a name="run-to-a-point-in-your-code-quickly-using-the-mouse"></a>使用鼠标快速运行到代码中的某个点

在调试器中，将鼠标悬停在代码行上，直到“运行到单击处”（将执行运行到此处）按钮![运行到单击处](../debugger/media/dbg-tour-run-to-click.png "运行时单击")出现在左侧。

![运行到单击处](../debugger/media/dbg-tour-run-to-click-2.png "运行时单击")

> [!NOTE]
> 自 [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] 起，可用使用“运行到单击位置”（将执行运行到此处）按钮。

单击“运行到单击处”（将执行运行到此处）按钮。 调试器将前进到单击的代码行。

使用此按钮类似于设置临时断点。 此命令对于快速到达应用代码的可见区域也很方便。 你可在任何打开的文件中使用“运行到单击处”。

## <a name="advance-the-debugger-out-of-the-current-function"></a>使调试器从当前函数中跳出

有时你可能希望继续调试会话，但在整个当前函数中一直使调试器前进。

按 Shift+F11（或“调试”>“单步跳出”）。

此命令将恢复应用执行（并使调试器前进），直到当前函数返回。

## <a name="run-to-cursor"></a>运行到光标处

按“停止调试”红色按钮![停止调试](../debugger/media/dbg-tour-stop-debugging.png "停止调试")或 **Shift** + **F5** 来停止调试器。

右键单击应用中的代码行，然后选择“运行到光标处”。 此命令将启动调试并在当前代码行上设置临时断点。

![运行到光标处](../debugger/media/dbg-tour-run-to-cursor.png "运行到光标处")

如果设置了断点，则调试器会在其命中的第一个断点处暂停。

按 F5，直至到达在其上选择了“运行到光标处”的代码行。

当编辑代码并希望快速设置临时断点并同时启动调试器时，此命令很有用。

> [!NOTE]
> 调试时可使用“调用堆栈”窗口中的“运行到光标处”。

## <a name="restart-your-app-quickly"></a>快速重启应用

单击调试工具栏中的“重启”按钮![重启应用](../debugger/media/dbg-tour-restart.png "重启应用")（“Ctrl+Shift+F5”）。

当你按下“重启”时，与停止应用并重启调试器相比，它节省了时间。 调试器在执行代码命中的第一个断点处暂停。

若确实要停止调试器并返回到代码编辑器，可以按红色停止![停止调试](../debugger/media/dbg-tour-stop-debugging.png "停止调试")按钮而不是“重启”。

## <a name="edit-your-code-and-continue-debugging-c-vb-c-xaml"></a>编辑代码并继续调试（C#、VB、C++、XAML）

在 Visual Studio 支持的大多数语言中，你都可以在调试会话的过程中编辑代码，然后继续调试。 要使用此功能，请先在调试器中暂停，用鼠标点击进入代码，进行编辑，然后按 **F5**、**F10** 或 **F11** 键继续调试。

![编辑并继续调试](../debugger/media/dbg-tips-edit-and-continue.gif "EditAndContinue")

有关功能使用和功能限制的详细信息，请参阅[编辑并继续](../debugger/edit-and-continue.md)。

若要在调试会话期间修改 XAML 代码，请参阅[使用 XAML 热重载编写和调试正在运行的 XAML 代码](../xaml-tools/xaml-hot-reload.md)。

## <a name="inspect-variables-with-data-tips"></a>使用数据提示检查变量

既然你已经有了粗略的了解，那么就有机会开始使用调试器检查应用状态（变量）。 那些允许你检查变量的功能是调试器的一些最有用的功能，并且有不同方法可执行此操作。 通常，当尝试调试问题时，你试图找出变量是否存储了你期望它们在特定应用状态具有的值。

在调试器中暂停时，将鼠标悬停在对象上并看到其默认属性值（在此示例中，文件名 `market 031.jpg` 是默认属性值）。

![查看数据提示](../debugger/media/dbg-tour-data-tips.gif "查看数据提示")

展开对象以查看其所有属性（例如本示例中的 `FullPath` 属性）。

通常，在调试时，你需要快速检查对象的属性值，数据提示是一种实现此目的的好方法。

> [!TIP]
> 在大多数受支持的语言中，可在调试会话中途编辑代码。 有关详细信息，请参阅[编辑并继续](../debugger/edit-and-continue.md)。

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>使用“自动”和“局部变量”窗口检查变量

调试时，查看代码编辑器底部的“自动”窗口。

![“自动”窗口](../debugger/media/dbg-tour-autos-window.png "“自动”窗口")

在“自动”窗口中，可看到变量及其当前值和类型。 “自动”窗口显示当前行或前一行使用的所有变量（在 C++ 中，该窗口显示前三个代码行中的变量。 查看文档以了解特定于语言的行为）。

> [!NOTE]
> 在 JavaScript 中，支持“局部变量”窗口，但不支持“自动”窗口。

接下来，查看“局部变量”窗口。 “局部变量”窗口显示当前范围中的变量。

![“局部变量”窗口](../debugger/media/dbg-tour-locals-window.png "局部变量窗口")

在此示例中，`this` 对象和 `f` 对象处于范围内。 有关详细信息，请参阅[在“自动”窗口和“局部变量”窗口中检查变量](../debugger/autos-and-locals-windows.md)。

## <a name="set-a-watch"></a>设置监视

可使用“监视”窗口指定要关注的变量（或表达式）。

在调试时，右键单击对象并选择“添加监视”。

![“监视”窗口](../debugger/media/dbg-tour-watch-window.png "监视窗口")

在本示例中，你在 `f` 对象上设置了监视，当在调试器中移动时，可看到其值发生了变化。 与其他变量窗口不同，“监视”窗口始终显示正在监视的变量（当超出范围时，它们会变灰）。

有关详细信息，请参阅[使用“监视”窗口和“快速监视”窗口设置监视](../debugger/watch-and-quickwatch-windows.md)

## <a name="examine-the-call-stack"></a>检查调用堆栈

调试时单击“调用堆栈”窗口，默认情况下，该窗口在右下方窗格中打开。

![检查调用堆栈](../debugger/media/dbg-tour-call-stack.png "检查调用堆栈")

“调用堆栈”窗口显示方法和函数被调用的顺序。 最上面一行显示当前函数（此示例中的 `Update` 方法）。 第二行显示 `Update` 是从 `Path.set` 属性调用的，依此类推。 调用堆栈是检查和理解应用执行流的好方法。

> [!NOTE]
> “调用堆栈”窗口类似于某些 IDE（如 Eclipse）中的调试透视图。

可双击代码行来查看该源代码，这也会更改调试器正在检查的当前范围。 此操作不会使调试器前进。

还可使用“调用堆栈”窗口中的右键单击菜单执行其他操作。 例如，你可将断点插入到指定的函数中，使用“运行到光标处”重启应用，然后检查源代码。 请参阅[如何：检查调用堆栈](../debugger/how-to-use-the-call-stack-window.md)。

## <a name="exception"></a> 检查异常

应用引发异常时，调试器会将你转至引发异常的代码行。

![异常帮助程序](../debugger/media/dbg-tour-exception-helper.png "异常帮助程序")

在此示例中，异常帮助程序向你显示 `System.Argument` 异常以及一条错误消息，指出该路径不是合法形式。 因此，我们知道方法或函数参数发生了错误。

在此示例中，`DirectoryInfo` 调用在存储于 `value` 变量中的空字符串上引发了错误。

异常帮助程序是帮助调试错误的好功能。 你还可以执行其他操作，如查看错误详细信息及从异常帮助程序添加监视。 或者，如有需要可更改引发特定异常的条件。 有关如何在代码中处理异常的详细信息，请参阅[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)。

> [!NOTE]
> 异常帮助程序取代了从 [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] 开始提供的异常情况助手。

展开“异常设置”节点以查看有关如何处理此异常类型的更多选项，但对于本教程无需更改任何内容！

## <a name="configure-debugging"></a>配置调试

可以将要生成的项目配置为[调试或发布配置](../debugger/how-to-set-debug-and-release-configurations.md)，配置项目属性进行调试，或配置[常规设置](../debugger/how-to-specify-debugger-settings.md)进行调试。 此外，还可以将调试器配置为使用 [DebuggerDisplay](using-the-debuggerdisplay-attribute.md) 特性或 [NatVis 框架](create-custom-views-of-native-objects.md)（对于 C/C++）等功能显示自定义信息。

调试属性特定于每个项目类型。 例如，在启动应用程序后，可以指定要传递给应用程序的参数。 在解决方案资源管理器中，右键单击项目并选择“属性”，可以访问特定于项目的属性。 调试属性通常显示在“生成”或“调试”选项卡中，具体取决于特定的项目类型。

![项目属性](../debugger/media/dbg-tour-project-properties.png "项目属性")

## <a name="debug-live-aspnet-apps-in-azure-app-service"></a>在 Azure 应用服务中调试实时 ASP.NET 应用

当执行感兴趣的代码时，Snapshot Debugger 会为生产中的应用拍摄快照。 若要指示该调试器拍摄快照，可以在代码中设置快照点和记录点。 通过该调试器，可精确查看出错的内容，而不会影响生产应用程序的流量。 Snapshot Debugger 有助于大幅减少解决生产环境中出现的问题所需的时间。

![启动 Snapshot Debugger](../debugger/media/snapshot-launch.png "启动 Snapshot Debugger")

快照集合适用于在 Azure 应用服务中运行的 ASP.NET 应用程序。 ASP.NET 应用程序必须在 .NET Framework 4.6.1 或更高版本上运行，并且 ASP.NET Core 应用程序必须在 Windows 上的 .NET Core 2.0 或更高版本上运行。

有关详细信息，请参阅[使用 Snapshot Debugger 调试实时 ASP.NET 应用](../debugger/debug-live-azure-applications.md)。

## <a name="view-snapshots-with-intellitrace-step-back-visual-studio-enterprise"></a>使用 IntelliTrace 后退查看快照 (Visual Studio Enterprise)

IntelliTrace 后退会在每个断点处及调试器步骤事件发生时自动拍摄应用程序的快照。 凭借记录的快照便可以返回到上一个断点或步骤，并查看当时应用程序的状态。 如果希望查看以前的应用程序状态，但不想重新启动调试或重新创建所需应用状态，使用 IntelliTrace 后退可以节省时间。

可以通过使用调试工具栏中的“后退”和前进”按钮浏览和查看快照。 这些按钮用于浏览“诊断工具”窗口中“事件”选项卡上显示的事件。

![“后退”和“前进”按钮](../debugger/media/intellitrace-step-back-icons-description.png  "“后退”和“前进”按钮")

有关详细信息，请参阅[使用 IntelliTrace 检查上一应用状态](../debugger/view-historical-application-state.md)页。

## <a name="debug-performance-issues"></a>调试性能问题

如果应用运行速度太慢或使用了太多内存，你可能需要尽早使用分析工具来测试应用。 有关分析工具（例如 CPU 使用情况工具和内存分析器）的详细信息，请参阅[首先查看分析工具](../profiling/profiling-feature-tour.md)。

## <a name="next-steps"></a>后续步骤

在本教程中，你已快速了解了许多调试器功能。 你可能会需要更深入地了解其中一个功能，例如断点。

> [!div class="nextstepaction"]
> [了解如何使用断点](../debugger/using-breakpoints.md)
