---
title: 快速入门 — 打开 Python 代码文件夹
description: 在此快速入门中，无需使用 Visual Studio 项目即可从文件夹中打开并运行 Python 代码（仅限 Visual Studio 2019）。
ms.date: 03/12/2019
ms.topic: quickstart
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
monikerRange: '>= vs-2019'
ms.openlocfilehash: ab234d9482cf9cbab49c15167ea45aff9ac2c7e6
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "62431065"
---
# <a name="quickstart-open-and-run-python-code-in-a-folder"></a>快速入门：打开并运行文件夹中的 Python 代码

[在 Visual Studio 2019 中安装 Python 支持](installing-python-support-in-visual-studio.md)后，就可以在 Visual Studio 2019 中轻松地运行现有 Python 代码，而无需创建 Visual Studio 项目。

> [!Note]
> 在 Visual Studio 2017 及更早版本中，需要创建 Visual Studio 项目才能运行 Python 代码，使用内置项目模板可以轻松执行此操作。 请参阅[快速入门：从现有代码创建 Python 项目](quickstart-01-python-in-visual-studio-project-from-existing-code.md)

1. 在本演练中，可以将任何文件夹与你喜欢的 Python 代码搭配使用。 若要按照如下所示的示例操作，请在相应文件夹中使用命令 `git clone https://github.com/gregmalcolm/python_koans` 将 gregmalcolm/python_koans GitHub 存储库克隆到你的计算机。

1. 在“启动”窗口中启动 Visual Studio 2019，然后在“开始”栏底部选择“打开”   。 或者，如果已在运行 Visual Studio，请改为选择“文件”   > “打开”   > “文件夹”  命令。

    ![Visual Studio 启动屏幕](media/quickstart-open-folder/01-open-local-folder.png)

1. 导航到包含 Python 代码的文件夹，然后选择“选择文件夹”  。 如果使用的是 python_koans 代码，请务必选中克隆文件夹中的 `python3` 文件夹。

    ![“打开文件夹”命令中的“选择文件夹”对话框](media/quickstart-open-folder/02-select-folder.png)

1. Visual Studio 将在解决方案资源管理器中的“文件夹视图”中显示该文件夹   。 可以使用文件夹名称左边缘的箭头展开和折叠文件夹：

    ![解决方案资源管理器中用于展开和折叠文件夹的控件](media/quickstart-open-folder/03-expand-collapse-folders.png)

1. 打开 Python 文件夹时，Visual Studio 将创建几个隐藏文件夹来管理与项目相关的设置。 若要查看这些文件夹（以及任何其他隐藏的文件和文件夹，如 .git  文件夹），请选择  “显示所有文件”工具栏按钮：

    ![解决方案资源管理器中的隐藏文件夹视图](media/quickstart-open-folder/05-view-hidden-folders.png)

1. 若要运行代码，首先需要确定启动文件或主程序文件。 在此处显示的示例中，启动文件为 contemplate-koans.py  。 右键单击该文件，然后选择“设为启动项”  。

    ![在解决方案资源管理器中设置启动项](media/quickstart-open-folder/06-set-as-startup-item-command.png)

    > [!Important]
    > 如果启动项不在已打开的文件夹的根目录中，还必须将一行添加到启动配置 JSON 文件中，如[设置工作目录](#set-a-working-directory)部分中所述。

1. 按 Ctrl  +F5  ，或依次选择“调试” > “启动但不调试”  运行代码  。 另外，还可以选择显示带有播放按钮的启动项的工具栏按钮，在 Visual Studio 调试程序中运行代码。 在所有情况下，Visual Studio 会检测到启动项是一个 Python 文件，因此会在默认 Python 环境中自动运行代码。 （该环境显示在工具栏上启动项的右侧。）

    ![启动调试程序工具栏按钮](media/quickstart-open-folder/07-start-debug-toolbar.png)

1. 程序的输出将显示在单独的命令窗口中：

    ![用于运行 Python 代码的输出窗口](media/quickstart-open-folder/08-result-window.png)

1. 若要在其他环境中运行代码，请从工具栏上的下拉列表框控件中选择该环境，然后再次启动启动项。

1. 若要关闭 Visual Studio 中的文件夹，请选择“文件”   > “关闭文件夹”  菜单命令。

## <a name="set-a-working-directory"></a>设置工作目录

默认情况下，Visual Studio 会运行作为该同一文件夹的根目录中的文件夹打开的 Python 项目。 但是，项目中的代码可假定正在子文件夹中运行 Python。 例如，假定打开 python_koans 存储库的根文件夹，然后将 python3/contemplate-koans.py  文件设置为启动项。 如果随后运行代码，会看到错误，指出找不到 koans.txt 文件  。 发生此错误是因为 contemplate-koans.py  假定正在 python3  文件夹（而不是存储库根目录）中运行 Python。

在这种情况下，还必须将一行添加到启动配置 JSON 文件以指定工作目录：

1. 在解决方案资源管理器中右键单击 Python (.py  ) 启动文件  ，然后选择“调试和启动设置”  。

    ![用于 Python 文件的“调试和启动设置”命令](media/quickstart-open-folder/09-debug-launch-settings-menu-command.png)

1. 在出现的“选择调试程序”  对话框中，选择“默认”  ，然后选择“选择”  。

    ![用于 Python 文件的“调试和启动设置”命令](media/quickstart-open-folder/10-select-debugger.png)

    > [!Note]
    > 如果没有看到“默认”  选项，请确保在选择“调试和启动设置”命令时右键单击了 Python .py  文件  。 Visual Studio 利用文件类型来确定要显示的调试程序选项。

1. Visual Studio 会打开名为 launch.vs.json 的文件  ，该文件位于隐藏的 .vs  文件夹中。 此文件描述项目的调试上下文。 若要指定工作目录，请为 `"workingDirectory"` 添加一个值，如 python-koans 示例的 `"workingDirectory": "python3"` 中所示：

    ```json
    {
      "version": "0.2.1",
      "defaults": {},
      "configurations": [
        {
          "type": "python",
          "interpreter": "(default)",
          "interpreterArguments": "",
          "scriptArguments": "",
          "env": {},
          "nativeDebug": false,
          "webBrowserUrl": "",
          "project": "python3\\contemplate_koans.py",
          "name": "contemplate_koans.py",
          "workingDirectory": "python3"
        }
      ]
    }
    ```

1. 保存该文件并再次启动程序，现在它在指定文件夹中运行。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [教程：在 Visual Studio 中使用 Python](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>请参阅

- [快速入门：从现有代码创建 Python 项目](quickstart-01-python-in-visual-studio-project-from-existing-code.md)
- [快速入门：通过存储库创建 Python 项目](quickstart-03-python-in-visual-studio-project-from-repository.md)
- [手动标识现有的 Python 解释器](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
