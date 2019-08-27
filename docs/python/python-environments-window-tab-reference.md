---
title: Python 环境窗口引用
description: 在 Visual Studio 的 Python 环境窗口中出现的每个选项卡的详细信息。
ms.date: 03/18/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 578f73aabfb8b5a4c8336c8611f634b8947c8885
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62784945"
---
# <a name="python-environments-window-tabs-reference"></a>“Python 环境”窗口选项卡引用

打开“Python 环境”窗口：

- 选择“查看” > “其他窗口” > “Python 环境”菜单命令。
- 在解决方案资源管理器中，右键单击某项目的“Python 环境”节点，选择“查看所有 Python 环境”。

如果将“Python 环境”窗口展开到足够宽，这些选项将显示为选项卡，更便于使用。 为清楚起见，本文中的选项卡显示在扩展后的视图中。

::: moniker range="vs-2017"
![“Python 环境”窗口扩展后的视图](media/environments/environments-expanded-view.png)
::: moniker-end
::: moniker range=">=vs-2019"
![“Python 环境”窗口扩展后的视图](media/environments/environments-expanded-view-2019.png)
::: moniker-end

## <a name="overview-tab"></a>概述选项卡

为环境提供基本信息和命令：

::: moniker range="vs-2017"
![Python 环境概述选项卡](media/environments/environments-overview-tab.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Python 环境概述选项卡](media/environments/environments-overview-tab-2019.png)
::: moniker-end

| 命令 | 说明 |
| --- | --- |
| **使此环境成为新项目的默认环境** | 设置活动环境，这可能会导致 Visual Studio（2017 版本 15.5 及更高版本）在加载 IntelliSense 数据库时短时间无响应。 含有多个包的环境可能无响应的时间更长。 |
| **访问分发服务器的网站** | 打开浏览器，访问 Python 分发所提供的 URL。 例如，对于 Python 3.x，会转到 python.org。 |
| **打开交互窗口** | 在 Visual Studio 中为此环境打开[交互 (REPL) 窗口](python-interactive-repl-in-visual-studio.md)，应用任何[启动脚本（见下文）](#startup-scripts)。 |
| **浏览交互式脚本** | 请参阅[启动脚本](#startup-scripts)。 |
| **使用 IPython 交互模式** | 设置后，将默认使用 IPython 打开交互窗口。 这样会启用内联绘图及扩展的 IPython 语法（如 `name?`）来查看 shell 命令的帮助和 `!command`。 建议在使用 Anaconda 分发时使用此选项，因为该选项需要额外的包。 有关详细信息，请参阅[在交互窗口中使用 IPython](interactive-repl-ipython.md)。 |
| **在 PowerShell 中打开** | 在 PowerShell 命令窗口中启动解释器。 |
| （文件夹和项目链接） | 提供对环境的安装文件夹、python.exe 解释器和 pythonw.exe 解释器的快速访问。 第一个会在 Windows 资源管理器中打开，后两个会打开控制台窗口。 |

### <a name="startup-scripts"></a>启动脚本

在日常工作流中使用交互窗口时，可能会开发定期使用的帮助器函数。 例如，可以创建用于在 Excel 中打开 DataFrame 的函数，然后将该代码保存为启动脚本，这样便始终可在交互窗口中使用该代码。

启动脚本包含交互窗口自动加载并运行的代码，包括导入、函数定义及任何其他文字内容。 此类脚本通过以下两种方式引用：

1. 安装环境时，Visual Studio 会创建文件夹 Documents\Visual Studio \<version>\Python Scripts\\\<environment>，其中 &lt;version&gt; 为 Visual Studio 版本（如 2017 或 2019），&lt;environment&gt; 对应环境的名称。 可以使用“浏览交互式脚本”命令轻松地导航到特定于环境的文件夹。 启动该环境的交互窗口时，它会按字母顺序加载和运行在此处找到的任何 .py 文件。

1. “工具” > “选项” > “Python” > “交互窗口”选项卡中的“脚本”控件（请参阅[交互窗口选项](python-support-options-and-settings-in-visual-studio.md#interactive-windows-options)）用于为所有环境中加载和运行的启动脚本指定另一个文件夹。 但是，此功能目前无效。

## <a name="configure-tab"></a>配置选项卡

如果可用，”配置”选项卡包含如下表中所述的详细信息。 如果此选项卡不显示，意味着 Visual Studio 自动管理所有详细信息。

::: moniker range="vs-2017"
![Python 环境配置选项卡](media/environments/environments-configure-tab.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Python 环境配置选项卡](media/environments/environments-configure-tab-2019.png)
::: moniker-end

| 字段 | 说明 |
| --- | --- |
| **说明** | 为环境提供的名称。 |
| **前缀路径** | 解释程序的基本文件夹位置。 通过填写此值并单击“自动检测”，Visual Studio 会尝试填充其他字段。 |
| **解释器路径** | 解释器可执行文件的路径，通常是前缀路径后加 python.exe |
| **窗口化解释器** | 非控制台可执行文件的路径，通常是前缀路径后加 pythonw.exe。 |
| **库路径**<br/>（如果可用） | 指定标准库的根，但如果 Visual Studio 能够从解释器请求更准确的路径，可能会忽略此值。 |
| **语言版本** | 从下拉菜单中选择。 |
| **体系结构** | 通常自动检测并进行填充，否则指定 32 位或 64 位。 |
| **路径环境变量** | 解释器用来查找搜索路径的环境变量。 启动 Python 时 Visual Studio 更改该变量的值，使其包含项目的搜索路径。 此属性通常应设置为 PYTHONPATH，但某些解释器使用不同的值。 |

## <a name="packages-tab"></a>包选项卡

在先前版本中还标记为“pip”。

使用 pip（“包(PyPI)”选项卡）或 conda（对于 Visual Studio 2017 版本 15.7 及更高版本的 conda 环境，为“包(Conda)”选项卡）管理环境中安装的程序包。 在此选项卡中，还可以搜索并安装新的程序包，包括其依赖项。

将显示已安装的程序包，并带有更新（向上箭头）和卸载（圈圈中的 X）程序包的控件：

![Python 环境包选项卡](media/environments/environments-pip-tab-controls.png)

输入搜索词筛选已安装的程序包的列表以及可从 PyPI 中安装的程序包。

::: moniker range="vs-2017"
![可以搜索“num”的 Python 环境程序包选项卡](media/environments/environments-pip-tab.png)
::: moniker-end
::: moniker range=">=vs-2019"
![可以搜索“num”的 Python 环境程序包选项卡](media/environments/environments-pip-tab-2019.png)
::: moniker-end

正如上图所示，搜索结果显示大量与搜索项匹配的包；但是，列表中第一项是直接运行 pip install \<name> 的命令。 如果位于“包(Conda)”选项卡上，则请参阅 conda install \<name>：

::: moniker range="vs-2017"
![显示 conda 安装命令的 Conda 包选项卡](media/environments/environments-conda-tab-install.png)
::: moniker-end
::: moniker range=">=vs-2019"
![显示 conda 安装命令的 Conda 包选项卡](media/environments/environments-conda-tab-install-2019.png)
::: moniker-end

在这两种情况下，可以在包名称后的搜索框中添加参数，进而自定义安装。 包含自变量时，搜索结果显示 pip install 或 conda install，后跟搜索框内容：

::: moniker range="vs-2017"
![在 pip 和 conda 安装命令上使用参数](media/environments/environments-pip-tab-arguments.png)
::: moniker-end
::: moniker range=">=vs-2019"
![在 pip 和 conda 安装命令上使用参数](media/environments/environments-pip-tab-arguments-2019.png)
::: moniker-end

安装一个包会在文件系统上环境的 Lib 文件中创建子文件夹。 例如，如果在 c:\Python36 中安装了 Python 3.6，则包安装在 c:\Python36\Lib 中，如果在 c:\Program Files\Anaconda3 上安装了 Anaconda3，则包安装在 c:\Program Files\Anaconda3\Lib 中。 对于 conda 环境，程序包安装在该环境的文件夹中。

### <a name="grant-administrator-privileges-for-package-install"></a>授予管理员包安装权限

将包安装到位于文件系统保护区域（例如 c:\Program Files\Anaconda3\Lib）的环境中时，Visual Studio 必须运行提升的 `pip install` 以允许它创建包子文件夹。 需要提升时，Visual Studio 会显示提示，“可能需要管理员权限才能安装、更新或删除此环境的包”：

![针对包安装的提升提示](media/environments/environments-pip-elevate.png)

“立刻提升”会将管理权限授予单个操作的 pip，同时取决于任何操作系统的权限提示。 选择“在没有管理员权限的情况下继续”会尝试安装该包，但尝试创建文件夹时 pip 会失败，显示输出，例如：“错误: 无法创建 'C:\Program Files\Anaconda3\Lib\site-packages\png.py':权限被拒绝。”

选择“安装或删除包时始终提升”可防止针对相应环境出现该对话框。 若要再次显示该对话框，请转到“工具” > “选项” > “Python” > “常规”，选择“重置所有永久隐藏的对话框”按钮。

在同一“选项”选项卡上，还可以选择“始终以管理员身份运行 pip”，针对所有环境禁止显示该对话框。 请参阅[选项 - “常规”选项卡](python-support-options-and-settings-in-visual-studio.md#general-options)。

### <a name="security-restrictions-with-older-versions-of-python"></a>较旧版本 Python 的安全限制

使用 Python 2.6、3.1 和 3.2 时，Visual Studio 显示警告“由于新的安全限制，来自 Internet 的安装可能不适用于此 Python 版本”：

![有关较旧版本 Python 的 pip 安装限制的消息](media/environments/environments-old-version-restriction.png)

警告出现的原因为：在这些较旧版本的 Python 中，`pip install` 不支持传输安全性层 (TLS) 1.2，而这是从包源 pypi.org 下载包的必需内容。自定义 Python 版本可能支持 `pip install` 可在其中正常工作的 TLS 1.2。

或许可以从 [bootstrap.pypa.io](https://bootstrap.pypa.io/) 下载包的相应 get-pip.py，手动从 [pypi.org](https://pypi.org/) 下载包，然后从该本地副本安装包。

但是，建议只需升级到 Python 2.7 或 3.3+，这样不会出现警告。

::: moniker range="vs-2017"
## <a name="intellisense-tab"></a>IntelliSense 选项卡

显示 IntelliSense 完成数据库的当前状态：

![Python 环境 IntelliSense 选项卡](media/environments/environments-intellisense-tab.png)

- 在 Visual Studio 2017 15.5 及更早版本中，IntelliSense 完成依赖于为该库编译的数据库。 安装库后，将在后台生成数据库，但可能需要一些时间，并且可能在开始编写代码时此过程还未完成。
- Visual Studio 2017 15.6 及更高版本默认使用更快的方法提供不依赖于数据库的完成。 因此，选项卡标记为“IntelliSense [数据库已禁用]”。 可通过清除选项“工具” > “选项” > “Python” > “实验性” > “针对环境使用新样式 IntelliSense”启用该数据库。

Visual Studio 检测到新环境（或添加一个）时，它会通过分析库源文件，自动开始编译数据库 。 此过程可能会花一分钟到一小时不等或者更多时间，具体取决于安装的组件。 （例如，Anaconda 随附了许多库，需要花费一些时间来编译该数据库。）完成后，会获得 IntelliSense 的详细信息，并且在安装更多库之前，无需再次刷新数据库（使用“刷新 DB”按钮）。

其中数据尚未编译的库将使用 **!** 标记；如果环境的数据库未完成，则 **!** 也会出现在主环境列表中该环境的旁边。

::: moniker-end

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中管理 Python 环境](managing-python-environments-in-visual-studio.md)
- [为项目选择解释器](selecting-a-python-environment-for-a-project.md)
- [对依赖项使用 requirements.txt](managing-required-packages-with-requirements-txt.md)
- [搜索路径](search-paths.md)
