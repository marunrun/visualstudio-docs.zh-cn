---
title: 将 PyLint 用于 Python 代码
description: 在 Visual Studio 中运行 PyLint 检查 Python 代码中的问题，包括自定义 linting 的命令行选项。
ms.date: 03/13/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: bf503cff7d8de2c00a93385113de05de00059390
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62956795"
---
# <a name="use-pylint-to-check-python-code"></a>使用 PyLint 检查 Python 代码

[PyLint](https://www.pylint.org/) 是一种广泛使用的工具，当前已集成到 Visual Studio for Python 项目中，可用于检查 Python 代码中的错误以及促进建立良好的 Python 编码模式。

## <a name="run-pylint"></a>运行 PyLint

右键单击解决方案资源管理器中的 Python 项目，并选择“Python” > “运行 PyLint...”：

![用于 Python 项目的上下文菜单上的 PyLint 命令](media/code-pylint-command.png)

如果尚无 PyLint，使用此命令时系统会提示你在活动环境中安装 PyLint。

PyLint 警告和错误显示在“错误列表”窗口中：

![PyLint 错误列表](media/code-pylint-error-list.png)

双击错误可直接转到出现问题的源代码。

> [!Tip]
> 有关所有 PyLint 输出消息的详细列表，请参阅[PyLint 功能参考](https://pylint.readthedocs.io/en/latest/technical_reference/features.html)。

## <a name="set-pylint-command-line-options"></a>设置 PyLint 命令行选项

PyLint 文档中的[命令行选项](https://pylint.readthedocs.io/en/latest/user_guide/run.html#command-line-options)部分介绍了如何通过 .pylintrc 配置文件控制 PyLint 的行为。 此类文件可置于 Visual Studio 中的 Python 项目的根路径中或其他地方，具体取决于想要应用这些设置的范围（请参阅[命令行选项](https://pylint.readthedocs.io/en/latest/user_guide/run.html#command-line-options)了解详细信息）。

例如，若要使用项目中的 .pylintrc 文件禁止显示上图所示的“缺少 docstring”警告，请执行以下步骤：

1. 使用命令行导航到包含 .pyproj 文件的项目根路径，并运行以下命令以生成已注释的配置文件：

   ```command
   pylint --generate-rcfile > .pylintrc
   ```

1. 在 Visual Studio 解决方案资源管理器中，右键单击项目，选择“添加” > “退出项”，导航到新的 .pylintrc 文件，并选中该文件，然后选择“添加”。

1. 打开要编辑的文件，该文件中包含可以使用的几种设置。 若要禁用警告，请找到 `[MESSAGES CONTROL]` 部分，然后在该部分中找到 `disable` 设置。 将出现特定消息的一条长字符串，可以向其追加所需的任何警告。 在此例中，追加 `,missing-docstring`（包括界定逗号）。

1. 保存 .pylintrc 文件，然后再次运行 PyLint 以查看现在禁止显示的警告。

> [!Tip]
> 若要从网络共享使用 .pylintrc 文件，请创建一个名为 `PYLINTRC` 的环境变量，其值为网络共享上使用 UNC 路径或映射驱动器号的文件名。 例如 `PYLINTRC=\\myshare\python\.pylintrc`。
