---
title: Visual Studio 中的 Python 教程步骤 5，安装包
titleSuffix: ''
description: 在 Visual Studio 中使用 Python 功能的核心教程的第 5 步，展示了用于在 Python 环境中管理包的 Visual Studio 功能。
ms.date: 03/09/2020
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 5e2644ccfff0e7c653f4ce2680299aea95a55ef9
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "79372896"
---
# <a name="step-5-install-packages-in-your-python-environment"></a>步骤 5：在 Python 环境中安装程序包

**上一步：[在调试器中运行代码](tutorial-working-with-python-in-visual-studio-step-04-debugging.md)**

Python 开发者社区制作了数千个有用的程序包，用户可以将它们合并到自己的项目中。 Visual Studio 提供一个 UI，用于管理 Python 环境中的程序包。

## <a name="view-environments"></a>查看环境

1. 选择“视图” > “其他窗口” > “Python 环境”菜单命令    。 “Python 环境”  窗口作为“解决方案资源管理器”  的同级打开，并向用户显示各种可用的环境。 列表中显示了使用 Visual Studio 安装程序安装的环境以及单独安装的环境。 其中包括全局环境、虚拟环境和 conda 环境。 粗体显示的环境是用于新项目的默认环境。 要详细了解如何使用环境，请参阅[如何在 Visual Studio 中创建和管理 Python 环境](managing-python-environments-in-visual-studio.md)。

   ![“Python 环境”窗口](media/environments/environments-default-view-2019.png)

   > [!NOTE]
   > 还可单击“解决方案资源管理器”窗口，再使用 Ctrl+K 或 Ctrl+` 键盘快捷方式打开“Python 环境”窗口。 如果快捷方式不起作用，并且在菜单中找不到“Python 环境”窗口，则可能是你未安装 Python 工作负载。 有关如何安装 Python 的指南，请参阅[如何在 Visual Studio 中安装 Python 支持](installing-python-support-in-visual-studio.md)。

2. 通过环境的“概述”  选项卡，可以快速访问该环境的交互  窗口以及安装文件夹和解释器。 例如，选择“打开交互窗口”  ，会在 Visual Studio 中显示该特定环境的交互  窗口。

3. 现在，通过选择“文件” > “新建” > “项目”来创建新项目，然后选择“Python 应用程序”模板     。 在随即出现的代码文件中，粘贴以下代码来创建像之前的教程步骤一样的余弦波，只不过这次以图形方式绘制。 或者，可使用之前创建的项目并替换代码。 

    ```python
    from math import radians
    import numpy as np     # installed with matplotlib
    import matplotlib.pyplot as plt

    def main():
        x = np.arange(0, radians(1800), radians(12))
        plt.plot(x, np.cos(x), 'b')
        plt.show()

    main()
    ```

4. 打开 Python 项目后，还可右键单击 Python 环境，再选择“查看所有 Python 环境”，从解决方案资源管理器中打开“Python 环境”窗口**V**

   ![环境](media/environments/environments-view-all-2019.png)

5. 查看编辑器窗格，你会发现如果你将鼠标悬停到 `numpy` 和 `matplotlib` 上，会导入显示未解析的语句。 这是因为尚未在默认全局环境中安装包。

   ![未解析的包导入](media/packages-unresolved-import.png)

## <a name="install-packages-using-the-python-environments-window"></a>使用“Python 环境”窗口安装包

1. 在“Python 环境”窗口中，为新的 Python 环境单击默认环境，然后选择“包”选项卡  。然后，你将看到环境中当前已安装的包的列表。

   ![环境中安装的程序包](media/environments/environments-installed-packages-2019.png)

2. 在搜索字段输入 `matplotlib` 的名称，再选择“运行命令: pip install matplotlib”选项来安装此项目  。 这将安装 `matplotlib`还将安装它依赖的所有包（在本例中，包含 `numpy`）。

   ![在环境中安装 matplotlib](media/environments/environments-add-matplotlib-2019.png)

5. 如果系统提示同意提升，请同意。

6. 安装程序包后，它会显示在“Python 环境”  窗口中。 单击程序包右侧的 **X** 可卸载它。

   ![在环境中完成 matplotlib 的安装](media/environments/environments-add-matplotlib2-2019.png)

   > [!NOTE]
   > 环境下方可能会出现一个小进度栏，指示 Visual Studio 正在为新安装的程序包生成 IntelliSense 数据库。 “IntelliSense”  选项卡也显示了更多详细信息。 请注意，完成该数据库之前，编辑器中的自动完成和语法检查等 IntelliSense 功能针对该程序包处于非活动状态。
   > 
   > Visual Studio 2017 15.6 及更高版本采用不同且更快的方法来使用 IntelliSense，并在“IntelliSense”选项卡上显示一条简要介绍此内容的消息  。

## <a name="run-the-program"></a>运行程序

1. 现已安装 [matplotlib](https://matplotlib.org/)，请按 (F5) 运行项目来查看输出；如果没有调试器，则使用 (Ctrl+F5)    ：

   ![matplotlib 示例的输出](media/environments/environments-add-matplotlib3.png)

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [使用 Git](tutorial-working-with-python-in-visual-studio-step-06-working-with-git.md)

## <a name="go-deeper"></a>深入了解

- [Python 环境](managing-python-environments-in-visual-studio.md)
- [了解 Visual Studio 中的 Django](learn-django-in-visual-studio-step-01-project-and-solution.md)
- [了解 Visual Studio 中的 Flask](learn-flask-visual-studio-step-01-project-solution.md)
