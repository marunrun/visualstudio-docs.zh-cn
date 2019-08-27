---
title: Windows 上 Visual Studio 中的 Python 支持
titleSuffix: ''
description: Visual Studio 中的 Python 功能摘要，这些功能让 Visual Studio 成为 Windows 上卓越的 Python IDE（也称为针对 Visual Studio 的 Python 工具，PTVS）。
ms.date: 06/05/2019
ms.topic: overview
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: c137b6bd8a38ac606a547ce961c4f040e60c6d87
ms.sourcegitcommit: 9753c7544cec852ca5efd0834e0956d9e53a5734
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "67043361"
---
# <a name="work-with-python-in-visual-studio-on-windows"></a>在 Windows 上的 Visual Studio 中使用 Python

Python 是一种受欢迎的编程语言，它可靠、灵活、易于学习、可在所有操作系统上免费使用，并且强大的开发人员社区和很多免费库都支持它。 Python 支持所有开发方式，包括 Web 应用程序、Web 服务、桌面应用、脚本编写和科学计算，许多高校人员、科学家、业余和专业开发人员都在使用 Python。 可以在 [python.org](https://www.python.org) 和 [Python for Beginners](https://www.python.org/about/gettingstarted/)（面向初学者的 Python）中了解有关该语言的详细信息。

Visual Studio 是 Windows 上功能强大的 Python IDE。 Visual Studio 通过 Python 开发  和数据科学  工作负载（Visual Studio 2017 及更高版本）和免费的针对 Visual Studio 的 Python 工具扩展（Visual Studio 2015 及更早版本），为 Python 语言提供[开源代码](https://github.com/Microsoft/ptvs)支持。

Python 目前不支持在 Visual Studio for Mac 中使用，但可通过 Visual Studio Code 在 Mac 和 Linux 上使用（请参阅[问题和解答](#questions-and-answers)）。

若要开始使用 Python，请执行以下操作：

- 按照[安装说明](installing-python-support-in-visual-studio.md)安装 Python 工作负载。
- 通过本文中各部分的内容熟悉 Visual Studio 的 Python 功能。
::: moniker range="vs-2017"
- 阅读一个或多个指导如何创建项目的快速入门教程。 如果不确定，可先从[通过 Flask 创建 Web 应用](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json)开始。
::: moniker-end
::: moniker range=">=vs-2019"
- 阅读一个或多个指导如何创建项目的快速入门教程。 如果不确定，请从[快速入门：打开并运行文件夹中的 Python 代码](quickstart-05-python-visual-studio-open-folder.md)或[使用 Flask 创建 Web 应用](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json)开始。
::: moniker-end
- 按照[在 Visual Studio 中使用 Python](tutorial-working-with-python-in-visual-studio-step-01-create-project.md) 教程操作，获得完整的端到端体验。

::: moniker range=">=vs-2019"
> [!Note]
> Visual Studio 支持 Python 版本 2.7 以及版本 3.5 和更高版本。 可以使用 Visual Studio 编辑在 Python 其他版本中编写的代码时，这些版本不受官方支持，IntelliSense 和调试等功能可能无法正常工作。
::: moniker-end

## <a name="support-for-multiple-interpreters"></a>对多个解释器的支持

Visual Studio 的“Python 环境”窗口（下方为其扩展后的加宽视图）具有一块用于管理所有全局 Python 环境、conda 环境和虚拟环境的单独区域  。 Visual Studio 可自动检测出标准位置是否安装 Python，并且允许用户配置自定义安装。 在每个环境中，用户都可以轻松管理包、打开该环境的交互窗口和访问环境文件夹。

::: moniker range="vs-2017"
![“Python 环境”窗口扩展后的视图](media/environments/environments-expanded-view.png)
::: moniker-end
::: moniker range=">=vs-2019"
![“Python 环境”窗口扩展后的视图](media/environments/environments-expanded-view-2019.png)
::: moniker-end

使用“打开交互窗口”  命令，在 Visual Studio 的上下文中以交互方式运行 Python。 使用“在 PowerShell 中打开”  命令，在所选环境的文件夹中打开单独的命令窗口。 可从该命令窗口运行任何 python 脚本。

更多相关信息：

- [管理 Python 环境](managing-python-environments-in-visual-studio.md)
- [“Python 环境”引用](python-environments-window-tab-reference.md)

## <a name="rich-editing-intellisense-and-code-comprehension"></a>多种多样的编辑、IntelliSense 和代码理解

Visual Studio 具备出色的 Python 编辑器，包括语法着色、跨代码和库的自动补全、代码格式设置、签名帮助、重构、Linting 和类型提示。 Visual Studio 还提供一些独一无二的功能，如类视图、转到定义  、查找所有引用  和代码片段。 与[交互窗口](#interactive-window)直接集成有助于快速开发已保存在文件中的 Python 代码。

![Visual Studio 中 Python 代码的代码补全](media/code-editing-completions-simple.png)

更多相关信息：

- 文档：[编辑 Python 代码](editing-python-code-in-visual-studio.md)
- 文档：[格式代码](formatting-python-code.md)
- 文档：[重构代码](refactoring-python-code.md)
- 文档：[使用 Linter](linting-python-code.md)
- 常规 Visual Studio 功能文档：[代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)

## <a name="interactive-window"></a>交互窗口

对于 Visual Studio 已知的每个 Python 环境，用户都可以直接在 Visual Studio 中轻松打开 Python 解释器的相同交互 (REPL) 环境，而无需使用单独的命令提示符。 也可以轻松地切换环境。 （若要打开单独的命令提示符，请在“Python环境”窗口中选择所需的环境，然后如之前的[对多个解释器的支持](#support-for-multiple-interpreters)下所述，选择“在 PowerShell 中打开”命令）   。

![Visual Studio 中的 Python 交互窗口](media/interactive-window.png)

Visual Studio 还紧密集成了 Python 代码编辑器和交互  窗口。 使用 Ctrl  +Enter  键盘快捷方式可将编辑器中的当前代码行（或代码块）发送给交互  窗口，然后移至下一行（或块），非常方便。 使用  +Enter  无需运行调试程序即可轻松浏览代码。 还可以使用相同的键盘快捷方式将选定代码发送给交互  窗口，并轻松地将交互  窗口中的代码粘贴到编辑器中。 将这些功能结合使用可以在交互  窗口中找出代码段的详细信息，并将结果轻松保存到编辑器的文件中。

Visual Studio 还支持 REPL 中的 IPython/Jupyter，包括内联图、.NET 和 Windows Presentation Foundation (WPF)。

更多相关信息：

- [交互窗口](python-interactive-repl-in-visual-studio.md)
- [Visual Studio 中的 IPython](interactive-repl-ipython.md)

## <a name="project-system-and-project-and-item-templates"></a>项目系统、项目模板和项模板

::: moniker range=">=vs-2019"
> [!Note]
> Visual Studio 2019 支持打开包含 Python 代码的文件夹并在不创建 Visual Studio 项目和解决方案文件的情况下运行该代码。 有关详细信息，请参阅[快速入门：打开并运行文件夹中的 Python 代码](quickstart-05-python-visual-studio-open-folder.md)。 但是，使用项目文件会获得本部分所述的优势。
::: moniker-end

Visual Studio 可帮助管理项目随时间增加的复杂性。  Visual Studio 项目不仅仅是一个文件夹结构：它包括理解不同文件的使用方式以及文件之间的关系。 Visual Studio 可帮助用户区分应用代码、测试代码、网页、JavaScript 和生成脚本等，从而启用文件对应的功能。 此外，Visual Studio 解决方案还可以帮助用户管理多个相关的项目，例如 Python 项目和 C++ 扩展项目。

![一个同时包含 Python 和 C++ 项目的 Visual Studio 解决方案](media/projects-solution-explorer-two-projects.png)

项目和项模板可自动完成不同类型的项目和文件的设置过程，能为用户节省宝贵的时间，无需用户管理错综复杂又容易出错的细枝末节。 Visual Studio 提供适用于 Web、Azure、数据科学、控制台和其他类型项目的模板，以及适用于 Python 类、单元测试、Azure Web 配置、HTML 甚至 Django 应用等文件的模板。

[![Visual Studio 中的 Python 项目和项模板](media/project-and-item-templates.png)](media/project-and-item-templates.png#lightbox)

更多相关信息：

- 文档：[管理 Python 项目](managing-python-projects-in-visual-studio.md)
- 文档：[项模板引用](python-item-templates.md)
- 文档：[Python 项目模板](managing-python-projects-in-visual-studio.md#project-templates)
- 文档：[使用 C++ 和 Python](working-with-c-cpp-python-in-visual-studio.md)
- 常规 Visual Studio 功能文档：[项目和项模板](../ide/creating-project-and-item-templates.md#visual-studio-templates)
- 常规 Visual Studio 功能文档：[Visual Studio 中的解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)

## <a name="full-featured-debugging"></a>功能完备的调试

功能强大的调试程序是 Visual Studio 的优势之一。 特别以 Python 为例，Visual Studio 支持 Python/C++ 混合模式调试、在 Linux 上进行远程调试、在交互  窗口中进行调试，以及调试 Python 单元测试。

![显示了一个异常弹出窗口的用于 Python 的 Visual Studio 调试程序](media/debugging-exception-popup.png)

::: moniker range=">=vs-2019"
在 Visual Studio 2019 中，可以在不使用 Visual Studio 项目文件的情况下运行和调试代码。 请参阅[快速入门：打开并运行文件夹中的 Python 代码](quickstart-05-python-visual-studio-open-folder.md)，查看有关示例。
::: moniker-end

更多相关信息：

- 文档：[调试 Python](debugging-python-in-visual-studio.md)
- 文档：[Python/C++ 混合模式调试](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)
- 文档：[在 Linux 上进行远程调试](debugging-python-code-on-remote-linux-machines.md)
- 常规 Visual Studio 功能文档：[Visual Studio 调试器功能导览](../debugger/debugger-feature-tour.md)

## <a name="profiling-tools-with-comprehensive-reporting"></a>具有丰富报表的分析工具

通过分析可以了解应用程序内的时间分配。 Visual Studio 支持使用基于 CPython 的解释器进行分析，并且能比较运行的不同分析之间的性能差异。

[![Visual Studio 探查器处理 Python 项目的结果](media/profiling-results.png)](media/profiling-results.png#lightbox)

更多相关信息：

- 文档：[Python 分析工具](profiling-python-code-in-visual-studio.md)
- 常规 Visual Studio 功能文档：[分析功能导览](../profiling/profiling-feature-tour.md)。 （并非所有 Visual Studio 分析功能都可用于 Python）。

## <a name="unit-testing-tools"></a>单元测试工具

在 Visual Studio 测试资源管理器  中发现、运行和管理测试，并且可轻松调试单元测试。

![在 Visual Studio 中调试 Python 单元测试](media/unit-test-debugging.png)

更多相关信息：

- 文档：[Python 的单元测试工具](unit-testing-python-in-visual-studio.md)
- 常规 Visual Studio 功能文档：[对代码进行单元测试](../test/unit-test-your-code.md)。

## <a name="azure-sdk-for-python"></a>Azure SDK for Python

用于 Python 的 Azure 库简化了从 Windows、Mac OS X 和 Linux 应用中使用 Azure 服务的过程。 可以使用它们创建和管理 Azure 资源，以及连接到 Azure 服务。 

有关详细信息，请参阅 [Azure SDK for Python](/python/azure/?view=azure-python) 和[用于 Python 的 Azure 库](/python/azure/python-sdk-azure-overview?view=azure-python)。

## <a name="questions-and-answers"></a>问题和解答

**问：是否可通过 Visual Studio for Mac 获得 Python 支持？**

答： 目前不行，但你可以在[开发者社区](https://developercommunity.visualstudio.com/content/idea/351820/python-tools-for-visual-studio-mac.html)上为该请求投票。 [Visual Studio for Mac](/visualstudio/mac/) 文档会标识当前支持的开发类型。 同时，Windows、Mac 和 Linux 上的 Visual Studio Code 可[通过可用扩展与 Python 配合工作](https://code.visualstudio.com/docs/languages/python)。

**问：构建 Python UI 可以使用什么工具？**

答： 该领域的主要产品是 [Qt 项目](https://www.qt.io/qt-for-application-development/)，其中与 Python 的绑定称为 [PySide（官方绑定）](https://wiki.qt.io/PySide)（另请参阅 [PySide 下载](https://download.qt.io/official_releases/pyside/.)）和 [PyQt](https://wiki.python.org/moin/PyQt)。 目前，Visual Studio 中的 Python 支持不包括用于 UI 开发的任何特定工具。

**问：Python 项目是否可以生成独立的可执行文件？**

答： Python 通常是一种解释型语言，其代码在适合 Python 功能的环境（如 Visual Studio 和 Web 服务器）中按需运行。 目前，Visual Studio 本身不提供创建独立可执行文件的方法，它本质上是一个具有嵌入式 Python 解释器的程序。 但是，如 [StackOverflow](https://stackoverflow.com/questions/5458048/how-to-make-a-python-script-standalone-executable-to-run-without-any-dependency) 所述，Python 社区提供了不同的方法来创建可执行文件。 如博客文章[使用 CPython 可嵌入 zip 文件](https://devblogs.microsoft.com/python/cpython-embeddable-zip-file/)中所述，CPython 还支持嵌入到本机应用程序中。

::: moniker range="<=vs-2017"

## <a name="feature-support"></a>功能支持

如[安装指南](installing-python-support-in-visual-studio.md)所述，可在下述 Visual Studio 版本中安装 Python 功能：

- [Visual Studio 2019（所有版本）](https://visualstudio.microsoft.com/vs/)
- Visual Studio 2017（所有版本）
- Visual Studio 2015（所有版本）
- Visual Studio 2013 Community Edition
- Visual Studio 2013 Express for Web 和 Update 2 或更高版本
- Visual Studio 2013 Express for Desktop 和 Update 2 或更高版本
- Visual Studio 2013（Pro 或更高版本）
- Visual Studio 2012（Pro 或更高版本）
- Visual Studio 2010 SP1（Pro 或更高版本；需要 .NET 4.5）

Visual Studio 2015 及更早版本可在 [visualstudio.microsoft.com/vs/older-downloads/](https://visualstudio.microsoft.com/vs/older-downloads/) 处获取。

> [!Important]
> 仅针对 Visual Studio 的最新版完全支持和维护这些功能。 可在早期版本中使用这些功能，但不主动维护它们。

|          Python 支持          |   2017+   |   2015   | 2013 Comm | 2013 Desktop | 2013 Web | 2013 Pro+ | 2012 Pro+ | 2010 SP1 Pro+ |
|----------------------------------|----------|----------|-----------|--------------|----------|-----------|-----------|---------------|
|   管理多个解释器   | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
| 自动检测热门解释器 | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|     添加自定义解释器      | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|       虚拟环境       | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|         Pip/易于安装         | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |

<br/>

|         项目系统         |   2017+   |   2015   | 2013 Comm | 2013 Desktop | 2013 Web | 2013 Pro+ |      2012 Pro+       | 2010 SP1 Pro+ |
|--------------------------------|----------|----------|-----------|--------------|----------|-----------|----------------------|---------------|
| 根据现有代码新建项目 | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  |       &#10004;       |   &#10004;    |
|         显示所有文件         | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  |       &#10004;       |   &#10004;    |
|         源代码管理         | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  |       &#10004;       |   &#10004;    |
|        Git 集成         | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;<sup>1</sup> |   &#10007;    |

<br/>

|           编辑            |   2017+   |   2015   | 2013 Comm | 2013 Desktop | 2013 Web | 2013 Pro+ | 2012 Pro+ | 2010 SP1 Pro+ |
|------------------------------|----------|----------|-----------|--------------|----------|-----------|-----------|---------------|
|     语法突出显示      | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|        自动完成         | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|        签名帮助        | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|          快速信息          | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|  对象浏览器/类视图   | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|        导航栏        | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|       转到定义       | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|         导航到          | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|     查找所有引用      | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|       自动缩进       | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|       代码格式设置        | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|      重构 - 重命名       | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|  重构 - 提取方法   | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
| 重构 - 添加/删除导入 | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|            PyLint            | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |

<br/>

|     交互窗口     |   2017+   |   2015   | 2013 Comm | 2013 Desktop | 2013 Web | 2013 Pro+ | 2012 Pro+ | 2010 SP1 Pro+ |
|----------------------------|----------|----------|-----------|--------------|----------|-----------|-----------|---------------|
|     交互窗口     | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
| 具有内联关系图的 IPython | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |

<br/>

|               桌面               |   2017+   |   2015   | 2013 Comm | 2013 Desktop | 2013 Web | 2013 Pro+ | 2012 Pro+ | 2010 SP1 Pro+ |
|-------------------------------------|----------|----------|-----------|--------------|----------|-----------|-----------|---------------|
|     控制台/Windows 应用程序     | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
| IronPython WPF（带 XAML 设计器） | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|      IronPython Windows 窗体       | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |

<br/>

|         Web         |   2017+   |   2015   | 2013 Comm | 2013 Desktop | 2013 Web | 2013 Pro+ | 2012 Pro+ | 2010 SP1 Pro+ |
|---------------------|----------|----------|-----------|--------------|----------|-----------|-----------|---------------|
| Django Web 项目  | &#10004; | &#10004; | &#10004;  |   &#10007;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
| Bottle Web 项目  | &#10004; | &#10004; | &#10004;  |   &#10007;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|  Flask Web 项目  | &#10004; | &#10004; | &#10004;  |   &#10007;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
| Generic Web 项目 | &#10004; | &#10004; | &#10004;  |   &#10007;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |

<br/>

|         Azure          |   2017+   |   2015   | 2013 Comm | 2013 Desktop |       2013 Web       |      2013 Pro+       |      2012 Pro+       |    2010 SP1 Pro+     |
|------------------------|----------|----------|-----------|--------------|----------------------|----------------------|----------------------|----------------------|
|   对网站的部署   | &#10004; | &#10004; | &#10004;  |   &#10007;   |       &#10004;       |       &#10004;       |       &#10004;       | &#10004;<sup>2</sup> |
|   对 Web 角色的部署   | &#10004; | &#10004; | &#10004;  |   &#10007;   | &#10004;<sup>4</sup> | &#10004;<sup>4</sup> | &#10004;<sup>3</sup> |       &#10007;       |
| 对辅助角色的部署  |    ?     |    ?     |     ?     |   &#10007;   | &#10004;<sup>4</sup> | &#10004;<sup>4</sup> | &#10004;<sup>3</sup> |       &#10007;       |
| 在 Azure 仿真程序中运行  |    ?     |    ?     |     ?     |   &#10007;   | &#10004;<sup>4</sup> | &#10004;<sup>4</sup> | &#10004;<sup>3</sup> |       &#10007;       |
|    远程调试    | &#10004; | &#10004; | &#10004;  |   &#10007;   | &#10004;<sup>6</sup> | &#10004;<sup>8</sup> | &#10004;<sup>8</sup> |       &#10007;       |
| 附加服务器资源管理器 | &#10004; | &#10004; | &#10004;  |   &#10007;   | &#10004;<sup>7</sup> | &#10004;<sup>7</sup> |       &#10007;       |       &#10007;       |

<br/>

|           Django 模板           |   2017+   |   2015   | 2013 Comm | 2013 Desktop |       2013 Web       |      2013 Pro+       | 2012 Pro+ | 2010 SP1 Pro+ |
|--------------------------------------|----------|----------|-----------|--------------|----------------------|----------------------|-----------|---------------|
|              调试               | &#10004; | &#10004; | &#10004;  |   &#10007;   |       &#10004;       |       &#10004;       | &#10004;  |   &#10004;    |
|            自动完成             | &#10004; | &#10004; | &#10004;  |   &#10007;   | &#10004;<sup>5</sup> | &#10004;<sup>5</sup> | &#10004;  |   &#10004;    |
| CSS 和 JavaScript 的自动完成 | &#10004; | &#10004; | &#10004;  |   &#10007;   | &#10004;<sup>5</sup> | &#10004;<sup>5</sup> | &#10007;  |   &#10007;    |

<br/>

|                  调试                  |   2017+   |   2015   | 2013 Comm | 2013 Desktop | 2013 Web | 2013 Pro+ | 2012 Pro+ | 2010 SP1 Pro+ |
|---------------------------------------------|----------|----------|-----------|--------------|----------|-----------|-----------|---------------|
|                  调试                  | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|         不含项目进行调试         | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |
|        调试 - 附加到编辑        | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10007; | &#10004;  | &#10004;  |   &#10004;    |
|            混合模式调试             | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10007;    |
| 远程调试（Windows、Mac OS X、Linux） | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10007; | &#10004;  | &#10004;  |   &#10004;    |
|          调试交互窗口           | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10004;    |

<br/>

<a name="matrix-profiling"></a>

| 分析 |   2017+   |   2015   | 2013 Comm | 2013 Desktop | 2013 Web | 2013 Pro+ | 2012 Pro+ | 2010 SP1 Pro+ |
|-----------|----------|----------|-----------|--------------|----------|-----------|-----------|---------------|
| 分析 | &#10004; | &#10004; | &#10004;  |   &#10007;   | &#10007; | &#10004;  | &#10004;  |   &#10004;    |

<br/>

|     测试      |   2017+   |   2015   | 2013 Comm | 2013 Desktop | 2013 Web | 2013 Pro+ | 2012 Pro+ | 2010 SP1 Pro+ |
|---------------|----------|----------|-----------|--------------|----------|-----------|-----------|---------------|
| 测试资源管理器 | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10007;    |
|   运行测试    | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10007;    |
|  调试测试   | &#10004; | &#10004; | &#10004;  |   &#10004;   | &#10004; | &#10004;  | &#10004;  |   &#10007;    |

<br/>

1. Visual Studio Tools for Git 扩展中提供了对 Visual Studio 2012 的 Git 支持，可从 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TFSPowerToolsTeam.VisualStudioToolsforGit) 中获得。

1. 部署到 Azure 网站需要 [Azure SDK for .NET 2.1 - Visual Studio 2010 SP1](https://go.microsoft.com/fwlink/?LinkId=313855)。 更高版本不支持 Visual Studio 2010。

1. 对 Azure Web 角色和辅助角色的支持需要[用于 .NET 2.3 - VS 2012 的 Azure SDK](https://go.microsoft.com/fwlink/?LinkId=323511) 或更高版本。

1. 对 Azure Web 角色和辅助角色的支持需要[用于 .NET 2.3 - VS 2013 的 Azure SDK](https://go.microsoft.com/fwlink/?LinkId=323510) 或更高版本。

1. Visual Studio 2013 中的 Django 模板编辑器具有一些已知问题，可通过安装 Update 2 解决。

1. 需要 Windows 8 或更高版本。 Visual Studio 2013 Express for Web 没有“附加到进程”  对话框，但 Azure 网站远程调试仍然可能在服务器资源管理器  中使用附加调试器 (Python)  命令。 远程调试需要安装 [Azure SDK for .NET 2.3 - Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=323510) 或更高版本。

1. 需要 Windows 8 或更高版本。 使用服务器资源管理器  中的附加调试器 (Python)  命令需要 [Azure SDK for .NET 2.3 - Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=323510) 或更高版本。

1. 需要 Windows 8 或更高版本。
::: moniker-end
