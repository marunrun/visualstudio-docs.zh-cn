---
title: Visual Studio 中的 Python 教程步骤 6，使用 Git
titleSuffix: ''
description: 在 Visual Studio 中使用 Python 的核心教程的第 6 步，介绍了 Visual Studio 的 Git 相关功能。
ms.date: 01/28/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: cd8ebd706d9228d23eb5d5ce3b1429063bae55e5
ms.sourcegitcommit: a5a54b147e772dc39e519da74ec41a0c25d99628
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289714"
---
# <a name="step-6-work-with-git"></a>步骤 6：使用 Git

**上一步：[安装程序包和管理 Python 环境](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)**

Visual Studio 提供与本地 Git 存储库以及 GitHub 和 Azure Repos 等服务上的远程存储库的直接集成。 集成包括克隆存储库、提交更改和管理分支。

本文简要概述了如何创建现有项目的本地 Git 存储库，并介绍 Visual Studio 的一些 Git 相关功能。

1. 在 Visual Studio 中打开项目后，比如[上一步](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)中的项目，右键单击解决方案并选择“将解决方案添加到源代码管理”  。 Visual Studio 将创建包含项目代码的本地 Git 存储库。

1. Visual Studio 检测到项目托管在 Git 存储库中时，Visual Studio 窗口右下角会显示 Git 相关控件。 控件显示挂起的提交、更改、存储库名称和分支。 将鼠标悬停在控件上可查看附加信息。

    ![将鼠标悬停在 Visual Studio 窗口中的 Git 控件上时显示附加信息](media/working-with-git-01.png)

1. 新建一个存储库或选择任意 Git 控件时，Visual Studio 会打开“团队资源管理器”窗口  。 （可随时通过“视图”   > “团队资源管理器”  菜单命令打开该窗口。）窗口带有三个主窗格，你可使用“团队资源管理器”标题上的下拉菜单进行切换  。 在选择“推送”  控件（向上箭头图标）时，还显示可用于发布内容的“同步”  窗格：

    ![创建本地存储库后 Visual Studio 中的团队资源管理器](media/working-with-git-02.png)

1. 选择“更改”（或带铅笔图标的 Git 控件），以查看未提交的更改并在必要时进行提交  。

    ![Visual Studio 中显示未提交更改的团队资源管理器](media/working-with-git-03.png)

    双击“更改”列表中的文件打开该文件的差异视图  ：

    ![文件更改的差异视图](media/working-with-git-05.png)

1. 选择“分支”（或带分支名称的 Git 控件），以检查分支并执行合并和变基操作  ：

    ![Visual Studio 中显示分支的团队资源管理器](media/working-with-git-04.png)

1. 选择带存储库名称的 Git 控件（上图中的“CosineWave”  ）之后，“团队资源管理器”  将显示可用于迅速彻底切换到其他存储库的“连接”  接口。

1. 使用本地存储库时，提交的更改直接进入存储库。 如果已连接到远程存储库，则选择“团队资源管理器”  中的下拉列表标题，再选择“同步”  以切换到“同步”  部分，然后处理此处显示的拉取  和提取  命令。

## <a name="go-deeper"></a>深入了解

有关基于远程 Git 存储库创建项目的简短演练，请参阅[快速入门：在 Visual Studio 中克隆 Python 代码存储库](quickstart-03-python-in-visual-studio-project-from-repository.md)。

有关更全面的教程（包括处理合并冲突、使用拉取请求查看代码、变基和挑拣分支之间的更改），请参阅[开始使用 Git 和 Azure Repos](/azure/devops/repos/git/gitquickstart)。

## <a name="tutorial-review"></a>教程回顾

恭喜你完成有关 Visual Studio 中 Python 的这一教程。 在本教程中，已了解如何：

- 创建项目和查看项目内容。
- 使用代码编辑器和运行项目。
- 使用交互  窗口开发新代码，并将该代码轻松复制到编辑器中。
- 在 Visual Studio 调试器中运行已完成的程序。
- 安装程序包和管理 Python 环境。
- 使用 Git 存储库中的代码。

在此处了解概念和操作说明指南，其中包括下文：

- [创建适用于 Python 的 C++ 扩展](working-with-c-cpp-python-in-visual-studio.md)
- [发布到 Azure 应用服务](publishing-python-web-applications-to-azure-from-visual-studio.md)
- [分析](profiling-python-code-in-visual-studio.md)
- [单元测试](unit-testing-python-in-visual-studio.md)
