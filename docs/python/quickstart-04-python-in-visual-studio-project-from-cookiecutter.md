---
title: 快速入门 - 使用 Cookiecutter 创建 Python 项目
description: 在此快速入门教程中，使用 Cookiecutter 模板创建适合 Python 的 Visual Studio 项目。
ms.date: 02/25/2019
ms.topic: quickstart
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 3f3e7f56f4a36a7958cba9bd7092f38d735123d4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62954480"
---
# <a name="quickstart-create-a-project-from-a-cookiecutter-template"></a>快速入门：通过 Cookiecutter 模板创建项目

[在 Visual Studio 中安装 Python 支持](installing-python-support-in-visual-studio.md)后，就可以从 Cookiecutter 模板轻松创建新项目，其中包括许多发布到 GitHub 的模板。 [Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) 可提供图形用户界面，用于发现模板、输入模板选项以及创建项目和文件。 Cookiecutter 随附在 Visual Studio 2017 及更高版本中，在 Visual Studio 早期版本中可单独安装。

1. 在本快速入门教程中，首先安装 Anaconda3 Python 分发版本，其中包括此处所示的 Cookiecutter 模板必需的 Python 程序包。 运行 Visual Studio 安装程序，选择“修改”，展开右侧的“Python 开发”选项，选择“Anaconda3”（32 位或 64 位均可）。 请注意，安装可能需要一些时间，具体取决于 Internet 速度，但这是安装所需程序包最简单的方法。

1. 启动 Visual Studio。

1. 选择“文件” > “新建” > “从 Cookiecutter”。 此命令会在 Visual Studio 中打开一个窗口，可在窗口中浏览模板。

    ![从 Cookiecutter 模板新建项目](media/projects-from-cookiecutter1.png)

1. 选择“Microsoft/python-sklearn-classifier-cookiecutter”模板，然后选择“下一步”。 （首次使用特定模板时，该过程可能需要几分钟，因为 Visual Studio 将安装所需的 Python 包。）

1. 接下来，在“创建到”字段中设置新项目的位置，然后选择“创建和打开项目”。

    ![第二步使用 Cookiecutter, 设置项目属性](media/projects-from-cookiecutter2.png)

1. 该过程完成后，显示“已成功使用模板创建文件...”消息。项目在解决方案资源管理器中自动打开。

1. 按 Ctrl+F5 或选择“调试” > “开始执行(不调试)”运行程序。

    ![python-sklearn-classifier-cookiecutter 模板项目的输出](media/projects-from-cookiecutter4.png)

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [教程：在 Visual Studio 中使用 Python](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>请参阅

- [使用 Cookiecutter 扩展](using-python-cookiecutter-templates.md)
- [手动标识现有的 Python 解释器](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
- [在 Visual Studio 2015 及更早版本中安装 Python 支持](installing-python-support-in-visual-studio.md)
- [安装位置](installing-python-support-in-visual-studio.md#install-locations)
