---
title: 如何：在 IDE 中移动 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- environments [Visual Studio], navigation
- documents [Visual Studio], navigating
- IDE, navigation
- navigation [Visual Studio]
- files [Visual Studio], navigating between
- windows [Visual Studio], navigating
- Window.NextDocumentWindowNav
- IDE navigator
ms.assetid: 6c36b6eb-c93f-496b-af08-4199f7afd8bd
caps.latest.revision: 33
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 89c4447eb6bbc4b2ae9f7667672626d5119c61d6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651787"
---
# <a name="how-to-move-around-in-the-visual-studio-ide"></a>如何：在 Visual Studio IDE 中移动
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

集成开发环境 (IDE) 的设计旨在使你可以根据首选项或项目要求，以几种不同方式在窗口间和文件间移动。 可以选择在编辑器中打开的文件之间循环切换，或在 IDE 中所有活动工具窗口之间循环。 还可以直接切换到在编辑器中任何打开的文件，而不考虑上一次访问的顺序。 在 IDE 中工作时，这些功能有助于提高工作效率。

> [!NOTE]
> 对话框中的可用选项以及显示的菜单命令的名称和位置可能与“帮助”中的描述不同，具体取决于您的当前设置或版本。 此帮助页是根据“常规开发设置”  而编写的。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="keyboard-shortcuts"></a>键盘快捷键
 Visual Studio 中几乎每个菜单命令都具有键盘快捷方式。 你也可以创建自己的自定义快捷方式。 有关详细信息，请参阅[标识并自定义键盘快捷方式](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。

## <a name="navigating-among-files-in-the-editor"></a>在编辑器中的文件之间导航
 可以使用多种方法在编辑器中打开的文件之间移动。 可以依据访问顺序在文件之间移动，使用 IDE 导航器快速查找当前打开的任何文件，或将收藏夹文件单边锁定到选项卡以使它们始终可见。

 “向后导航”和“向前导航”可在编辑器中打开的文件之间依据访问文件的顺序进行循环切换，非常类似于在 Microsoft Internet Explorer 中查看历史记录时所执行的“后退”和“前进”。

#### <a name="to-move-through-open-files-in-order-of-use"></a>按使用顺序在打开的文件之间移动

- 若要以最近使用的顺序激活打开的文档，请按 CTRL + 减号。

- 若要以相反顺序激活打开的文档，请按 CTRL + SHIFT + 减号。

  > [!NOTE]
  > 还可以在“视图”  菜单上找到“向后导航”  和“向前导航”  。

  还可以切换到编辑器中打开的特定文件，而不考虑上次访问该文件的时间，方法是使用“IDE 导航器”  、编辑器中的“活动文件”  列表或“Windows”  对话框。

  “IDE 导航器”  工作方式非常类似于 Windows 应用程序切换器。 不能从菜单使用它，仅可使用键盘快捷方式进行访问。 可以使用两个命令中的任一个来访问“IDE 导航器”  （如下所示）以便在文件间循环切换，具体取决于你希望的循环切换顺序。

  ![Visual Studio IDE 导航器](../ide/media/vs2015-ide-navigator.png "|::ref1::|")

  使用 `Window.PreviousDocumentWindowNav` 可移动到最近访问的文件，使用 `Window.NextDocumentWindowNav` 可按相反顺序移动。 常规开发设置将 CTRL + SHIFT + TAB 分配给 `Window.PreviousDocumentWindowNav`，将 CTRL + TAB 分配给 `Window.NextDocumentWindowNav`。

> [!NOTE]
> 如果所用设置组合尚未向此命令分配快捷键组合，可以使用“选项”  对话框的“键盘”  页分配自己的自定义命令。 有关详细信息，请参阅[标识并自定义键盘快捷方式](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。

#### <a name="to-switch-to-specific-files-in-the-editor"></a>切换到编辑器中的特定文件

- 按 Ctrl+Tab 显示“IDE 导航器”  。 按住 CTRL 键并重复按 TAB，直到选中要切换到的文件。

    > [!TIP]
    > 若要颠倒浏览“活动文件”  列表的顺序，请按住 Ctrl+Shift 键，并按 Tab。

     \- 或 -

- 在编辑器的右上角，选择“活动文件”  按钮，然后从列表中选择要切换到的文件。

     \- 或 -

- 在菜单栏上，依次选择“窗口”  、“窗口”  。

- 在列表中，选择想要查看的文件，然后选择“激活”  。

## <a name="navigating-among-tool-windows-in-the-ide"></a>在 IDE 中的工具窗口间导航
 “IDE 导航器”  还允许在 IDE 中打开的工具窗口之间循环切换。 可以使用两个命令中的任一个来访问“IDE 导航器”  以便在工具窗口间循环切换，具体取决于你希望的循环切换顺序。 使用 `Window.PreviousToolWindowNav` 可移动到最近访问的文件，使用 `Window.NextToolWindowNav` 可按相反顺序移动。 常规开发设置将 SHIFT + ALT + F7 分配给 `Window.PreviousDocumentWindowNav`，将 ALT + F7 分配给 `Window.NextDocumentWindowNav`。

> [!NOTE]
> 如果所用设置组合尚未向此命令分配快捷键组合，可以使用“选项”  对话框的“键盘”  页分配自己的自定义命令。 有关详细信息，请参阅[标识并自定义键盘快捷方式](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。

#### <a name="to-switch-to-a-specific-tool-window-in-the-ide"></a>切换到 IDE 中的特定工具窗口

- 按 Alt+F7 显示“IDE 导航器”  。 按住 ALT 键并重复按 F7，直到选中要切换到的窗口。

    > [!TIP]
    > 若要颠倒浏览“活动工具窗口”  列表的顺序，请按住 Shift+Alt 键，并按 F7。

## <a name="see-also"></a>另请参阅
 [自定义窗口布局](../ide/customizing-window-layouts-in-visual-studio.md) [默认键盘快捷键](../ide/default-keyboard-shortcuts-in-visual-studio.md)
