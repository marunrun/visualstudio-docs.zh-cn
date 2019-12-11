---
title: 教程：调试 Visual Basic 代码
description: 了解如何启动 Visual Studio 调试器、单步执行代码以及检查数据。
ms.custom: debug-experiment, seodec18, get-started
ms.date: 11/27/2018
ms.technology: vs-ide-debug
ms.topic: tutorial
dev_langs:
- CSharp
helpviewer_keywords:
- debugger
ms.assetid: 62734c0d-a75a-4576-8f73-0e97c19280e1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9b38089a088186a30ebd13cae68d19ac23235bf9
ms.sourcegitcommit: 697f2ab875fd789685811687387e9e8e471a38c4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74829984"
---
# <a name="tutorial-learn-to-debug-visual-basic-code-using-visual-studio"></a>教程：学习使用 Visual Studio 调试 Visual Basic 代码

本文通过分步演练介绍了 Visual Studio 调试器的功能。 如果需要更加深入地了解调试器功能，请参阅[初探调试器](../../debugger/debugger-feature-tour.md)。 当你调试应用时，通常意味着运行附带有调试器的应用程序  。 执行此操作时，调试器在运行过程中可提供许多方法让你查看代码的情况。 你可以逐步浏览代码、查看变量中存储的值、设置对变量的监视以查看值何时改变、检查代码的执行路径、查看代码分支是否正在运行等等。 如果这是你第一次尝试调试代码，可能需要在浏览本文之前阅读[零基础调试](../../debugger/debugging-absolute-beginners.md)。

在本教程中，你将：

> [!div class="checklist"]
> * 启动调试器并命中断点。
> * 了解在调试器中逐步执行代码的命令
> * 检查数据提示和调试器窗口中的变量
> * 检查调用堆栈

## <a name="prerequisites"></a>系统必备

::: moniker range=">=vs-2019"

须安装 Visual Studio 2019 且具有“.NET 桌面开发”工作负载  。

::: moniker-end
::: moniker range="vs-2017"

须安装 Visual Studio 2017 且具有“.NET 桌面开发”工作负载  。

::: moniker-end

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 Visual Studio 安装程序启动。 选择“.NET 桌面开发”工作负载，然后选择“修改”   。

## <a name="create-a-project"></a>创建项目

1. 打开 Visual Studio。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口  。 键入 Ctrl+Q 以打开搜索框，键入“visual basic”，选择“模板”，然后选择“创建新的控制台应用(.NET Core)项目”或“创建新的控制台应用(.NET Framework)项目”      。 在出现的对话框中，键入名称（如 get-started-debugging），然后选择“创建”   。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在顶部菜单栏，依次选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左窗格中，在“Visual Basic”下，选择“Windows 桌面”，然后在中间窗格中选择“控制台应用(.NET Framework)”     。 然后，键入名称（如“get-started-debugging”）并单击“确定”   。
    ::: moniker-end

    如果没有看到“控制台应用(.NET Framework)”项目模板，请转到“工具” > “获取工具和功能...”，这会打开 Visual Studio 安装程序    。 选择“.NET 桌面开发”工作负载，然后选择“修改”   。

    Visual Studio 随即创建项目。

1. 在 Module1.vb  中，替换所有默认代码

    ```vb
    Module Module1

        Sub Main()
        End Sub

    End Module
    ```

    替换为此代码：

    ```vb
    Imports System
    Imports System.Collections.Generic

    Public Class Shape

      ' A few example members
        Public Property X As Integer
            Get
                Return X
            End Get
            Set
            End Set
        End Property

        Public Property Y As Integer
            Get
                Return Y
            End Get
            Set
            End Set
        End Property

        Public Property Height As Integer
            Get
                Return Height
            End Get
            Set
            End Set
        End Property

        Public Property Width As Integer
            Get
                Return Width
            End Get
            Set
            End Set
        End Property

        ' Virtual method
        Public Overridable Sub Draw()
            Console.WriteLine("Performing base class drawing tasks")
        End Sub
    End Class

    Public Class Circle
        Inherits Shape

        Public Overrides Sub Draw()
            ' Code to draw a circle...
            Console.WriteLine("Drawing a circle")
            MyBase.Draw()
        End Sub
    End Class

    Public Class Rectangle
        Inherits Shape

        Public Overrides Sub Draw()
            ' Code to draw a rectangle...
            Console.WriteLine("Drawing a rectangle")
            MyBase.Draw()
        End Sub
    End Class

    Public Class Triangle
        Inherits Shape

        Public Overrides Sub Draw()
            ' Code to draw a triangle...
            Console.WriteLine("Drawing a trangle")
            MyBase.Draw()
        End Sub
    End Class

    Module Module1

        Sub Main(ByVal args() As String)

            Dim shapes = New List(Of Shape) From
            {
                New Rectangle,
                New Triangle,
                New Circle
            }

            For Each shape In shapes
                shape.Draw()
            Next
            ' Keep the console open in debug mode.
            Console.WriteLine("Press any key to exit.")
            Console.ReadKey()

        End Sub

    End Module

    ' Output:
    '    Drawing a rectangle
    '    Performing base class drawing tasks
    '    Drawing a triangle
    '    Performing base class drawing tasks
    '    Drawing a circle
    '    Performing base class drawing tasks
    ```

## <a name="start-the-debugger"></a>启动调试器！

1. 按 F5  （“调试”>“开始调试”  ）或调试工具栏中的“开始调试”  按钮![开始调试](../../debugger/media/dbg-tour-start-debugging.png "开始调试")。

     通过 **F5** 启动应用时，调试器会附加到应用进程，但现在我们还未执行任何特殊操作来检查代码。 因此应用只会加载，控制台输出如你所见。

    ```cmd
    Drawing a rectangle
    Performing base class drawing tasks
    Drawing a triangle
    Performing base class drawing tasks
    Drawing a circle
    Performing base class drawing tasks
    ```

     在本教程中，我们将使用调试器仔细查看此应用，并查看调试器功能。

2. 按红色的停止![停止调试](../../debugger/media/dbg-tour-stop-debugging.png "停止调试")按钮来停止调试器。

## <a name="set-a-breakpoint-and-start-the-debugger"></a>设置断点并启动调试器

1. 在 `Main` 函数的 `For Each` 循环中，通过单击以下代码行的左边距来设置断点：

    `shape.Draw()`

    设置断点的位置会出现一个红色圆圈。

    ![设置断点](../visual-basic/media/get-started-set-breakpoint-vb.png)

    断点是可靠调试的最基本和最重要的功能。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码，以使你可以查看变量的值或内存的行为，或确定代码的分支是否运行。

2. 按“F5”  或“开始调试”  按钮![开始调试](../../debugger/media/dbg-tour-start-debugging.png "开始调试")，应用随即启动，调试器将运行到你设置断点的代码行。

    ![命中断点](../visual-basic/media/get-started-hit-breakpoint-vb.png)

    黄色箭头表示调试器暂停处的语句，它还在同一点上暂停应用执行（此语句尚未执行）。

     如果应用尚未运行，则按 F5 会启动调试器并在第一个断点处停止  。 否则，按 F5 将继续运行应用至下一个断点  。

    当你知道要详细检查的代码行或代码段时，断点功能非常有用。

## <a name="navigate-code-in-the-debugger-using-step-commands"></a>使用单步执行命令在调试器中导航代码

大多数情况下，我们使用键盘快捷方式，因为这是在调试器中快速执行应用的好方法（括号中显示了等效的命令，如菜单命令）。

1. 在 `Main` 函数中的 `shape.Draw` 方法调用中暂停时，按 F11（或选择“调试”>“单步执行”）前进到 `Rectangle` 类的代码   。

     ![使用 F11 单步执行代码](../visual-basic/media/get-started-f11-vb.png "F11 单步执行")

     F11 是“单步执行”命令，每按一次，应用就执行下一个语句  。 F11 是一种以最详尽方式检查执行流的好方法。 （为了更快地浏览代码，我们还向你展示一些其他选项。）默认情况下，调试器会跳过非用户代码（如果需要更多详细信息，请参阅[仅我的代码](../../debugger/just-my-code.md)）。

2. 按几次 F10（或选择“调试”>“单步跳过”），直到调试器停止于 `MyBase.Draw` 方法调用，然后再按一次 F10    。

     ![使用 F10 单步跳过代码](../visual-basic/media/get-started-step-over-vb.png "F10 单步跳过")

     请注意，这次调试器不会单步执行基类 (`Shape`) 的 `Draw` 方法。 按 F10 将使调试器前进，但不会单步执行应用代码中的函数或方法（代码仍将执行）  。 通过在进行 `MyBase.Draw` 方法调用时按“F10”（而不是“F11”），我们跳过了 `MyBase.Draw` 的实现代码（我们现在可能对此不感兴趣）   。

## <a name="navigate-code-using-run-to-click"></a>使用“运行时单击”导航代码

1. 在代码编辑器中，向下滚动并将鼠标悬停在 `Triangle` 类中的 `Console.WriteLine` 方法上，直到左侧出现绿色的“运行时单击”  按钮![运行时单击](../../debugger/media/dbg-tour-run-to-click.png "运行时单击")。 按钮的工具提示显示“将执行运行到此处”。

     ![使用“运行时单击”功能](../visual-basic/media/get-started-run-to-click-vb.png "运行时单击")

   > [!NOTE]
   > “运行时单击”是 [!include[vs_dev15](../../misc/includes/vs_dev15_md.md)] 中的新增按钮  。 如果未看到绿色箭头按钮，请在此示例中改为使用 F11 以使调试器前进到正确的位置  。

2. 单击“运行时单击”  按钮![运行时单击](../../debugger/media/dbg-tour-run-to-click.png "运行时单击")。

    使用此按钮类似于设置临时断点。 “运行时单击”对于快速到达应用代码的可见区域十分方便（你可在任何打开的文件中单击）  。

    调试器前进到 `Triangle` 类的 `Console.WriteLine` 方法实现。 （如果调试程序在你之前设置的断点处首次暂停，请再次使用“运行时单击”  ，使调试程序前进到 `Console.WriteLine`。）

    暂停时，你注意到有拼写错误！ “Drawing a trangle”输出拼写错误。 在调试器中运行应用时，我们可直接在此处修复它。

## <a name="edit-code-and-continue-debugging"></a>编辑代码并继续调试

1. 单击“Drawing a trangle”内并键入校正，将“trangle”更改为“triangle”。

1. 按一次 F11，你会看到调试器再次前进  。

    > [!NOTE]
    > 根据你在调试器中编辑的代码类型，可能会看到一条警告消息。 在某些情况下，代码需要重新编译才能继续。

## <a name="step-out"></a>单步跳出

假设你已完成了对 `Triangle` 类中 `Draw` 方法的检查，并且希望退出该函数但保持位于调试器中。 可使用“单步跳出”命令执行此操作  。

1. 按 Shift + F11（或“调试”>“单步跳出”）    。

     此命令将恢复应用执行（并使调试器前进），直到当前函数返回。

     你应当会回到 `Main` 方法的 `For Each` 循环中。 如果没有，请再次按 Shift + F11   。

## <a name="restart-your-app-quickly"></a>快速重启应用

单击调试工具栏中的“重启”  ![重启应用](../../debugger/media/dbg-tour-restart.png "重启应用")按钮 (Ctrl + Shift + F5)    。

当你按下“重启”时，与停止应用并重启调试器相比，它节省了时间  。 调试器在执行代码命中的第一个断点处暂停。

调试器再次在你在 `shape.Draw()` 方法上设置的断点处停止。

## <a name="inspect-variables-with-data-tips"></a>使用数据提示检查变量

允许你检查变量的功能是调试器最有用的功能之一，并且有不同的方法来执行此操作。 通常，当尝试调试问题时，你试图找出变量是否存储了你期望它们在特定时间具有的值。

1. 在 `shape.Draw()` 方法上暂停时，将鼠标悬停在 `shapes` 对象上，你会看到其默认属性值 `Count` 属性。

1. 展开 `shapes` 对象以查看其所有属性，例如数组 `[0]` 的第一个索引，其值为 `Rectangle`。

     ![查看数据提示](../visual-basic/media/get-started-data-tip-vb.png "查看数据提示")

    可进一步展开对象以查看其属性，例如矩形的 `Height` 属性。

    通常，在调试时，你需要快速检查对象的属性值，数据提示是一种实现此目的的好方法。

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>使用“自动”和“局部变量”窗口检查变量

1. 查看代码编辑器底部的“自动”窗口  。

     ![在“自动”窗口中检查变量](../visual-basic/media/get-started-autos-window-vb.png "“自动”窗口")

    在“自动”窗口中，可看到变量及其当前值  。 “自动”窗口显示当前行或前一行使用的所有变量（检查文档中特定于语言的行为）  。

2. 接下来，我们来看看“自动”窗口旁边的选项卡中的“局部变量”窗口   。

    “局部变量”窗口显示当前[作用域](https://www.wikipedia.org/wiki/Scope_(computer_science))中的变量，即当前执行上下文  。

## <a name="set-a-watch"></a>设置监视

1. 在主代码编辑器窗口中，右键单击 `shapes` 对象，然后选择“添加监视”  。

    “监视”窗口将在代码编辑器的底部打开  。 可使用“监视”窗口指定要关注的变量（或表达式）  。

    现在，你在 `shapes` 对象上设置好了监视，当你在调试器中移动时，可看到其值发生变化。 与其他变量窗口不同，“监视”窗口始终显示你正在监视的变量（当超出作用域时，它们会变灰）  。

## <a name="examine-the-call-stack"></a>检查调用堆栈

1. 在 `For Each` 循环中暂停时，单击“调用堆栈”窗口，默认情况下，该窗口在右下方窗格中打开  。

2. 单击 F11 几次，直到在代码编辑器中 `Rectangle` 类的 `MyBase.Draw` 方法中看到调试器暂停  。 查看“调用堆栈”窗口  。

    ![检查调用堆栈](../visual-basic/media/get-started-call-stack-vb.png "检查调用堆栈")

    “调用堆栈”窗口显示方法和函数被调用的顺序  。 最上面一行显示当前函数（此应用中的 `Rectangle.Draw` 方法）。 第二行显示 `Rectangle.Draw` 是从 `Main` 函数调用的，依此类推。

   > [!NOTE]
   > “调用堆栈”窗口类似于某些 IDE（如 Eclipse）中的调试透视图  。

    调用堆栈是检查和理解应用执行流的好方法。

    可双击代码行来查看该源代码，这也会更改调试器正在检查的当前作用域。 此操作不会使调试器前进。

    还可使用“调用堆栈”窗口中的右键单击菜单执行其他操作  。 例如，你可将断点插入到指定的函数中，使用“运行到光标处”推进调试器，然后检查源代码  。 有关详细信息，请参阅[如何：检查调用堆栈](../../debugger/how-to-use-the-call-stack-window.md)。

## <a name="change-the-execution-flow"></a>更改执行流

1. 调试器在 `Rectangle` 类的 `MyBase.Draw` 方法调用中暂停调试器后，使用鼠标抓住左侧的黄色箭头（执行指针），将黄色箭头向上移动一行到 `Console.WriteLine` 方法调用。

1. 按下 F11  。

    调试器将重新运行 `Console.WriteLine` 方法（你会在控制台窗口输出中看到重复的输出）。

    通过更改执行流，你可以进行测试不同代码执行路径或重新运行代码等操作，而无需重启调试器。

    > [!WARNING]
    > 通常你需要小心使用此功能，工具提示中会出现警告。 你也可能会看到其他警告。 移动指针无法将应用程序还原到更早的应用状态。

1. 按 F5 继续运行应用  。

    恭喜你完成本教程！

## <a name="next-steps"></a>后续步骤

在本教程中，你已了解了如何启动调试器、逐步执行代码以及检查变量。 你可能会希望更深入地了解调试器功能以及查看指向更多信息的链接。

> [!div class="nextstepaction"]
> [初探调试器](../../debugger/debugger-feature-tour.md)
