---
title: 使用 requirements.txt 文件管理包依赖项
description: requirements.txt 文件描述了项目的依赖项。 如果收到包含 requirements.txt 文件的项目，你将可以在一个步骤中轻松安装这些依赖关系。
ms.date: 03/18/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: a1853df63354801ebf0413d3c8707135cb9bb800
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62535696"
---
# <a name="manage-required-packages-with-requirementstxt"></a>使用 requirements.txt 管理所需的包

若要与其他人共享项目、使用生成系统，或打算将项目复制到需要在其中还原环境的其他任何位置，必须指定项目需要的外部包。 建议的方法是使用 [requirements.txt 文件](https://pip.readthedocs.org/en/latest/user_guide.html#requirements-files) (readthedocs.org)，文件中包含安装相关包所需版本的 pip 命令列表。 最常见的命令是 `pip freeze > requirements.txt`，它将环境的当前包列表记录到 requirements.txt  中。

从技术上讲，任何文件名都可用于跟踪要求（通过安装包时使用 `-r <full path to file>`），但 Visual Studio 提供针对 requirements.txt  的特定支持：

- 如果已加载包含 requirements.txt 的项目，且想要安装该文件列出的所有包，请展开“解决方案资源管理器”中的“Python 环境”节点，然后右键单击环境节点并选择“从 requirements.txt 安装”：

    ![从 requirements.txt 安装](media/environments/environments-requirements-txt-install.png)

- 如果要在虚拟环境中安装依赖项，请首先创建并激活该环境，然后使用“从 requirements.txt 安装”  命令。 有关创建虚拟环境的详细信息，请参阅[使用虚拟环境](selecting-a-python-environment-for-a-project.md#use-virtual-environments)。

- 如果环境中已安装所有必需的包，可在“解决方案资源管理器”  中右键单击该环境，并选择“生成 requirements.txt”  以创建必需的文件。 如果文件已存在，会出现有关如何进行更新的提示：

    ![更新 requirements.txt 选项](media/environments/environments-requirements-txt-replace.png)

  - “替换整个文件”  将删除存在的所有项、注释和选项。
  - “刷新现有条目”会检测包的要求并更新版本说明符，匹配当前安装的版本  。
  - “更新并添加项”  将刷新找到的任何要求，并将所有其他包添加到文件末尾。

因为 requirements.txt  文件的目的是冻结环境的要求，因此所有已安装的包都采用精确的版本编写。 使用精确的版本可确保轻松地在其他计算机上重现环境。 即使采用一个版本范围（作为另一个包的依赖项）或使用安装程序而非 pip 安装了包，也会包含这些包。

如果包不能通过 pip 安装，且它出现在 requirements.txt  文件中，则整个安装会失败。 在这种情况下，手动编辑文件以排除此包或使用 [pip 的选项](https://pip.readthedocs.org/en/latest/reference/pip_install.html#requirements-file-format)来指包的可安装版本。 例如，你可能更喜欢使用 [`pip wheel`](https://pip.readthedocs.org/en/latest/reference/pip_wheel.html) 来编译依赖项，并向 requirements.txt 添加 `--find-links <path>` 选项：

```output
C:\Project>pip wheel azure
Downloading/unpacking azure
    Running setup.py (path:C:\Project\env\build\azure\setup.py) egg_info for package azure

Building wheels for collected packages: azure
    Running setup.py bdist_wheel for azure
    Destination directory: c:\project\wheelhouse
Successfully built azure
Cleaning up...

C:\Project>type requirements.txt
--find-links wheelhouse
--no-index
azure==0.8.0

C:\Project>pip install -r requirements.txt -v
Downloading/unpacking azure==0.8.0 (from -r requirements.txt (line 3))
    Local files found: C:/Project/wheelhouse/azure-0.8.0-py3-none-any.whl
Installing collected packages: azure
Successfully installed azure
Cleaning up...
    Removing temporary dir C:\Project\env\build...
```

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中管理 Python 环境](managing-python-environments-in-visual-studio.md)
- [为项目选择解释器](selecting-a-python-environment-for-a-project.md)
- [搜索路径](search-paths.md)
- [“Python 环境”窗口参考](python-environments-window-tab-reference.md)
