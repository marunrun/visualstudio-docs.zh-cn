---
title: Python/C++ 混合模式调试的符号
description: Visual Studio 如何为完整的混合模式 C++ 和 Python 调试提供加载符号的功能。
ms.date: 11/12/2018
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- python
- data-science
ms.openlocfilehash: 77dc73b0be050e5108f73d38dfbbaa763d236995
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62957588"
---
# <a name="install-debugging-symbols-for-python-interpreters"></a>安装用于 Python 解释器的调试符号

为了提供完整的调试体验，Visual Studio 中的 [Python 混合模式调试器](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)需要 Python 解释器（正在用于分析大量内部数据结构）的调试符号。 例如，对于 python27.dll，相应的符号文件是 python27.pdb；对于 python36.dll，符号文件是 python36.pdb     。 解释器的每个版本都提供了各种模块的符号文件。

对于 Visual Studio 2017 及更高版本，Python 3 和 Anaconda 3 解释器会自动安装各自的符号，Visual Studio 会自动找到这些符号。 对于 Visual Studio 2015 及更早版本，或使用其他解释器时，需要单独下载符号，然后通过“调试” > “符号”选项卡中的“工具” > “选项”对话框，将 Visual Studio 指向它们     。以下各节将详细介绍这些步骤。

Visual Studio 可能会在需要符号的时候（通常是在启动混合模式的调试会话时）提示你。 在这种情况下，将显示一个对话框，其中包含两个选项：

- “打开符号设置”对话框将打开“选项”对话框以转到“调试” > “符号”选项卡     。
- “为解释器下载符号”将打开当前文档页面，在这种情况下，选择“工具” > “选项”并导航到“调试” > “符号”选项卡以继续操作      。

    ![混合模式调试器符号提示](media/mixed-mode-debugging-symbols-required.png)

## <a name="download-symbols"></a>下载符号

- Python 3.5 及更高版本：通过 Python 安装程序获取调试符号。 选择“自定义安装”  ，选择“下一步”  以转到“高级选项”  ，然后选择“下载调试符号”  和“下载调试二进制文件”  这两个框：

    ![Python 3.x 安装程序包含调试符号](media/mixed-mode-debugging-symbols-installer35.png)

    将在根安装文件夹中找到符号文件 (.pdb)（各个模块的符号文件也在 DLLs 文件夹中）   。 因此，Visual Studio 会自动找到它们，不需要进一步操作。

- Python 3.4.x 及更早版本：[正式分发](#official-distributions)或 [Enthought Canopy](#enthought-canopy) 以可下载 .zip 文件的形式提供符号  。 下载后，将文件提取到本地文件夹（如 Python 文件夹内的 Symbols 文件夹）以继续操作  。

    > [!Important]
    > Python 较低版本之间，以及 32 位 和 64 位版本之间的符号都有所不同，因此需要完全匹配这些版本。 若要检查所使用的解释器，请在解决方案资源管理器中展开项目下的“Python 环境”节点，并记下环境名称    。 然后切换到“Python 环境”窗口，并记下安装位置   。 然后，在该位置打开命令窗口，并启动 python.exe，后者将显示确切版本以及版本属于 32 位还是 64 位  。

- 对于 ActiveState Python 等任何其他第三方 Python 分发，请联系该分发的作者并请求他们为你提供符号。 WinPython 部件采用了未做更改的标准 Python 器，因此请使用相应版本号的正式分发中的符号。

## <a name="point-visual-studio-to-the-symbols"></a>将 Visual Studio 指向符号

如果单独下载符号，请按照以下步骤使 Visual Studio 找到符号。 如果通过 Python 3.5 或更高版本的安装程序安装符号，Visual Studio 会自动找到它们。

1. 选择“工具” > “选项”菜单，然后导航到“调试” > “符号”     。

1. 选择工具栏上的“添加”按钮（见下文），输入在其中展开了下载的符号的文件夹位置（即 python.pdb 所在的文件夹，例如 c:\python34\Symbols，如下所示），然后选择“确定”     。

    ![混合模式调试器符号选项](media/mixed-mode-debugging-symbols.png)

1. 在调试会话期间，Visual Studio 可能还会提示你输入 Python 解释器的源文件位置。 如果已下载源文件（例如从 [python.org/downloads/](https://www.python.org/downloads/)），当然也可以指向它们。

> [!Note]
> 对话框中显示的符号缓存功能用于创建从联机源获取的符号的本地缓存。 Python 解释器符号不需要这些功能，因为符号已存在于本地。 有关任何情况的详细信息，请参阅[在 Visual Studio 调试器中指定符号和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。

## <a name="official-distributions"></a>正式分发

| Python 版本 | 下载 |
| --- | --- |
| 3.5 及更高版本 | 通过 Python 安装程序安装符号。 |
| 3.4.4 | [32 位](https://www.python.org/ftp/python/3.4.4/python-3.4.4-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.4.4/python-3.4.4.amd64-pdb.zip) |
| 3.4.3 | [32 位](https://www.python.org/ftp/python/3.4.3/python-3.4.3-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.4.3/python-3.4.3.amd64-pdb.zip) |
| 3.4.2 | [32 位](https://www.python.org/ftp/python/3.4.2/python-3.4.2-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.4.2/python-3.4.2.amd64-pdb.zip) |
| 3.4.1 | [32 位](https://www.python.org/ftp/python/3.4.1/python-3.4.1-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.4.1/python-3.4.1.amd64-pdb.zip) |
| 3.4.0 | [32 位](https://www.python.org/ftp/python/3.4.0/python-3.4.0-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.4.0/python-3.4.0.amd64-pdb.zip) |
| 3.3.5 | [32 位](https://www.python.org/ftp/python/3.3.5/python-3.3.5-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.3.5/python-3.3.5.amd64-pdb.zip) |
| 3.3.4 | [32 位](https://www.python.org/ftp/python/3.3.4/python-3.3.4-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.3.4/python-3.3.4.amd64-pdb.zip) |
| 3.3.3 | [32 位](https://www.python.org/ftp/python/3.3.3/python-3.3.3-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.3.3/python-3.3.3.amd64-pdb.zip) |
| 3.3.2 | [32 位](https://www.python.org/ftp/python/3.3.2/python-3.3.2-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.3.2/python-3.3.2.amd64-pdb.zip) |
| 3.3.1 | [32 位](https://www.python.org/ftp/python/3.3.1/python-3.3.1-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.3.1/python-3.3.1.amd64-pdb.zip) |
| 3.3.0 | [32 位](https://www.python.org/ftp/python/3.3.0/python-3.3.0-pdb.zip) - [64 位](https://www.python.org/ftp/python/3.3.0/python-3.3.0.amd64-pdb.zip) |
| 2.7.15 | [32 位](https://www.python.org/ftp/python/2.7.15/python-2.7.15-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.15/python-2.7.15.amd64-pdb.zip) |
| 2.7.14 | [32 位](https://www.python.org/ftp/python/2.7.14/python-2.7.14-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.14/python-2.7.14.amd64-pdb.zip) |
| 2.7.13 | [32 位](https://www.python.org/ftp/python/2.7.13/python-2.7.13-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.13/python-2.7.13.amd64-pdb.zip) |
| 2.7.12 | [32 位](https://www.python.org/ftp/python/2.7.12/python-2.7.12-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64-pdb.zip) |
| 2.7.11 | [32 位](https://www.python.org/ftp/python/2.7.11/python-2.7.11-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.11/python-2.7.11.amd64-pdb.zip) |
| 2.7.10 | [32 位](https://www.python.org/ftp/python/2.7.10/python-2.7.10-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.10/python-2.7.10.amd64-pdb.zip) |
| 2.7.9 | [32 位](https://www.python.org/ftp/python/2.7.9/python-2.7.9-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.9/python-2.7.9.amd64-pdb.zip) |
| 2.7.8 | [32 位](https://www.python.org/ftp/python/2.7.8/python-2.7.8-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.8/python-2.7.8.amd64-pdb.zip) |
| 2.7.7 | [32 位](https://www.python.org/ftp/python/2.7.7/python-2.7.7-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.7/python-2.7.7.amd64-pdb.zip) |
| 2.7.6 | [32 位](https://www.python.org/ftp/python/2.7.6/python-2.7.6-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.6/python-2.7.6.amd64-pdb.zip) |
| 2.7.5 | [32 位](https://www.python.org/ftp/python/2.7.5/python-2.7.5-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.5/python-2.7.5.amd64-pdb.zip) |
| 2.7.4 | [32 位](https://www.python.org/ftp/python/2.7.4/python-2.7.4-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.4/python-2.7.4.amd64-pdb.zip) |
| 2.7.3 | [32 位](https://www.python.org/ftp/python/2.7.3/python-2.7.3-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.3/python-2.7.3.amd64-pdb.zip) |
| 2.7.2 | [32 位](https://www.python.org/ftp/python/2.7.2/python-2.7.2-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.2/python-2.7.2.amd64-pdb.zip) |
| 2.7.1 | [32 位](https://www.python.org/ftp/python/2.7.1/python-2.7.1-pdb.zip) - [64 位](https://www.python.org/ftp/python/2.7.1/python-2.7.1.amd64-pdb.zip) |

## <a name="enthought-canopy"></a>Enthought Canopy

Enthought Canopy provides 从版本 1.2 开始为其二进制文件提供符号。 如之前所述，这些符号将自动与分发一起安装，但仍需向符号路径手动添加包含这些符号的文件夹。 对于 Canopy 的典型每用户安装，64 位版本的符号位于 %UserProfile%\AppData\Local\Enthought\Canopy\User\Scripts，32 位版本的符号位于 %UserProfile%\AppData\Local\Enthought\Canopy32\User\Scripts   。

Enthought Canopy 1.1 及早期版本，以及 Enthought Python 分发 (EPD) 不提供解释器符号，因此不兼容混合模式调试。
