---
title: Visual Studio 中的 Python 教程步骤 3，交互式 REPL
titleSuffix: ''
description: 在 Visual Studio 中使用 Python 功能的核心教程的第 3 步，介绍了 Python 交互式 REPL 窗口。
ms.date: 01/28/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 15e0b45fd77096ba2227391736aad5c895014d1c
ms.sourcegitcommit: 0554b59a2a251661e56824fb9cd6e9b1f326cef1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2019
ms.locfileid: "71831875"
---
# <a name="step-3-use-the-interactive-repl-window"></a>步骤 3：使用交互式 REPL 窗口

**上一步：[编写并运行代码](tutorial-working-with-python-in-visual-studio-step-02-writing-code.md)**

适用于 Python 的 Visual Studio 交互窗口  提供丰富的“读取–求值–打印-循环”(REPL) 体验，极大地缩短了常用的“编辑-生成-调试”周期。 该交互  窗口提供 Python 命令行 REPL 体验的所有功能。 通过该窗口还可以非常轻松地与 Visual Studio 编辑器中的源文件交换代码，免去了使用命令行时的繁琐操作。

> [!NOTE]
> 对于 REPL 问题，请确保已安装 `ipython` 和 `ipykernel` 包，为了帮助安装包，请参阅 [Python 环境包选项卡](https://docs.microsoft.com/en-us/visualstudio/python/python-environments-window-tab-reference#packages-tab)。

1. 通过以下方式打开交互  窗口：在“解决方案资源管理器”  中右键单击项目的 Python 环境（比如先前图片中显示的“Python 3.6（32 位）”  ），选择“打开交互窗口”  。 也可以从 Visual Studio 主菜单选择“视图”   > “其他窗口”   > “Python 交互窗口”  。

1. 交互  窗口在编辑器下方打开，其中显示标准的 **>>>** Python REPL 提示符。 可通过“环境”  下拉列表选择要使用的特定解释器。 通常还会想要放大交互  窗口，这一点可通过拖动两个窗口之间的分隔条实现：

    ![Python 交互窗口以及通过拖动重设大小](media/vs-getting-started-python-11-interactive1b.png)

    > [!Tip]
    > 可通过拖动边界分隔条重设 Visual Studio 中所有窗口的大小。 还可以将窗口拖出 Visual Studio 框架，以及在框架内按喜欢的方式重新排列窗口。 有关完整的详细信息，请参阅[自定义窗口布局](../ide/customizing-window-layouts-in-visual-studio.md)。

1. 输入几个语句（如 `print("Hello, Visual Studio")`）和表达式（如 `123/456`）以查看即时结果：

    ![Python 交互窗口即时结果](media/vs-getting-started-python-12-interactive2.png)

1. 开始编写多行语句（如函数定义）时，交互  窗口将针对后续行显示 Python 的 ...  提示符，它与命令行 REPL 不同，可以提供自动缩进：

    ![含语句后续符的 Python 交互窗口](media/vs-getting-started-python-13-interactive3.png)

1. 交互  窗口提供所有已输入内容的完整历史记录，并通过多行历史记录项改进了命令行 REPL。 例如，可以轻松地将 `f` 函数的整个定义重新调用为单个单元，并轻松地将名称更改为 `make_double`，而不用逐行重新创建函数。

1. Visual Studio 可从编辑器窗口向交互  窗口发送多行代码。 此功能可用于维护源文件中的代码并将其选定部分轻松发送到交互  窗口。 然后就可以在快速 REPL 环境中使用此类代码片段，而不必运行整个程序。 若要查看此功能，应先将 PythonApplication1.py  文件中的 `for` 循环替换为以下代码：

    ```python
    # Create a string with spaces proportional to a cosine of x in degrees
    def make_dot_string(x):
        return ' ' * int(20 * cos(radians(x)) + 20) + 'o'
    ```

1. 选择 .py 文件中的 `import`、`from` 和 `make_dot_string` 函数语句，单击鼠标右键，选择“发送到交互窗口”（或按 Ctrl+Enter）     。 代码片段会立即粘贴至交互  窗口并运行。 现在选择 `make_dot_string` 函数，重复相同的命令，即再次运行该代码片段。 由于代码定义了一个函数，因此可通过数次调用它来快速测试该函数：

    ![将代码发送到交互窗口并测试它](media/vs-getting-started-python-14-interactive4.png)

    > [!Tip]
    > 如果在未  选择任何内容的情况下，在编辑器中使用 Ctrl  +Enter  ，则会在交互  窗口中运行当前代码行，并自动在下一行放置插入点。 利用此功能，通过反复按 Ctrl  +Enter  即可便捷地单步调试代码，仅使用 Python 命令行则无法做到这一点。 它还允许在不运行调试器的情况下单步调试代码，而且不必从头开始启动程序。

1. 还可以将任何源中的多行代码复制并粘贴到交互  窗口，比如下面的代码片段，使用 Python 命令行 REPL 则难以实现此操作。 粘贴后，交互  窗口会运行该代码，就像直接在窗口中键入的一样：

    ```python
    for i in range(360):
        s = make_dot_string(i)
        print(s)
    ```

    ![使用“发送到交互窗口”粘贴多行代码](media/vs-getting-started-python-15-interactive5.png)

1. 如用户所见，此代码运行正常，但其输出不太乐观。 `for` 循环中的另一个单步执行值会显示更多余弦波。 幸运的是，由于整个 `for` 循环在 REPL 历史记录中作为单个单元，因此可轻易返回并进行任何所需的更改，然后再次测试函数。 按向上键先重新调用 `for` 循环。 然后按向左键或向右键开始在代码中导航（在执行此操作前，向上键和向下键继续循环访问历史记录）。 导航到 `range` 规范并将其更改为 `range(0, 360, 12)`。 然后按 Ctrl  +Enter  （在代码中的任意位置）再次运行整个语句：

    ![在交互窗口中编辑以前的语句](media/vs-getting-started-python-16-interactive6.png)

1. 反复尝试使用不同的单步执行设置，直到找到最喜欢的值。 也可以延长范围（例如 `range(0, 1800, 12)`）使波形重复。

1. 如果对在交互  窗口中编写的代码感到满意，可选择代码，单击右键，选择“复制代码”  (Ctrl  +Shift  +C  )，然后粘贴到编辑器中。 注意 Visual Studio 的这一特殊功能如何自动省略所有输出以及 `>>>` 和 `...` 提示符。 例如，下图演示如何对包含提示符和输出的选定内容使用“复制代码”  命令：

    ![交互窗口中用于包含提示符和输出的选定内容的“复制代码”命令](media/vs-getting-started-python-17-interactive7.png)

    粘贴到编辑器时，仅得到以下代码：

    ```python
    for i in range(0, 1800, 12):
        s = make_dot_string(i)
        print(s)
    ```

    若想复制交互  窗口的准确内容，包括提示符和输出，只需使用标准的“复制”  命令。

1. 刚刚已经了解如何使用交互  窗口的快速 REPL 环境处理一小段代码的细节问题，然后将该代码轻松添加到项目的源文件。 如果现在使用 Ctrl  +F5  （或“调试”   > “启动而不调试”**Start without Debugging**）再次运行代码，则会看到想要的准确结果。

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [在调试器中运行代码](tutorial-working-with-python-in-visual-studio-step-04-debugging.md)

## <a name="go-deeper"></a>深入了解

- [使用交互窗口](python-interactive-repl-in-visual-studio.md)
- [使用 IPython REPL](interactive-repl-ipython.md)
