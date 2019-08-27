---
title: 管理外部工具
ms.date: 11/20/2017
ms.topic: conceptual
f1_keywords:
- vs.externaltools
helpviewer_keywords:
- external tools [Visual Studio]
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3562ed9ebf2d62ab002ac227486218c8c38ad337
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62535668"
---
# <a name="manage-external-tools"></a>管理外部工具

可以使用“工具”菜单从 Visual Studio 内部调用外部工具。 “工具”菜单上提供了几个默认工具，但你也可以通过添加自己的其他可执行文件来自定义该菜单。

## <a name="tools-available-on-the-tools-menu"></a>“工具”菜单中提供的工具

“工具”菜单包含若干内置命令，包括：

::: moniker range="vs-2017"

* 用于[管理 Visual Studio 扩展](finding-and-using-visual-studio-extensions.md)的“扩展和更新”
* 用于[整理代码片段](code-snippets.md)的“代码片段管理器”
* 用于[自定义菜单和工具栏](how-to-customize-menus-and-toolbars-in-visual-studio.md)的“自定义”
* 用于[为 Visual Studio IDE 和其他工具设置各种不同选项](reference/options-dialog-box-visual-studio.md)的“选项”

::: moniker-end

::: moniker range=">=vs-2019"

* 用于[整理代码片段](code-snippets.md)的“代码片段管理器”
* 用于[自定义菜单和工具栏](how-to-customize-menus-and-toolbars-in-visual-studio.md)的“自定义”
* 用于[为 Visual Studio IDE 和其他工具设置各种不同选项](reference/options-dialog-box-visual-studio.md)的“选项”

::: moniker-end

## <a name="add-new-tools-to-the-tools-menu"></a>将新工具添加到“工具”菜单

可以添加将在“工具”菜单中显示的外部工具。

1. 通过选择“工具” > “外部工具”，打开“外部工具”对话框。

1. 单击“添加”，然后填写信息。 例如，以下条目会导致 Windows 资源管理器在当前已在 Visual Studio 中打开的文件目录中打开：

   * 标题：`Open File Location`

   * 命令：`explorer.exe`

   * 参数：`/root, "$(ItemDir)"`

   ![“外部工具”对话框](media/external-tools-dialog.png)

以下是在定义外部工具时可以使用的参数的完整列表：

|name|参数|说明|
|----------|--------------|-----------------|
|项路径|$(ItemPath)|当前文件的完整文件名（驱动器 + 路径 + 文件名）。|
|项目录|$(ItemDir)|当前文件的目录（驱动器 + 路径）。|
|项文件名|$(ItemFilename)|当前文件的文件名（文件名）。|
|项扩展名|$(ItemExt)|当前文件的文件扩展名。|
|当前行|$(CurLine)|代码窗口中光标的当前行位置。|
|当前列|$(CurCol)|代码窗口中光标的当前列位置。|
|当前文本|$(CurText)|选定的文本。|
|目标路径|$(TargetPath)|要生成的项的完整文件名（驱动器 + 路径 + 文件名）。|
|目标目录|$(TargetDir)|要生成的项的目录。|
|Target Name|$(TargetName)|要生成的项的文件名。|
|目标扩展名|$(TargetExt)|要生成的项的文件扩展名。|
|二进制目录|$(BinDir)|正在生成的二进制文件的最终位置（定义为驱动器 + 路径）。|
|项目目录|$(ProjectDir)|当前项目的目录（驱动器 + 路径）。|
|项目文件名|$(ProjectFileName)|当前项目的文件名（驱动器 + 路径 + 文件名）。|
|解决方案目录|$(SolutionDir)|当前解决方案的目录（驱动器 + 路径）。|
|解决方案文件名|$(SolutionFileName)|当前解决方案的文件名（驱动器 + 路径 + 文件名）。|

> [!NOTE]
> IDE 状态栏会显示“当前行”和“当前列”变量，用于指示插入点在活动代码编辑器中的位置。 “当前文本”变量返回在该位置选择的文本或代码。

## <a name="see-also"></a>请参阅

- [C/C++ 生成工具](/cpp/build/reference/c-cpp-build-tools)
