---
title: Visual Studio 中的 Python 教程步骤 2，编写和运行代码
titleSuffix: ''
description: 在 Visual Studio 中使用 Python 功能的核心教程的第 2 步，包括编辑代码和运行项目。
ms.date: 01/28/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: fda68b9e5bffbd1afab3389a0d8d624312a8de3f
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "62429999"
---
# <a name="step-2-write-and-run-code"></a>步骤 2：编写并运行代码

**上一步：[创建新的 Python 项目](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)**

虽然可以在解决方案资源管理器中管理项目文件，但处理文件内容（如源代码）通常还是在编辑器窗口进行。 编辑器根据上下文识别正在编辑的文件类型，其中包括编程语言（基于文件扩展名），并使用 IntelliSense 提供适合该语言的功能，比如语法着色和自动完成。

1. 创建新的“Python 应用程序”项目后，名为 PythonApplication1.py  的默认空文件将在 Visual Studio 编辑器中打开。

1. 在编辑器中，开始键入 `print("Hello, Visual Studio")`，注意 Visual Studio IntelliSense 如何在此过程中显示自动完成选项。 下拉列表中加外边框的选项是按 Tab  键时使用的默认完成选项。 涉及到较长的语句或标识符时，最适合使用“完成”。

    ![IntelliSense 自动完成弹出窗口](media/vs-getting-started-python-04-IntelliSense1b.png)

1. IntelliSense 根据正在使用的语句、正在调用的函数等显示不同的信息。 使用 `print` 函数时，在 `print` 后面键入 `(` 表示函数调用将显示该函数的完整使用情况信息。 IntelliSense 弹出窗口还用粗体显示当前参数（如此处所示的 **value**）：

    ![某函数的 IntelliSense 自动完成弹出窗口](media/vs-getting-started-python-05-IntelliSense2b.png)

1. 完成该语句，使其与以下内容匹配：

    ```python
    print("Hello, Visual Studio")
    ```

1. 注意语法着色如何区分 `print` 语句与 `"Hello Visual Studio"` 参数。 另外，暂时删除字符串上的最后一个 `"`，并注意 Visual Studio 如何在包含语法错误的代码下方显示一条红色下划线。 然后，替换 `"` 以更正此代码。

    ![IntelliSense 语法着色和错误突出显示](media/vs-getting-started-python-06-IntelliSense3b.png)

    > [!Tip]
    > 由于一个人的开发环境是件非常私人的事情，因此，Visual Studio 允许用户完全控制 Visual Studio 的外观和行为。 选择“工具”   > “选项”  菜单命令，浏览“环境”  和“文本编辑器”  选项卡下面的设置。 默认情况下仅显示部分选项；若要查看每种编程语言的每个选项，请选择对话框底部的“显示所有设置”  。

1. 按 Ctrl  +F5  或选择“调试”   > “开始执行(不调试)”  菜单项，运行到目前为止编写的代码。 如果代码中仍然存在错误，Visual Studio 会发出警告。

1. 运行程序时，会出现一个显示结果的控制台窗口，就像从命令行使用 PythonApplication1.py  运行 Python 解释器一样。 按键关闭窗口，返回到 Visual Studio 编辑器。

    ![首次运行程序时的输出](media/vs-getting-started-python-07-output.png)

1. 除了完成语句和函数外，IntelliSense 还提供 Python `import` 和 `from` 语句的完成。 这些完成有助于轻松发现环境中可用的模块以及这些模块的成员。 在编辑器中，删除 `print` 行，开始键入 `import`。 键入空格时会显示模块列表：

    ![显示 import 语句的可用模块的 IntellSense](media/vs-getting-started-python-08-import1.png)

1. 通过键入或选择 `sys` 完成行。

1. 在下一行中，键入 `from` 再次查看模块列表：

    ![显示 from 语句的可用模块的 IntellSense](media/vs-getting-started-python-09-import2.png)

1. 选择或键入 `math`，然后继续键入一个空格和 `import`，将显示模块成员：

    ![显示模块成员的 IntellSense](media/vs-getting-started-python-10-import3.png)

1. 通过导入 `sin`、`cos` 和 `radians` 成员完成，注意自动完成可用于每个成员。 完成后，代码应如下所示：

    ```python
    import sys
    from math import cos, radians
    ```

    > [!Tip]
    > 完成可处理键入时的子字符串，匹配单词的某些部分、单词开头的字母，甚至是跳过的字符。 请参阅[编辑代码 - 完成](editing-python-code-in-visual-studio.md#completions)，了解详细信息。

1. 再添加一小段代码以输出 360 度的余弦值：

    ```python
    for i in range(360):
        print(cos(radians(i)))
    ```

1. 使用 Ctrl  +F5  或“调试”   > “开始执行(不调试)”  再次运行程序。 完成后，关闭输出窗口。

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [使用交互 REPL 窗口](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md)

## <a name="go-deeper"></a>深入了解

- [编辑代码](editing-python-code-in-visual-studio.md)
- [格式代码](formatting-python-code.md)
- [重构代码](refactoring-python-code.md)
- [使用 PyLint](linting-python-code.md)
