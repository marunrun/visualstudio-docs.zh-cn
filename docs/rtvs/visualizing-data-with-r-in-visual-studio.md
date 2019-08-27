---
title: 使用 R 可视化数据
description: 在 Visual Studio 中如何使用绘图窗口从 R 程序中绘制数据。
ms.date: 06/29/2017
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: a48ad7800f8ea2b992e848cfbf6b4fdac99b2062
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62811039"
---
# <a name="create-visual-data-plots-with-r"></a>使用 R 创建可视数据图

绘图是数据科学家工作流的关键部分。 在针对 Visual Studio 的 R 工具 (RTVS) 中，所有绘图活动围绕一个或多个绘图窗口进行，这些窗口旨在提高此关键活动的生产效率。

![绘制英雄形象](media/plotting-hero-image.png)

|   |   |
|---|---|
| ![视频的摄像机图标](../install/media/video-icon.png "观看视频") | [观看视频 (youtube.com)](https://www.youtube.com/watch?v=ZTbKmz5RSgY) 了解使用 R 进行绘制（2 分 02 秒）。 |

## <a name="the-plot-window"></a>绘图窗口

绘图窗口包含一系列绘图，每个绘图均由 `plot` 命令生成。 例如，如果无可用绘图窗口，则可使用 `plot(1:100)` 创建新绘图窗口：

![1 到 100 的线性图](media/plotting-1-to-100.png)

从技术上讲，R `plot` 命令将其输出呈现到 R 图形设备；绘图窗口会呈现 R 图形设备的内容，这就是为什么每个绘图窗口都有设备编号的原因。

绘图窗口独立于 Visual Studio 项目，且在加载和关闭项目时仍保持打开状态。

生成绘图时会用到“活动”绘图窗口，在绘图历史记录中保存之前的绘图（请参阅[绘图历史记录](#plot-history)）。 例如，输入 `plot(100:1)`，第一个绘图将被替换为向下的行。

与所有其他 Visual Studio 窗口类似。 绘图窗口支持自定义布局（请参阅[在 Visual Studio 中自定义窗口布局](../ide/customizing-window-layouts-in-visual-studio.md)。 绘图窗口可停靠在 Visual Studio 框架内的不同位置，在该框架内调整大小，或者完全从框架中提出，独立调整大小。

调整绘图窗口大小后，始终会重新呈现绘图，以提供最佳质量的图像。 通常会在将绘图导出到文件或剪贴板之前使用下一节所述的命令调整绘图的大小。

## <a name="plot-window-commands"></a>绘图窗口命令

绘图窗口工具栏会保存适用的命令，其中大部分命令可通过“R 工具” > “绘图”菜单使用。

| Button | 命令 | 说明 |
| --- | --- | --- |
| ![“新建绘图窗口”按钮](media/plotting-toolbar-01-new-plot-window.png) | 新建绘图窗口 | 创建具有自己的历史记录的单独绘图窗口。 请参阅[多个绘图窗口](#multiple-plot-windows)。 |
| ![“激活绘图窗口”按钮](media/plotting-toolbar-02-activate-plot-window.png) | 激活绘图窗口 | 将当前绘图窗口设置为活动窗口，以便将后续 `plot` 命令呈现给该窗口。 请参阅[多个绘图窗口](#multiple-plot-windows)。 请参阅[多个绘图窗口](#multiple-plot-windows)。 |
| ![“绘图历史记录窗口”按钮](media/plotting-toolbar-03-plot-history.png) | 绘图历史记录窗口 | 打开一个窗口，其中历史记录中的所有绘图均显示为缩略图。 请参阅[绘图历史记录](#plot-history)。 |
| ![“绘图历史记录”按钮](media/plotting-toolbar-04-plot-history-arrows.png) | 上一个/下一个绘图 |  导航到历史记录中的上一个或下一个绘图。 还可使用 Ctrl+Alt+F11（上一个）和 Ctrl+Alt+F12（下一个）在历史记录中导航。 请参阅[绘图历史记录](#plot-history)。 |
| ![“另存为图像”按钮](media/plotting-toolbar-05-save-as-image.png)| 另存为图像 | 提示输入文件名并将当前绘图（按窗口大小显示的窗口内容）保存到图像文件。 可用格式为 `.png`、`.jpg`、`.bmp` 和 `.tif`。 |
| ![“另存为 PDF”按钮](media/plotting-toolbar-06-save-as-pdf.png)| 另存为 PDF | 使用当前窗口大小将当前绘图保存到 PDF 文件。 如果 PDF 进行了缩放，则会重新呈现绘图。 |
| ![“复制为位图”按钮](media/plotting-toolbar-07-copy-as-bitmap.png)| 复制为位图 | 使用当前窗口大小将图形复制到剪贴板作为光栅位图。 |
| ![“复制为图元文件”按钮](media/plotting-toolbar-08-copy-as-metafile.png)| 复制为图元文件 | 将绘图复制到剪贴板作为 [Windows 图元文件](https://en.wikipedia.org/wiki/Windows_Metafile)（维基百科）。 |
| ![“删除绘图”按钮](media/plotting-toolbar-09-remove-plot.png)| 删除绘图 | 从历史记录中删除当前绘图。 |
| ![“清除所有绘图”按钮](media/plotting-toolbar-10-clear-all-plots.png) | 清除所有绘图 | 从历史记录中删除所有绘图（确认提示）。 |

## <a name="multiple-plot-windows"></a>多个绘图窗口

由于数据科学家经常处理来自许多不同的数据集的多个绘图，所以通过使用 RTVS 可创建多个独立的绘图窗口。 然后可以根据需要在 Visual Studio 框架内或在该框架外排列这些窗口。 （请参阅[在 Visual Studio 中自定义窗口布局](../ide/customizing-window-layouts-in-visual-studio.md)，了解有关调整停靠和调整大小的常规信息。）

可使用工具栏按钮或“R 工具” > “绘图” > “新建绘图窗口”创建新的绘图窗口。 新的绘图窗口会成为“活动”窗口，会在该窗口中呈现新绘图。 要更改活动窗口，请切换到该窗口，然后选择“激活绘图窗口”工具栏按钮或使用“R 工具” > “绘图” > “激活绘图窗口”。

绘图也是独立的对象，这意味着可以使用鼠标拖放或使用右键单击上下文菜单和“编辑”菜单上的“复制”、“剪切”和“粘贴”命令，在绘图窗口间复制或移动绘图。

拖放的默认行为是复制；按住 Shift 键进行拖放则是移动。

## <a name="plot-history"></a>绘图历史记录

绘图命令保留在每个窗口的绘图历史记录中，确保保留了会话中的所有绘图。 要浏览历史记录，请使用绘图窗口工具栏上的箭头按钮，或按 Ctrl+Alt+F11 和 Ctrl+Alt+F12。 还可使用工具栏按钮或“R 工具” > “绘图”菜单命令，再次从窗口中删除单个绘图或清除所有绘图。

要查看整个绘图集合，请使用工具栏按钮或“R 工具” > “绘图” > “绘图历史窗口”打开“绘图历史记录窗口”。
历史记录会提供已在该窗口中显示的绘图缩略图列表，并且按不同绘图窗口（或设备）进行分组。 使用工具栏上的“缩放”按钮更改缩略图的大小。

![绘图历史记录窗口](media/plotting-plot-history-window.png)

若要在其关联的窗口中打开绘图，请双击并选中该绘图，然后选择“显示绘图”工具栏按钮，或右键单击并选择“显示绘图”。 还可选中单个绘图，并从右键单击上下文或“编辑”菜单进行复制、剪切或删除。

所有窗口的绘图历史记录的生命周期取决于交互 R 会话的生命周期。 如果重置 R 会话，或者退出并重启 Visual Studio，会重置绘图历史记录。

## <a name="programmatically-manipulate-plot-windows"></a>以编程方式操作绘图窗口

可通过编程方式用 R 代码操作绘图窗口，使用设备编号识别特定的绘图窗口。

- `dev.list()`：列出当前 R 会话中的所有图形设备。
- `dev.new()`：创建一个新的图形设备（一个新的绘图窗口）。
- `dev.set(<device number>)`：设置活动图形设备。
- `dev.off()`：删除活动设备。
