---
title: Visual Studio 中的 Python 教程步骤 1，创建项目
titleSuffix: ''
description: 在 Visual Studio 中使用 Python 功能的核心教程概述和第 1 步，包括系统必备组件和创建新的 Python 项目。
ms.date: 01/28/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: ed4fdbfe7090a66d955461f2c3a394f6fb661c5a
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "62430701"
---
# <a name="tutorial-work-with-python-in-visual-studio"></a>教程：在 Visual Studio 中使用 Python

Python 是一种受欢迎的编程语言，它可靠、灵活、易于学习、可在所有操作系统上免费使用，并且强大的开发人员社区和很多免费库都支持它。 该语言支持所有开发方式，包括 Web 应用程序、Web 服务、桌面应用、脚本编写和科学计算，许多高校人员、科学家、业余和专业开发人员都在使用 Python。

Visual Studio 为 Python 提供一级语言支持。 本教程将指导你完成以下步骤：

- [步骤 0：安装](tutorial-working-with-python-in-visual-studio-step-00-installation.md)
- [步骤 1：创建 Python 项目（本文）](#step-1-create-a-new-python-project)
- [步骤 2：编写和运行代码，以便在工作时查看 Visual Studio IntelliSense](tutorial-working-with-python-in-visual-studio-step-02-writing-code.md)
- [步骤 3：在 REPL 交互窗口中创建更多代码](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md)
- [步骤 4：在 Visual Studio 调试器中运行已完成的程序](tutorial-working-with-python-in-visual-studio-step-04-debugging.md)
- [步骤 5：安装程序包和管理 Python 环境](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)
- [步骤 6：使用 Git](tutorial-working-with-python-in-visual-studio-step-06-working-with-git.md)

[!INCLUDE[tutorial-prereqs](includes/tutorial-prereqs.md)]

## <a name="step-1-create-a-new-python-project"></a>步骤 1：创建新的 Python 项目

*项目*是 Visual Studio 管理所有文件（包括源代码、资源、配置等等）的一种方式，这些文件结合在一起可生成单个应用程序。 项目可规范和维护其所有文件以及由多个项目共享的外部资源之间的关系。 比起在临时文件夹、脚本、文本文件中甚至完全按自己的想法简单地管理项目关系，这样做让应用程序能够更轻松地扩展和增长。

本教程将从一个包含单一空代码文件的简单项目开始。

1. 在 Visual Studio 中，选择“文件” > “新建” > “项目”(Ctrl+Shift+N)，这会打开“新建项目”对话框。 可在该对话框中浏览各种语言的模板，然后为项目选择一个模板，并指定 Visual Studio 放置文件的位置。

1. 若要查看 Python 模板，可在左侧选择“已安装” > “Python”或搜索“Python”。 如果忘记了模板在语言树中的位置，使用搜索是找到该模板的好方法。

    ![显示 Python 项目的新建项目对话框](media/vs-getting-started-python-01-new-project.png)

    注意 Visual Studio 中的 Python 支持如何包含大量项目模板，包括使用 Bottle、Flask 和 Django 框架的 Web 应用程序。 但为了便于演示，我们以空项目开始。

1. 选择“Python 应用程序”模板，为项目指定名称并选择“确定”。

1. 几分钟后，Visual Studio 会在“解决方案资源管理器”窗口 (1) 中显示项目结构。 默认代码文件在编辑器 (2) 中处于打开状态。 “属性”窗口 (3) 也会出现，其中显示在“解决方案资源管理器”中选定的任何项的附加信息（包括它在磁盘上的确切位置）。

    ![具有 Python 项目的解决方案资源管理器](media/vs-getting-started-python-02-windows.png)

1. 花点时间熟悉一下“解决方案资源管理器”，可在该管理器中浏览项目中的文件和文件夹。

    ![解决方案资源管理器已展开显示各种功能](media/vs-getting-started-python-03-solution-explorer.png)

    (1) 粗体突出显示的是项目，其名称是在“新建项目”对话框中指定的名称。 在磁盘上，此项目由项目文件夹中的 .pyproj 文件表示。

    (2) 顶层是一个*解决方案*，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器。 例如，如果为 Python 应用程序编写 C++ 扩展，该 C++ 项目可以驻留在同一解决方案中。 解决方案还可以包含 Web 服务的项目，以及专用测试程序的项目。

    (3) 在项目下方可以看到源文件，在本例中，只有一个 .py 文件。 选择文件时会在“属性”窗口中显示其属性。 双击文件会以任何适合该文件的方式打开该文件。

    (4) 项目下方还有“Python 环境”节点。 展开后，可以看到可用的 Python 解释器。 展开解释器节点可查看安装到该环境 (5) 中的库。

    右键单击“解决方案资源管理器”中的任意节点或项均可访问适用命令菜单。 例如，“重命名”命令可用于更改任何节点或项（包括项目和解决方案）的名称。

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [编写并运行代码](tutorial-working-with-python-in-visual-studio-step-02-writing-code.md)

## <a name="go-deeper"></a>深入了解

- [Visual Studio 中的 Python 项目](managing-python-projects-in-visual-studio.md)。
- [在 python.org 上了解 Python 语言](https://www.python.org)
- [Python for Beginners](https://www.python.org/about/gettingstarted/)（面向初学者的 Python，python.org）
