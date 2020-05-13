---
title: 适用于 R 的变量资源管理器
description: Visual Studio 中的变量资源管理器显示当前 R 会话中给定作用域中的所有变量。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 799b7f2789898e0d02d9588f9a3ad7d1e8098a00
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62809777"
---
# <a name="variable-explorer"></a>变量资源管理器

“变量资源管理器”窗口可通过使用“R 工具” > “窗口” > “变量资源管理器”（如果使用了“R 工具” > “数据科学设置”，则可使用 Ctrl+8）打开，显示当前 R 会话中给定范围的所有变量         。 例如，如果已打开“变量资源管理器”，并在[交互窗口](interactive-repl-for-r-in-visual-studio.md)输入以下行  ：

```R
x <- 42
y <- 43
n <- c(1,2,3,5,8,13)
```

则会出现“变量资源管理器”窗口，如下所示  ：

![Visual Studio 中的“变量资源管理器”窗口](media/variable-explorer-window.png)

如果在会话中定义了更复杂的 R 数据帧，则可在数据中导航。 例如，运行 `cars <- mtcars` 后，可展开“变量资源管理器”中的不同节点，浏览数据集  ：

![变量资源管理器的展开视图](media/variable-explorer-expanded-results.png)

若要删除变量，请右键单击并选择“删除”，或选择该变量，然后按 Delete 键   。

还可使用渐进式搜索在数据帧中搜索观察。 首先，在数据帧中展开要搜索的节点，然后在搜索框中输入搜索项。

## <a name="details-table-view"></a>详细信息（表）视图

由于数据通常是表格形式，因此可以通过选择放大镜图标或右键单击并选择“显示详细信息”  ，以单独表格形式查看复杂数据类型。

![“变量资源管理器”表视图](media/variable-explorer-table-view.png)

单击列标题按列对数据排序（在升序和降序之间切换）。 按下 Shift 并单击其他列，也会将这些列添加到排序中  。 单击列（不按 Shift）将返回单列排序  。

单击列标题的顺序决定了执行排序的顺序。 例如，按住 Shift+单击“cyl”列，然后按住 Shift+单击“mpg”列两次，该操作将对列表中的气缸数进行升序排序，对每加仑行驶英里数进行降序排序       ：

![按两列排序的数据表视图。](media/variable-explorer-table-view-sorting.png)

因为“变量资源管理器”和表视图位于不同 Visual Studio 窗口，因此可随意安排以进行并排处理  。 请参阅[自定义 Visual Studio 中的窗口布局](../ide/customizing-window-layouts-in-visual-studio.md)，了解常规说明。

## <a name="open-in-excel-or-other-csv-capable-application"></a>在 Excel（或其他支持 CSV 的应用程序）中打开

为了进行进一步的操作和分析，可将会话变量导出为 CSV。 通过“变量资源管理器”中每个节点旁的小 Excel 图标（![Excel 导出图标](media/variable-explorer-excel-icon.png)），或者通过右键单击项并选择“在 CSV 应用中打开”即可完成导出   。 选择该图标即可将数据写入 %userprofile%\Documents\RTVS_CSV_Exports 文件夹中的新 CSV 文件，然后启动该文件，在与 .csv 扩展名关联的所有应用程序中打开该文件   。

## <a name="scopes"></a>范围

默认情况下，“变量资源管理器”向全局范围开放  。 可从窗口顶部的下拉列表中选择包，切换到包范围。

![显示包范围的变量资源管理器](media/variable-explorer-package-scopes.png)

在调试器断点处停止时，也可切换到函数范围（请注意，“变量资源管理器”不会自动切换到被调试代码的函数范围）  ：

![在调试过程中显示数据帧的变量资源管理器](media/variable-explorer-as-locals-window.png)

在调试器中逐行执行代码时（例如在函数中显示局部变量），“变量资源管理器”可自动更改函数范围  。

## <a name="import-data-into-variable-explorer"></a>将数据导入变量资源管理器

“变量资源管理器”工具栏上的两个命令（也可通过“R 工具” > “数据”菜单提供）将外部 CSV 数据集导入 R 会话：    “从 Web URL 将数据集导入 R 会话”和“从文本文件将数据集导入 R 会话”   。

确定要导入的 CSV 文件后，Visual Studio 会显示一个“导入数据集”对话框，在其中可以选择数据文件的解析方式（即，采用什么字段分隔符以及如何处理引号）  。 还可以预览导入的数据帧和原始数据文件：

![“添加数据集”对话框](media/variable-explorer-import-dataset-dialog.png)
