---
title: 如何应用 Python 搜索路径
description: Visual Studio 提供了一种更具体的方法来指定环境和项目的搜索路径，以避免使用系统范围的变量。
ms.date: 03/13/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 3a23afff970405bf7ae1bbd1c8aad326eb133780
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520375"
---
# <a name="how-visual-studio-uses-python-search-paths"></a>Visual Studio 如何使用 Python 搜索路径

借助典型的 Python 用法，`PYTHONPATH` 环境变量（或 `IRONPYTHONPATH` 等）可为模块文件提供默认搜索路径。 也就是说，当使用 `from <name> import...` 或 `import <name>` 语句时，Python 会搜索下列位置以获得匹配的名称：

1. Python 的内置模块。
1. 包含正在运行的 Python 代码的文件夹。
1. 适用环境变量定义的“模块搜索路径”。 （请参阅核心 Python 文档中的[模块搜索路径](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)和[环境变量](https://docs.python.org/2/using/cmdline.html#envvar-PYTHONPATH)。）

但 Visual Studio 会忽略搜索路径环境变量，即使已为整个系统设置了该变量。 实际上，此变量被忽略的具体原因是整个系统都设置了此变量，从而引发了一些无法自动解答的问题，例如引用的模块是适用于 Python 2.7 还是 Python 3.6+  。 它们是否将替代标准库模块？ 开发人员是否注意到此行为，或者它是一个恶意的攻击尝试？

因此，Visual Studio 提供了一种方法，可直接在环境和项目中指定搜索路径。 在 Visual Studio 中运行或调试的代码会接收 `PYTHONPATH` 值（和其他等效变量）中的搜索路径。 通过添加搜索路径，Visual Studio 会在需要时检查这些位置中的库并为它们构建 IntelliSense 数据库（Visual Studio 2017 版本 15.5 及更早版本；构建数据库需要一些时间，具体取决于库的数量）。

若要添加搜索路径，请转到“解决方案资源管理器”，展开项目节点，右键单击搜索路径，选择“将文件夹添加到搜索路径”    ：

::: moniker range="vs-2017"
![解决方案资源管理器中搜索路径上的“将文件夹添加到搜索路径”命令](media/search-paths-command.png)
::: moniker-end
::: moniker range=">=vs-2019"
![解决方案资源管理器中搜索路径上的“将文件夹添加到搜索路径”命令](media/search-paths-command-2019.png)
::: moniker-end

该命令显示你之后在其中选择要包含的文件夹的浏览器。

如果 `PYTHONPATH` 环境变量已包括所需文件夹，请使用“将 PYTHONPATH 添加到搜索路径”作为方便的快捷方式  。

一旦文件夹添加到搜索路径，Visual Studio 将对与该项目关联的任何环境使用这些路径。 （如果环境基于 Python 3，在尝试将搜索路径添加到 Python 2.7 模块时，可能会发生错误。）

选择“将 Zip 存档添加到搜索路径”命令，还可将带有 .zip 或 .egg 扩展名的文件添加为搜索路径    。 与文件夹一样，将扫描这些文件的内容，并使其对 IntelliSense 可用。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中管理 Python 环境](managing-python-environments-in-visual-studio.md)
- [为项目选择解释器](selecting-a-python-environment-for-a-project.md)
- [对依赖项使用 requirements.txt](managing-required-packages-with-requirements-txt.md)
- [“Python 环境”窗口参考](python-environments-window-tab-reference.md)
