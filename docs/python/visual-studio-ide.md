---
title: 面向 Python 开发人员的 Visual Studio 概述
titleSuffix: ''
ms.date: 03/13/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
dev_langs:
- Python
ms.workload:
- python
- data-science
ms.openlocfilehash: 3b01d088618c07f1a3ff24aff2386584ebfad060
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72983683"
---
# <a name="welcome-to-the-visual-studio-ide--python"></a>欢迎使用 Visual Studio IDE | Python

Visual Studio“集成开发环境”是面向 Python （和其他语言）的创新启动板，可用于编辑、调试并生成代码，然后发布应用  。 集成开发环境 (IDE) 是一个功能丰富的程序，可用于软件开发的许多方面。 除了大多数 IDE 提供的标准编辑器和调试器之外，Visual Studio 还包括代码完成工具、交互式 REPL 环境以及其他功能，以简化软件开发过程。

[![带有 Python 项目的 Visual Studio](media/tour-ide-overview.png)](media/tour-ide-overview.png#lightbox)

此图像显示 Visual Studio 中含有一个打开的 Python 项目和若干重要的工具窗口：

- 可通过[解决方案资源管理器](../ide/solutions-and-projects-in-visual-studio.md)（右上方）查看、导航和管理代码文件  。 解决方案资源管理器可将代码文件分组为[解决方案和项目](/visualstudio/get-started/tutorial-projects-solutions)，从而帮助整理代码  。
  - 除“解决方案资源管理器”外，还有[“Python 环境”](managing-python-environments-in-visual-studio.md)，可在其中管理计算机上安装的不同 Python 解释器   。

  ::: moniker range=">=vs-2019"
  - 还可以打开并运行文件夹中的 Python 代码，而无需创建 Visual Studio 项目和解决方案文件。 有关详细信息，请参阅[快速入门：打开并运行文件夹中的 Python 代码](quickstart-05-python-visual-studio-open-folder.md)。
  ::: moniker-end

- [编辑器窗口](../ide/writing-code-in-the-code-and-text-editor.md)（中心）用于显示文件内容，你可能会在该窗口花费大部分时间。 这是[编辑 Python 代码](editing-python-code-in-visual-studio.md)、在代码结构中导航以及在调试会话期间设置断点的地方。 使用 Python，还可以选择代码并通过按 Ctrl+Enter 在[交互式 REPL 窗口](python-interactive-repl-in-visual-studio.md)中运行该代码。

- [“输出”窗口](../ide/reference/output-window.md)（底部中心）是 Visual Studio 发送通知（例如，调试和错误消息、警告、发布状态消息等）的位置。 每个消息源都有自己的选项卡。
  - [Python 交互式 REPL 窗口](python-interactive-repl-in-visual-studio.md)与输出窗口显示在同一区域中。

- 利用版本控制技术（如 [Git](https://git-scm.com/) 和 [Team Foundation 版本控制 (TFVC)](/azure/devops/repos/tfvc/overview?view=vsts)），[团队资源管理器](/azure/devops/user-guide/work-team-explorer?view=vsts)（右下方）可让你跟踪工作项并与他人共享代码。

## <a name="editions"></a>版本

Visual Studio 适用于 Windows 和 Mac；但仅对用于 Windows 的 Visual Studio 提供 Python 支持。

Windows 上有三个版本的 Visual Studio：社区版、专业版和企业版。 请参阅[比较 Visual Studio IDE](https://visualstudio.microsoft.com/vs/compare/)，了解各个版本支持哪些功能。

## <a name="popular-productivity-features"></a>高效性方面的常用功能

Visual Studio 中的一些常用功能可帮助你在开发软件时提高工作效率，这些功能包括：

- [IntelliSense](editing-python-code-in-visual-studio.md#intellisense)

   IntelliSense 由一组功能构成，它可用于在编辑器中直接显示代码相关信息，还能在某些情况下编写小段代码。 如同在编辑器中拥有了基本文档内联，从而节省了在其他位置查看类型信息的时间。 IntelliSense 功能因语言而异，[编辑 Python 代码](editing-python-code-in-visual-studio.md#intellisense)文章提供了有关 Python 的详细介绍。 下图显示了 IntelliSense 如何显示类型的成员列表：

   ![通过 Visual Studio IntelliSense 实现成员完成](media/code-editing-completions-simple.png)

- [重构](refactoring-python-code.md)

   通过右键单击一段代码并选择“快速操作和重构”，便可执行 Visual Studio 提供的一系列操作，例如智能重命名变量、将一个或多个代码行提取到新方法中、更改方法参数的顺序等操作  。

   ![在 Visual Studio 中重构](media/tour-ide-refactor-extract-method.png)

- [Linting](refactoring-python-code.md)

   Linting 检查 Python 代码中的错误和常见问题，鼓励使用好的 Python 编码模式。

   ![用于 Python 项目的上下文菜单上的 PyLint 命令](media/code-pylint-command.png)

- 搜索框

   visual Studio 有时会因为有如此多的菜单、选项和属性而让人不知所措。 使用搜索框可以在 Visual Studio 中快速找到所需内容。 开始键入要查找内容的名称时，Visual Studio 会列出结果，这些结果可以准确地将你导向目标位置。 如果需要向 Visual Studio 添加功能，例如添加对其他编程语言的支持，搜索框提供了打开 Visual Studio 安装程序以安装工作负载或单个组件的结果。

   ![Visual Studio 中的搜索框](media/tour-ide-quick-launch.png)

- 波形曲线和[快速操作](../ide/quick-actions.md)

   波形曲线是波浪形下划线，它可以在键入时对代码中的错误或潜在问题发出警报。 这些可视线索使你能立即修复问题，而无需等待在生成期间或运行程序时发现错误。 如果将鼠标悬停在波形曲线上，将看到关于此错误的其他信息。 左边距中也可能会出现一个灯泡，提供修复此错误的“快速操作”建议。

   ![Visual Studio 中的波形曲线](media/tour-ide-squiggles.png)

- [转到和速览定义](../ide/go-to-and-peek-definition.md)

   “转到定义”功能可将你直接带到定义函数或类型的位置  。 “速览定义”命令在窗口中显示定义而不打开单独的文件  。 “查找所有引用”命令还提供了一种有用的方法来发现不仅定义而且使用了给定标识符的位置  。

   ![代码导航命令](media/tour-ide-navigation-commands.png)

## <a name="powerful-features-for-python"></a>面向 Python 的强大功能

::: moniker range=">=vs-2019"
- [无项目运行代码](quickstart-05-python-visual-studio-open-folder.md)

    自 Visual Studio 2019 起，可以打开包含 Python 代码的文件夹，以使用 IntelliSense 和调试等功能，而无需为代码创建 Visual Studio 项目。
::: moniker-end

- [使用 Visual Studio 进行协作](/visualstudio/liveshare/use/vs)
  
    使用 Visual Studio Live Share，无论使用什么编程语言或要生成哪种类型的应用，均可以与他人实时协作进行编辑和调试。 

- [Python 交互式 REPL](python-interactive-repl-in-visual-studio.md)

    Visual Studio 为每个 Python 环境提供交互读取-评估-打印-循环 (REPL) 窗口，改进了在命令行中运行 python.exe  获得的 REPL。 在“交互式”窗口中，可以输入任意 Python 代码并查看即时结果  。

    ![Python 交互窗口](media/interactive-window.png)

- [调试](debugging-python-in-visual-studio.md)

    Visual Studio 提供全面的 Python 调试体验，包括附加到正在运行的进程，在监视窗口和即时窗口中计算表达式，检查局部变量、断点、单步执行/单步跳出/单步跳过语句、设置下一语句等    。 你还可以调试在 Linux 计算机上运行的远程 Python 代码。

    ![在 Visual Studio 中调试 Python](media/remote-debugging-breakpoint-hit.png)

- [与 C++ 交互](working-with-c-cpp-python-in-visual-studio.md)

    为 Python 创建的许多库都是用 C++ 编写的，旨在获得最佳性能。 Visual Studio 提供了丰富的用于开发 C++ 扩展的工具，包括[混合模式调试](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)。

    ![Python 和 C++ 混合模式调试](media/mixed-mode-debugging.png)

- [分析](profiling-python-code-in-visual-studio.md)

    使用基于 CPython 的解释器时，可以在 Visual Studio 中评估 Python 代码的性能。

    ![分析性能报告](media/profiling-results.png)

- [单元测试](unit-testing-python-in-visual-studio.md)

    Visual Studio 在 IDE 上下文中为单元测试的发现、运行和调试提供集成支持。

    ![测试状态显示为失败的单元测试](media/unit-test-A-fail.png)

## <a name="next-steps"></a>后续步骤

通过以下快速入门或教程之一，进一步探索 Visual Studio 中的 Python：

> [!div class="nextstepaction"]
> [快速入门：通过 Flask 创建 Web 应用](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json)

> [!div class="nextstepaction"]
> [在 Visual Studio 中使用 Python](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

> [!div class="nextstepaction"]
> [Visual Studio 中的 Django Web 框架入门](learn-django-in-visual-studio-step-01-project-and-solution.md)

> [!div class="nextstepaction"]
> [在 Visual Studio 中开始使用 Flask Web 框架](learn-flask-visual-studio-step-01-project-solution.md)

## <a name="see-also"></a>请参阅

- 发现[更多 Visual Studio 功能](../ide/advanced-feature-overview.md)
- 访问 [visualstudio.microsoft.com](https://visualstudio.microsoft.com/vs/)
- 阅读 [Visual Studio 博客](https://devblogs.microsoft.com/visualstudio/)
