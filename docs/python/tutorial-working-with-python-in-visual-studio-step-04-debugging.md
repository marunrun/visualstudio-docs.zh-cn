---
title: Visual Studio 中的 Python 教程步骤 4，调试
titleSuffix: ''
description: 在 Visual Studio 中使用 Python 功能的核心教程的第 4 步，介绍了如何在调试器中运行 Python 代码。
ms.date: 01/28/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: d7fe5a8b2275248c0fc68f9237e9e259973c567b
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801719"
---
# <a name="step-4-run-code-in-the-debugger"></a>步骤 4：在调试器中运行代码

**上一步：[使用交互式 REPL 窗口](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md)**

除了管理项目、提供丰富的编辑体验和交互  窗口，Visual Studio 还对 Python 代码提供功能全面的调试。 在调试器中，可以分步运行代码，包括循环的每次迭代。 还可以在符合某些条件时暂停程序。 无论程序何时在调试器中暂停，用户都可以检查整个程序状态，并更改变量的值。 此类操作对于追查程序 bug 至关重要，而且非常有助于仔细跟踪确切的程序流程。

1. 用以下代码替换 PythonApplication1.py  文件中的代码。 此代码变体展开了 `make_dot_string`，以便用户在调试器中检查其各个步骤。 它还将 `for` 循环放入 `main` 函数，并通过调用该函数显式运行该循环：

    ```python
    from math import cos, radians

    # Create a string with spaces proportional to a cosine of x in degrees
    def make_dot_string(x):
        rad = radians(x)                             # cos works with radians
        numspaces = int(20 * cos(radians(x)) + 20)   # scale to 0-40 spaces
        st = ' ' * numspaces + 'o'                   # place 'o' after the spaces
        return st

    def main():
        for i in range(0, 1800, 12):
            s = make_dot_string(i)
            print(s)

    main()
    ```

1. 按 F5  或选择“调试”   > “开始调试”  菜单命令，检查代码是否正常运行。 此命令会在调试器中运行代码，但由于在程序运行时未执行任何操作来暂停程序，因此它只针对几次迭代输出波浪图案。 按任意键关闭输出窗口。

    > [!Tip]
    > 要在程序完成时自动关闭输出窗口，请选择“工具” > “选项”菜单命令，展开“Python”节点，选择“调试”，然后清除选项“进程正常退出时等待输入”      ：
    >
    > ![Python 调试选项，用于在程序正常退出时关闭输出窗口](media/vs-getting-started-python-22-debugging5.png)

1. 若要在 `for` 语句上设置断点，可单击该行的灰色边距，或将插入点置于该行并使用“调试”   > “切换断点”  命令 (F9  )。 灰色边距中显示的红点用来表示该断点（如以下箭头标记所示）：

    ![设置断点](media/vs-getting-started-python-18-debugging1.png)

1. 再次启动调试器 (F5  )，将看到代码运行至包含该断点的行处停止。 可在此处检查调用堆栈，并检查变量。 范围内的变量经过定义后显示在“自动”  窗口中；也可以在该窗口底部切换到“局部变量”  视图，以显示 Visual Studio 在当前范围（包括函数）内找到的所有变量，即使这些变量尚未定义也会显示：

    ![Python 的断点 UI 体验](media/vs-getting-started-python-19-debugging2b.png)

1. 观察 Visual Studio 窗口顶部的调试工具栏（如下所示）。 此工具栏可供快速访问最常见的调试命令（也可以在“调试”  菜单上找到）：

    ![基本调试工具栏按钮](media/vs-getting-started-python-20-debugging3.png)

    按钮从左到右如下所示：
    - 继续  (F5  )：运行程序直到下一个断点或直到程序完成。
    - 全部中断  (Ctrl  +Alt  +Break  )：暂停长时间运行的程序。
    - 停止调试  (Shift  +F5  )：停止程序（无论已运行到哪个位置），并退出调试器。
    - 重新启动  (Ctrl  +Shift  +F5  )：停止程序（无论已运行到哪个位置），并在调试器中从头开始重新启动程序。
    - 显示下一语句 (Alt+Num &#42;)：切换到下一行要运行的代码     。 在调试会话期间在代码内导航，并且想要快速返回到调试器的暂停点时，此按钮最有用。
    - 单步执行(进入过程)  (F11  )：运行下一行代码，并进入被调用的函数。
    - 单步执行(跳过过程)  (F10  )：运行下一行代码，但不进入被调用的函数。
    - 单步执行(跳出过程)  (Shift**Shift**+F11  )：运行当前函数的其余部分，并在调用代码中暂停。

1. 使用“单步执行(跳过过程)”  单步执行（跳过过程）`for` 语句。 *单步执行*是指调试器运行当前代码行，包括所有函数调用，然后立即再次暂停。 注意变量 `i` 现在在“局部变量”  和“自动”  窗口中是如何定义的。

1. 单步执行（跳过过程）下一行代码，该命令将调用 `make_dot_string` 并暂停。 确切来说，此处的单步执行(跳过过程)  是指调试器运行整个 `make_dot_string` 并在它返回时暂停。 调试器不在该函数内停止，除非其中存在单独的断点。

1. 继续单步执行（跳过过程）代码几次，观察“局部变量”  或“自动”  窗口中的值如何变化。

1. 在“局部变量”  或“自动”  窗口中，双击 `i` 或 `s` 变量的“值”  列，以编辑值。 按 Enter 或单击该值外的任意位置以应用任何更改。

1. 继续使用“单步执行(进入过程)”  单步调试代码。 “单步执行(进入过程)”  是指调试器进入它有相关调试信息的任何函数调用内，比如 `make_dot_string`。 进入 `make_dot_string` 后，可以检查其局部变量并专门单步调试其代码。

1. 继续使用“单步执行(进入过程)”  单步执行代码，注意到达 `make_dot_string` 末尾时，下一步会返回到 `for` 循环并为 `s` 变量赋予新的返回值。 再次单步执行 `print` 语句时，请注意，在 `print` 上单步执行（进入过程）  不会进入该函数。 这是因为 `print` 不是用 Python 编写的，而是 Python 运行时内的本机代码。

1. 继续使用“单步执行(进入过程)”  ，直到再次部分进入 `make_dot_string`。 然后使用“单步执行(跳出过程)”  ，注意将返回到 `for` 循环。 使用“单步执行(跳出过程)”  时，调试器运行函数的其余部分，然后在调用代码中自动暂停。 此命令对于以下情况非常有用：已单步调试某个要调试的较长函数的某一部分，但无需单步调试其余部分，并且不想在调用代码中设置显式断点。

1. 若要继续运行程序直到下一个断点，请使用“继续”  (F5  )。 因为 `for` 循环中有断点，所以下一次迭代将中断。

1. 单步调试某个循环的数百次迭代是一个很枯燥的过程，因此，Visual Studio 允许用户对断点添加*条件*。 仅当满足该条件时，调试器才会在断点处暂停程序。 例如，可以对 `for` 语句上的断点使用条件，使其仅在 `i` 值超过 1600 时暂停。 若要设置此条件，请右键单击红色断点，选择“条件”  (Alt  +F9   > C  )。 在随即显示的“断点设置”  弹出窗口中，输入 `i > 1600` 作为表达式，选择“关闭”  。 按 F5  继续，注意程序在下一次中断前会运行多次迭代。

    ![设定断点条件](media/vs-getting-started-python-21-debugging4.png)

1. 若要一直运行程序直到结束，请右键单击边距中的点，并选择“禁用断点” (Ctrl+F9) 以禁用断点。 然后选择“继续”  （或按 F5  ）运行程序。 程序结束时，Visual Studio 会停止其调试会话，并恢复为其编辑模式。 请注意，要删除断点，还可以选择该点或右键单击该点并选择“删除断点”，但这也会删除已设置的所有条件。

> [!Tip]
> 在某些情况下，比如无法启动 Python 解释器自身，输出窗口可能短暂出现后就自动关闭，使用户没有机会查看任何错误消息。 如果出现这种情况，请在“解决方案资源管理器”  中右键单击项目，选择“属性”  ，选择“调试”  选项卡，然后将 `-i` 添加到“解释器参数”  字段。 此参数会使解释器在程序完成后进入交互模式，从而使窗口保持打开状态，直到按 Ctrl+Z > Enter 退出为止    。

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [在 Python 环境中安装程序包](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)

## <a name="go-deeper"></a>深入了解

- [调试](debugging-python-in-visual-studio.md)
- [在 Visual Studio 中调试](../debugger/debugger-feature-tour.md)提供了 Visual Studio 调试功能的完整文档。
