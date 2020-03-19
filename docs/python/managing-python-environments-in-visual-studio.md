---
title: 管理 Python 环境和解释器
description: 使用 Python 环境窗口来管理全局、虚拟和 Conda 环境、安装 Python 解释器和包以及将环境分配给 Visual Studio 项目。
ms.date: 08/06/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- python
- data-science
ms.openlocfilehash: 5e269e19a09aec157e38eaf8938b5995c2647803
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79307159"
---
# <a name="how-to-create-and-manage-python-environments-in-visual-studio"></a>如何在 Visual Studio 中创建和管理 Python 环境

Python 环境  是在其中运行 Python 代码的上下文，它包括全局、虚拟和 Conda 环境。 环境由解释器、库（通常是 Python 标准库）以及一组已安装的包组成。 这些组成部分共同确定哪些语言结构和语法有效、哪些操作系统功能可访问以及哪些包可使用。

在 Windows 上的 Visual Studio 中，可使用“Python 环境”窗口（如本文中所述）管理这些环境并选择其中一个作为新项目的默认环境  。 环境的其他方面可在以下文章中找到：

- 对于任何给定的项目，可[选择特定环境](selecting-a-python-environment-for-a-project.md)而不使用默认环境。

- 有关为 Python 项目创建和使用虚拟环境的详细信息，请参阅[使用虚拟环境](selecting-a-python-environment-for-a-project.md#use-virtual-environments)。

- 如果想在环境中安装包，请参阅[“包”选项卡引用](python-environments-window-tab-reference.md#packages-tab)。

- 若要安装另一个 Python 解释器，请参阅[安装 Python 解释器](installing-python-interpreters.md)。 通常，如果下载并运行传统 Python 分发版的安装程序，Visual Studio 会检测新的安装和环境是否出现在“Python 环境”窗口中并且是否可以为项目选择它们  。

如果不熟悉 Visual Studio 中的 Python，以下文章还提供了一般背景知识：

- [在 Visual Studio 中使用 Python](overview-of-python-tools-for-visual-studio.md)
- [在 Visual Studio 中安装 Python 支持](installing-python-support-in-visual-studio.md)

::: moniker range="vs-2017"
> [!Note]
> 你无法管理使用“文件” > “打开” > “文件夹”命令仅以文件夹方式打开的 Python 代码的环境    。 但是，[从现有代码创建 Python 项目](quickstart-01-python-in-visual-studio-project-from-existing-code.md)即可享受 Visual Studio 的环境功能。
::: moniker-end

::: moniker range=">=vs-2019"
> [!Note]
> 可以使用“文件” > “打开” > “文件夹”命令管理作为文件夹打开的 Python 代码环境    。 使用 Python 工具栏，可以在所有检测到的环境之间切换，还可以添加新环境。 环境信息存储在 Workspace.vs 文件夹中的 PythonSettings.json 文件中。
::: moniker-end

## <a name="the-python-environments-window"></a>“Python 环境”窗口

Visual Studio 了解的环境显示在“Python 环境”  窗口中。 要打开该窗口，请使用以下某个方法：

- 选择“视图” > “其他窗口” > “Python 环境”菜单命令    。
- 在解决方案资源管理器中，右键单击某项目的“Python 环境”节点，选择“查看所有 Python 环境”    ：

    ::: moniker range="vs-2017"
    ![解决方案资源管理器中的“查看所有环境”命令](media/environments/environments-view-all.png)
    ::: moniker-end
    ::: moniker range=">=vs-2019"
    ![解决方案资源管理器中的“查看所有环境”命令](media/environments/environments-view-all-2019.png)
    ::: moniker-end

在任一情况下，“Python 环境”窗口将出现在解决方案资源管理器旁边   ：

::: moniker range="vs-2017"
![“Python 环境”窗口](media/environments/environments-default-view.png)
::: moniker-end
::: moniker range=">=vs-2019"
![“Python 环境”窗口](media/environments/environments-default-view-2019.png)
::: moniker-end

Visual Studio 使用注册表查找已安装的全局环境（遵循 [PEP 514 ](https://www.python.org/dev/peps/pep-0514/)），以及查找虚拟环境和 conda 环境（请参阅[环境类型](#types-of-environments)）。 如果在列表中看不到预期的环境，请参阅[手动标识现有环境](#manually-identify-an-existing-environment)。

选择列表中的环境时，Visual Studio 将在“概述”选项卡上显示该环境的各种属性和命令  。例如，可在上图中看到解释器的位置是 C:\Python36-32  。 “概述“选项卡底部的四个命令在解释器运行时分别打开一个命令提示符  。 有关详细信息，请参阅[“Python 环境”窗口选项卡引用 - 概述](python-environments-window-tab-reference.md#overview-tab)。

使用环境列表下方的下拉列表可切换到不同的选项卡，例如“包”和“IntelliSense”   。 [“Python 环境”窗口选项卡引用](python-environments-window-tab-reference.md)中也介绍了这些选项卡。

选择环境不会改变其与任何项目的关系。 Visual Studio 可将列表中以粗体显示的默认环境用于任意新项目。 要在新项目中使用不同的环境，请使用“将此作为新项目的默认环境”命令  。 在项目的上下文中，可以始终选择特定环境。 有关详细信息，请参阅[选择项目环境](selecting-a-python-environment-for-a-project.md)。

列出的每个环境右侧的控件可为此环境打开“交互”窗口  。 （在 Visual Studio 2017 15.5 及更早版本中，可能还会显示另一个控件，用于刷新此环境的 IntelliSense 数据库。 有关数据库的详细信息，请参阅[“环境”窗口选项卡引用](python-environments-window-tab-reference.md)。）

::: moniker range="vs-2017"
> [!Tip]
> 如果将“Python 环境”  窗口展开到足够宽，可以获得更加完整的环境视图，从而可使操作更加便捷。
>
> ![“Python 环境”窗口扩展后的视图](media/environments/environments-expanded-view.png)
::: moniker-end

::: moniker range=">=vs-2019"
> [!Tip]
> 如果将“Python 环境”  窗口展开到足够宽，可以获得更加完整的环境视图，从而可使操作更加便捷。
>
> ![“Python 环境”窗口扩展后的视图](media/environments/environments-expanded-view-2019.png)
::: moniker-end

> [!Note]
> 尽管 Visual Studio 遵循系统-站点-包选项，但它没有提供从 Visual Studio 中更改它的方法。

### <a name="what-if-no-environments-appear"></a>如果未出现环境该怎么办？

如果未出现任何环境，这意味着 Visual Studio 在标准位置中未能检测到任何 Python 安装。 例如，你可能已安装 Visual Studio 2017 或更高版本但清除了 Python 工作负载的安装程序选项中的所有解释器选项。 同样地，你可能已安装 Visual Studio 2015 或更早版本，但未手动安装解释器（请参阅[安装 Python 解释器](installing-python-interpreters.md)）。

如果知道计算机上有一个 Python 解释器，但 Visual Studio（任何版本）未检测到它，则使用“+ 自定义”命令来手动指定其位置  。 请参阅下一节[手动标识现有环境](#manually-identify-an-existing-environment)。

> [!Tip]
> Visual Studio 可检测现有解释器的更新，如使用 python.org 的安装程序将 Python 2.7.11 升级到 2.7.14。在安装过程中，较旧的环境从“Python 环境”  列表消失后，更新才会显示在其位置上。
>
> 但是，如果你使用文件系统手动移动解释器及其环境，则 Visual Studio 不会知道新位置。 有关详细信息，请参阅[移动解释器](installing-python-interpreters.md#move-an-interpreter)。

### <a name="types-of-environments"></a>环境类型

Visual Studio 可使用全局、虚拟和 conda 环境。

#### <a name="global-environments"></a>全局环境

每个 Python 安装（例如，Python 2.7、Python 3.6、Python 3.7 和 Anaconda 4.4.0 等，请参阅[安装 Python 解释器](installing-python-interpreters.md)）都会维护自己的全局环境  。 每个环境都包括特定的 Python 解释器、其标准库和一组预安装包以及在激活该环境时安装的任何其他包。 将包安装到全局环境使其适用于使用此环境的所有项目。 如果环境位于文件系统的保护区域内（例如，c:\program files 内），则安装包时需要管理员权限  。

全局环境适用于计算机上的所有项目。 在 Visual Studio 中，选择一个全局环境作为默认环境，此环境可用于所有项目，除非为项目专门选择了其他环境。 有关详细信息，请参阅[选择项目环境](selecting-a-python-environment-for-a-project.md)。

#### <a name="virtual-environments"></a>虚拟环境

虽然使用全局环境是一种简单的入门方式，但随着时间的推移，该环境中将充斥着你为不同项目安装的许多不同的包。 这使得很难根据已知版本的一组特定包对应用程序进行彻底测试，而这正是你在生成服务器或 Web 服务器上设置的环境。 当两个项目需要不兼容的包或相同包的不同版本时，也会发生冲突。

因此，开发人员通常会为项目创建虚拟环境  。 虚拟环境是项目中的子文件夹，其中包含特定解释器的副本。 激活虚拟环境时，任何安装的包仅安装在环境的子文件夹中。 然后，当你在该环境中运行 Python 程序时，便知道它仅针对那些特定的包运行。

Visual Studio 为创建项目的虚拟环境提供直接支持。 例如，如果打开包含 requirements.txt 的项目，或者通过包含该文件的模板创建项目，Visual Studio 会提示你自动创建虚拟环境并安装这些依赖项  。

在打开的项目中，可随时创建新的虚拟环境。 在“解决方案资源管理器”中，展开项目节点，右键单击“Python 环境”并选择“添加虚拟环境”   。 有关详细信息，请参阅[创建虚拟环境](/visualstudio/python/selecting-a-python-environment-for-a-project?view=vs-2019#create-a-virtual-environment-1)。

Visual Studio 还提供可从虚拟环境生成 requirements.txt 文件的命令，简化了在其他计算机上重新创建环境的过程  。 有关详细信息，请参阅[使用虚拟环境](selecting-a-python-environment-for-a-project.md#use-virtual-environments)。

#### <a name="conda-environments"></a>Conda 环境

Conda 环境是使用 `conda` 工具或通过 Visual Studio 2017 版本 15.7 及更高版本中的集成式 Conda 管理创建的环境。 （需要 Anaconda 或 Miniconda；它们可通过 Visual Studio 安装程序获得，请参阅[安装](installing-python-support-in-visual-studio.md#visual-studio-2019-and-visual-studio-2017)。）

::: moniker range="vs-2017"

1. 选择“Python 环境”窗口中的“+ 创建 Conda 环境”，这将打开“新建 Conda 环境”选项卡    ：

    ![创建新 Conda 环境的选项卡](media/environments/environments-conda-1.png)

1. 在“名称”字段中输入环境名称，在“Python”字段中选择基础 Python 解释器，然后选择“创建”    。

1. “输出”窗口显示新环境的创建进度，创建完成后将显示几条 CLI 指令  ：

    ![成功创建 Conda 环境](media/environments/environments-conda-2.png)

1. 如[为项目选择环境](selecting-a-python-environment-for-a-project.md)中所述，在 Visual Studio 中，可像激活任何其他环境一样，为项目激活 Conda 环境。

1. 若要在环境中安装包，请使用[包选项卡](python-environments-window-tab-reference.md#packages-tab)。
::: moniker-end

::: moniker range=">=vs-2019"

1. 在“Python 环境”窗口中（或从 Python 工具栏上）选择“+ 添加环境”   ，这将打开“添加环境”  对话框。 在该对话框中，选择“Conda 环境”  选项卡：

    ![“添加环境”对话框中的“Conda 环境”选项卡](media/environments/environments-conda-1-2019.png)

1. 配置以下字段：

    | 字段 | 描述 |
    | --- | --- |
    | 项目 | 要在其中创建环境的项目（如果在同一 Visual Studio 解决方案中有多个项目）。 |
    | “属性” | Conda 环境的名称。 |
    | 添加包 | 如果你有描述依赖项的 environment.yml 文件，请选择“环境文件”   ，或选择“一个或多个 Anaconda 包名称”  并在下面的字段中列出至少一个 Python 包或 Python 版本。 包列表可指示 conda 创建 Python 环境。 若要安装最新版本的 Python，请使用 `python`；若要安装特定版本，请使用 `python=,major>.<minor>`，如 `python=3.7` 所述。 还可以使用包按钮从一系列菜单中选择 Python 版本和常见包。 |
    | 设置为当前环境 | 创建环境后，在所选项目中激活新环境。 |
    | 设置为新项目的默认环境 | 自动设置和激活 Visual Studio 中创建的任何新项目中的 conda 环境。 此选项与使用“Python 环境”窗口中的“将此作为新项目的默认环境”相同   。 |
    | 在“Python 环境”窗口中查看 | 指定是否在创建环境后显示“Python 环境”  窗口。 |

    > [!Important]
    > 在创建 conda 环境时，请务必使用 `environments.yml` 或包列表指定至少一个 Python 版本或 Python 包，确保环境包含 Python 运行时。 否则，Visual Studio 将忽略环境：环境不显示在“Python 环境”  窗口中的任何位置，不能设置为一个项目的当前环境，并且不可用作全局环境。
    >
    > 如果碰巧创建没有指定 Python 版本的 conda 环境，请使用 `conda info` 命令查看 conda 环境文件夹的位置，然后从该位置手动删除该环境的子文件夹。

1. 选择“创建”  ，并在“输出”  窗口中观察进度。 创建完成后，输出将附带几项 CLI 说明：

    ![成功创建 Conda 环境](media/environments/environments-conda-2-2019.png)

1. 如[为项目选择环境](selecting-a-python-environment-for-a-project.md)中所述，在 Visual Studio 中，可像激活任何其他环境一样，为项目激活 Conda 环境。

1. 若要在环境中安装其他包，请使用[“包”选项卡](python-environments-window-tab-reference.md#packages-tab)。
::: moniker-end

> [!Note]
> 为获得 Conda 环境的最佳使用结果，请使用 Conda 4.4.8 或更高版本（Conda 版本与 Anaconda 版本不同）。 可以通过 Visual Studio 安装程序安装合适版本的 Miniconda (Visual Studio 2019) 和 Anaconda (Visual Studio 2017)。

若要查看 Conda 版本、Conda 环境的存储位置以及其他信息，请在 Anaconda 命令提示符（即路径中包含 Anaconda 的命令提示符）运行 `conda info`：

```cli
conda info
```

conda 环境文件夹如下所示：

```output
       envs directories : C:\Users\user\.conda\envs
                          c:\anaconda3\envs
                          C:\Users\user\AppData\Local\conda\conda\envs
```

由于未使用项目存储 Conda 环境，这些环境与全局环境的功能类似。 例如，将新包安装到 Conda 环境，从而使该包适用于使用此环境的所有项目。

对于 Visual Studio 2017 版本 15.6 及更早版本，可以根据[手动标识现有环境](#manually-identify-an-existing-environment)中所述，通过手动指向 Conda 环境进行使用。

根据下一节所述，Visual Studio 2017 版本 15.7 及更高版本自动检测 Conda 环境，并在“Python 环境”窗口中显示这些环境  。

## <a name="manually-identify-an-existing-environment"></a>手动标识现有环境

使用以下步骤来标识安装在非标准位置的环境（包括 Visual Studio 2017 版本 15.6 及更早版本中的 Conda 环境）：

::: moniker range="vs-2017"

1. 选择“Python 环境”  窗口中的“+ 自定义”  ，这将打开“配置”  选项卡：

    ![新自定义环境的默认视图](media/environments/environments-custom-1.png)

1. 在“说明”  字段中为该环境输入名称。

1. （使用“...”）在“前缀路径”字段中输入或浏览解释器的路径   。

1. 如果 Visual Studio 监测到此位置存在 Python 解释器（如下所示的 conda 环境的路径），它将启用“自动检测”命令  。 选择“自动检测”填写剩余的字段  。 你还可以手动填写这些字段。

    ![启用“自动检测”命令](media/environments/environments-custom-2.png)

    ![使用“自动检测”后填写环境字段](media/environments/environments-custom-3.png)

1. 如果字段包含所需的值，则选择“应用”  保存配置。 现在你可以在 Visual Studio 中使用像任何其他环境一样的环境了。

1. 如果需要删除手动标识的环境，请在“配置”  选项卡上选择“删除”  命令。自动检测环境不提供此选项。 有关更多信息，请参阅[配置选项卡](python-environments-window-tab-reference.md#configure-tab)。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在“Python 环境”窗口中（或从 Python 工具栏上）选择“+ 添加环境”   ，这将打开“添加环境”  对话框。 在该对话框中，选择“现有环境”  选项卡：

    ![“添加环境”对话框中的“现有环境”选项卡](media/environments/environments-custom-1-2019.png)

1. 选择“环境”  下拉列表，然后选择“自定义”  ：

    ![“添加环境”对话框中的“自定义环境”选项](media/environments/environments-custom-2-2019.png)

1. 在对话框中提供的字段中，输入或浏览（使用 ...  ）到“前缀路径”下的解释器路径  ，它将填充大多数其他字段。 在检查这些值并根据需要修改后，选择“添加”  。 

    ![用于在“添加环境”对话框中指定自定义环境选项详细信息的字段](media/environments/environments-custom-3-2019.png)

1. 可在“Python 环境”窗口中随时检查和修改环境的详细信息  。 在该窗口中，选择环境，然后选择“配置”  选项卡。进行更改后，选择  “应用”命令。 还可以使用“删除”  命令（对自动检测的环境不可用）删除环境。 有关更多信息，请参阅[配置选项卡](python-environments-window-tab-reference.md#configure-tab)。
::: moniker-end

## <a name="fix-or-delete-invalid-environments"></a>修复或删除无效环境

如果 Visual Studio 找到环境的注册表项，但解释器的路径无效，则“Python 环境”窗口将显示标有删除线字体的名称  ：

::: moniker range="vs-2017"
![“Python 环境”窗口显示无效环境](media/environments/environments-invalid-entry.png)
::: moniker-end
::: moniker range=">=vs-2019"
![“Python 环境”窗口显示无效环境](media/environments/environments-invalid-entry-2019.png)
::: moniker-end

若要更正希望保留的环境，首先请尝试使用其安装程序的“修复”进程  。 例如，标准 Python 3.x 的安装程序包含该选项。

若要更正没有修复选项的环境，或删除无效环境，请使用以下步骤直接修改注册表。 更改注册表后，Visual Studio 会自动更新“Python 环境”窗口  。

1. 运行 Regedit.exe  。
1. 导航到 HKEY_LOCAL_MACHINE\SOFTWARE\Python  。 对于 IronPython，则请查找 IronPython  。
1. 展开与分发匹配的节点，例如 CPython 为 PythonCore 或 Anaconda 为 ContinuumAnalytics   。 对于 IronPython，请展开版本号节点。
1. 检查 InstallPath 节点下的值  ：

    ![典型 CPython 安装的注册表项](media/environments/environments-registry-entries.png)

    - 如果计算机上仍存在该环境，请将 ExecutablePath 的值更改为正确位置  。 还根据需要更正“(默认)”值和 WindowedExecutablePath 值   。
    - 如果计算机上不再存在该环境，且想将其从“Python 环境”窗口中删除，请删除 InstallPath 的父节点，例如上图中的 3.6    。

## <a name="see-also"></a>请参阅

- [安装 Python 解释器](installing-python-interpreters.md)
- [为项目选择解释器](selecting-a-python-environment-for-a-project.md)
- [对依赖项使用 requirements.txt](managing-required-packages-with-requirements-txt.md)
- [搜索路径](search-paths.md)
- [“Python 环境”窗口参考](python-environments-window-tab-reference.md)
