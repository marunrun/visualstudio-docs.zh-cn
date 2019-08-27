---
title: 选择用于项目的 Python 解释器和项目
description: 可以专门选择 Python 环境（包括 Anaconda 和虚拟环境）以应用于特定项目。
ms.date: 03/18/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 9d7736365e8e2bb371a71580492401bb2660fcc3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62429622"
---
# <a name="how-to-select-a-python-environment-for-a-project"></a>如何选择用于项目的 Python 环境

Python 项目中的所有代码都在特定环境的上下文中运行，例如全局 Python 环境、Anaconda 环境、虚拟环境或 conda 环境。 Visual Studio 还将该环境用于调试、导入和成员完成、语法检查，以及需要特定于 Python 版本和一组已安装包的语言服务的任何其他任务。

Visual Studio 中所有新的 Python 项目最初都被配置为使用默认的全局环境，它出现在“解决方案资源管理器”的“Python 环境”节点下：

![“解决方案浏览器”中显示的全局默认 Python 环境](media/environments/environments-project.png)

::: moniker range="vs-2017"
要更改项目环境，请右键单击“Python 环境”节点，然后选择“添加/删除 Python 环境”。 在包含全局、虚拟和 conda 环境的所示列表中，选择希望在“Python 环境”节点下显示的所有环境：

![“添加/删除 Python 环境”对话框](media/environments/environments-add-remove.png)

一旦选择“确定”，所有选择的环境都将显示在“Python 环境”节点下。 当前激活的环境以粗体显示：

![“解决方案浏览器”中显示的多个 Python 环境](media/environments/environments-project-multiple.png)

要快速激活其他环境，请右键单击环境名称，并选择“激活环境”。 你的选择将保存在项目中，当你在将来打开该项目，环境就会被激活。 如果在“添加/删除 Python 环境”对话框中清除所有选项，Visual Studio 将激活全局默认环境。

“Python 环境”节点的上下文菜单还提供其他命令：

| 命令 | 说明 |
| --- | --- |
| **添加虚拟环境** | 首先在项目中新建一个虚拟环境。 详情请参阅[创建虚拟环境](#create-a-virtual-environment)。 |
| **添加现有虚拟环境** | 系统提示你选择一个包含虚拟环境的文件夹并将其添加到“Python 环境”下的列表，但不进行激活。 请参阅[激活现有的虚拟环境](#activate-an-existing-virtual-environment)。 |
| **创建 Conda 环境** | 切换到“Python 环境”窗口，在此处输入环境的名称并指定其基础解释器。 请参阅 [Conda 环境](managing-python-environments-in-visual-studio.md#conda-environments)。 |
::: moniker-end

::: moniker range=">=vs-2019"
若要更改项目的环境，请右键单击“Python 环境”节点，然后选择“添加环境”，或从 Python 工具栏的环境下拉列表中选择“添加环境”。

在“添加环境”对话框中，选择“现有环境”选项卡，然后从“环境”下拉列表中选择新环境：

![在“添加环境”对话框中选择项目环境](media/environments/environments-project-2019.png)

如果已向项目中添加除全局默认值以外的环境，则可能需要激活新添加的环境。 右键单击“Python 环境”节点下的该环境，然后选择“激活环境”。 若要从项目中删除环境，请选择“删除”。

![激活并删除项目环境](media/environments/environments-project-add-remove-2019.png)
::: moniker-end

## <a name="use-virtual-environments"></a>使用虚拟环境

虚拟环境是特定 Python 解释器和一组特定库的独特组合，它与其他全局环境以及 conda 环境不同。 虚拟环境特定于项目，但保留在项目文件夹中。 该文件夹包含环境中已安装的库，还有一个 pyvenv.cfg 文件用于指定到文件系统中其他位置的环境基础解释器的路径。 （即，虚拟环境中没有解释器副本，只有解释器链接。）

使用虚拟环境的一项优势是，随着项目的开发，虚拟环境始终反映出项目的确切依赖项。 （另一方面，无论是否在项目中使用库，共享的全局环境中都包含任意数量的库。）随后即可通过虚拟环境轻松创建 requirements.txt 文件，此文件之后用于在另一台开发/生产计算机上重新安装上述依赖项。 有关详细信息，请参阅[使用 requirements.txt 管理所需的包](managing-required-packages-with-requirements-txt.md)。

在 Visual Studio 中打开包含 requirements.txt 文件的项目时，Visual Studio 自动显示用于重新创建虚拟环境的选项。 在未安装 Visual Studio 的计算机上，可运行 `pip install -r requirements.txt` 还原包。

由于虚拟环境包含到基础解释器的硬编码路径，且你可使用 requirements.txt 重新创建环境，因此通常省略来自源代码管理功能集的整个虚拟环境。

下述部分介绍了如何激活项目中的现有虚拟环境以及如何创建新的虚拟环境。

在 Visual Studio 中，可通过“解决方案资源管理器”中的“Python 环境”节点，如其他任意环境一样激活项目的虚拟环境。

虚拟环境添加到项目后，立即显示在“Python 环境”窗口中。 随后，即可像激活其他任意环境一样激活它，还可管理它的包。

::: moniker range="vs-2017"
### <a name="create-a-virtual-environment"></a>创建虚拟环境

可以按以下方式直接在 Visual Studio 中创建新的虚拟环境：

1. 在“解决方案资源管理器”中，右键单击“Python 环境”并选择“添加虚拟环境”，将会打开以下对话框：

    ![创建虚拟环境](media/environments/environments-add-virtual-1.png)

1. 在“虚拟环境位置”字段中，指定虚拟环境的路径。 如果仅指定一个名称，则会在当前项目中在具有该名称的子文件夹中创建虚拟环境。

1. 选择一个环境作为基础解释器，并选择“创建”。 Visual Studio 会在配置环境和下载任何必要的包时显示一个进度栏。 完成后，虚拟环境将显示在所含项目的“Python 环境”窗口中。

1. 默认情况下不会激活虚拟环境。 若要为项目激活虚拟环境，请右键单击该项目，然后选择“激活环境”。

> [!Note]
> 如果位置路径标识一个现有的虚拟环境，Visual Studio 会自动检测基础解释器（使用环境 lib 目录中的 orig-prefix.txt 文件）并将“创建”按钮更改为“添加”。
>
> 添加虚拟环境时，如果 requirements.txt 文件存在，“添加虚拟环境”对话框会显示一个自动安装包的选项，从而可以轻松地在另一台计算机上重新创建环境：
>
> ![使用 requirements.txt 创建虚拟环境](media/environments/environments-requirements-txt.png)
>
> 无论采用哪种方式，结果都与使用“添加现有的虚拟环境”命令相同。

### <a name="activate-an-existing-virtual-environment"></a>激活现有的虚拟环境

如果你已经在其他地方创建了虚拟环境，可以按以下方式为项目激活它：

1. 在“解决方案资源管理器”中，右键单击“Python 环境”并选择“添加现有虚拟环境”。

1. 在出现的“浏览”对话框中，导航到包含虚拟环境的文件夹并选中，然后选择“确定”。 如果 Visual Studio 在该环境中检测到 requirements.txt 文件，它会询问是否安装这些包。

1. 稍后，虚拟环境会出现在“解决方案资源管理器”中的“Python 环境”节点下。 默认情况下不会激活虚拟环境，因此请右键单击它并选择“激活环境”。
::: moniker-end

::: moniker range=">=vs-2019"
### <a name="create-a-virtual-environment"></a>创建虚拟环境

可以按以下方式直接在 Visual Studio 中创建新的虚拟环境：

1. 右键单击“解决方案资源管理器”中的“Python 环境”，然后选择“添加环境”，或从 Python 工具栏上的环境下拉列表中选择“添加环境”。 在出现的“添加环境”对话框中，选择“虚拟环境”选项卡：

    ![“添加环境”对话框的“虚拟环境”选项卡](media/environments/environments-add-virtual-1-2019.png)

1. 为虚拟环境指定一个名称，选择基础解释器，然后验证其位置。 在“从文件安装包”下，提供 requirements.txt 文件的路径（如果需要）。

1. 查看对话框中的其他选项：

    | 选项 | 说明 |
    | --- | --- |
    | 设置为当前环境 | 创建环境后，在所选项目中激活新环境。 |
    | 设置为新项目的默认环境 | 自动设置和激活 Visual Studio 中创建的任何新项目中的虚拟环境。 使用此选项时，应将虚拟环境置于特定项目之外的位置中。  |
    | 在“Python 环境”窗口中查看 | 指定在创建环境之后是否打开“Python 环境”窗口。 |
    | 使此环境全局可用 | 指定虚拟环境是否同时充当全局环境。 使用此选项时，应将虚拟环境置于特定项目之外的位置中。 |

1. 选择“创建”以完成虚拟环境。 Visual Studio 会在配置环境和下载任何必要的包时显示一个进度栏。 完成后，虚拟环境将激活并显示在“解决方案资源管理器”的“Python 环境”节点中以及所含项目的“Python 环境”窗口中。

### <a name="activate-an-existing-virtual-environment"></a>激活现有的虚拟环境

如果你已经在其他地方创建了虚拟环境，可以按以下方式为项目激活它：

1. 右键单击“解决方案资源管理器”中的“Python 环境”，然后选择“添加环境”。

1. 在出现的“浏览”对话框中，导航到包含虚拟环境的文件夹并选中，然后选择“确定”。 如果 Visual Studio 在该环境中检测到 requirements.txt 文件，它会询问是否安装这些包。

1. 稍后，虚拟环境会出现在“解决方案资源管理器”中的“Python 环境”节点下。 默认情况下不会激活虚拟环境，因此请右键单击它并选择“激活环境”。
::: moniker-end

### <a name="remove-a-virtual-environment"></a>删除虚拟环境

1. 在“解决方案资源管理器”中，右键单击虚拟环境，然后选择“删除”。

1. Visual Studio 会询问是否移除或删除虚拟环境。 选择“移除”，使其对项目不可用，但在文件系统上保留它。 选择“删除”，从项目中移除环境，并从文件系统中删除它。 基础解释器不受影响。

## <a name="view-installed-packages"></a>查看已安装的包

在“解决方案资源管理器”中，展开特定环境节点以快速查看在该环境中安装的包（也就是说，你可以激活环境时在代码中导入和使用这些包）：

![解决方案资源管理器中某环境的 Python 包](media/environments/environments-installed-packages.png)

::: moniker range="vs-2017"
若要安装新包，右键单击该环境并选择“安装 Python 包”以切换到“Python 环境”窗口中的相应“包”选项卡。 输入搜索词（通常是包名称），Visual Studio 将显示匹配的包。
::: moniker-end
::: moniker range=">=vs-2019"
若要安装新包，右键单击该环境并选择“管理 Python 包”（或使用 Python 工具栏上的包按钮）以切换到“Python 环境”窗口中的相应“包”选项卡。 在“包”选项卡上，输入搜索词（通常为包名称），随后 Visual Studio 将显示匹配的包。
::: moniker-end

在 Visual Studio 中，已从[“Python 包索引 (PyPI)”](https://pypi.org)中下载适用于大多数环境的包（和依赖项），用户可以在其中搜索可用包。 Visual Studio 的状态栏和输出窗口显示有关安装的信息。 若要卸载包，请右键单击它，并选择“删除”。

Conda 包管理器通常将 `https://repo.continuum.io/pkgs/` 用作默认通道，但也可以使用其他通道。 有关详细信息，请参阅[管理通道](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-channels.html) (docs.conda.io)。

请注意，显示的项未必总准确，且安装和卸载可能不可靠或不可用。 Visual Studio 使用 pip 程序包管理器（如果可用），并且需要时会下载并安装它。 Visual Studio 还可以使用 easy_install 程序包管理器。 也会显示使用 `pip` 或 `easy_install` 从命令行安装的包。

另请注意，Visual Studio 目前不支持使用 `conda` 将包安装到 conda 环境中。 而是使用命令行中的 `conda`。

> [!Tip]
> 当包中包含用于 .pyd*\** 文件中本机组件的源代码时，pip 无法安装包，这种情况很常见。 如果没有安装要求的 Visual Studio 版本，pip 无法编译这些组件。 在此情况下显示的错误消息是：“错误：找不到 vcvarsall.bat”**。 `easy_install` 通常可下载预编译的二进制文件，且你可通过 [https://aka.ms/VCPython27](https://aka.ms/VCPython27) 下载适合旧版 Python 的编译器。 有关详细信息，请参阅 Python 工具团队博客上的[How to deal with the pain of "unable to find vcvarsallbat"](https://devblogs.microsoft.com/python/unable-to-find-vcvarsall-bat/)（如何处理“找不到 vcvarsallbat”问题）。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中管理 Python 环境](managing-python-environments-in-visual-studio.md)
- [对依赖项使用 requirements.txt](managing-required-packages-with-requirements-txt.md)
- [搜索路径](search-paths.md)
- [“Python 环境”窗口参考](python-environments-window-tab-reference.md)
