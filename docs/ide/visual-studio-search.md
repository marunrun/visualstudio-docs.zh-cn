---
title: 使用 Visual Studio 搜索
description: 了解如何使用 Visual Studio 搜索来查找设置、菜单和代码。
ms.date: 10/08/2020
ms.topic: how-to
helpviewer_keywords:
- environments [Visual Studio], navigation
- documents [Visual Studio], navigating
- IDE, navigation
- navigation [Visual Studio]
- files [Visual Studio], navigating between
- windows [Visual Studio], navigating
- Window.QuickLaunch
- IDE navigator
ms.assetid: 3870a8fd-4afa-4f1e-a811-9fdf41a9e82d
monikerRange: vs-2019
author: profexorgeek
ms.author: jusjohns
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b9f8182646af4facb0f2f86c74f95dff091d55d1
ms.sourcegitcommit: cea9e5787ff33e0e18aa1942bf4236748e0ef547
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92199678"
---
# <a name="use-visual-studio-search"></a>使用 Visual Studio 搜索

Visual Studio 集成开发环境 (IDE) 提供了许多菜单、选项和功能，使用者可能很难记住。 Visual Studio 搜索功能是一个单一搜索框，可帮助开发人员查找 IDE 菜单和选项，还能搜索代码。 无论你是刚接触 Visual Studio 还是经验丰富的开发人员，此功能都可以提供一种快速搜索 IDE 功能和代码的方法。

使用 Ctrl+Q 键盘快捷方式访问搜索框，或者单击默认位于菜单栏旁边的 Visual Studio 搜索输入框 ：

:::image type="content" source="media/visual-studio-search-cropped.png" alt-text="Visual Studio 搜索框" lightbox="media/visual-studio-search.png":::

> [!NOTE]
> Visual Studio 搜索执行的命令为 `Window.QuickLaunch`，你可能会看到此功能，它称为“快速搜索”或“快速启动”。

与其他搜索功能（如“在文件中查找”或“搜索解决方案资源管理器”）不同，用于 Visual Studio 结果的搜索包括 IDE 功能、菜单选项、文件名等。 以下部分讨论 Visual Studio 搜索可找到的不同类型的结果。

## <a name="search-menus-options-and-windows"></a>搜索菜单、选项和窗口

你可以使用 Visual Studio 搜索框来查找设置、选项和类似的配置项目。 例如，搜索“更改主题”，以快速查找并打开对话框，使用该对话框可更改 Visual Studio 颜色主题，如以下屏幕截图所示：

:::image type="content" source="media/visual-studio-search-options.png" alt-text="Visual Studio 搜索框":::

> [!TIP]
> 在大多数情况下，Visual Studio 搜索还会提供结果中每个项的菜单、快捷键和位置。

你可以使用 Visual Studio 搜索框来查找菜单项和命令。 例如，搜索“clean sol”，可快速查找并执行“清理解决方案”命令。 搜索结果还会提示如何在菜单中找到此命令，如以下屏幕截图所示：

:::image type="content" source="media/visual-studio-search-menu.png" alt-text="Visual Studio 搜索框":::

最后，还可以搜索意外关闭的窗口或面板。 例如，搜索“测试”，以查找并打开“测试资源管理器”窗口：

:::image type="content" source="media/visual-studio-search-window.png" alt-text="Visual Studio 搜索框":::

## <a name="search-files-and-code"></a>搜索文件和代码

Visual Studio 搜索还会在解决方案项中搜索文件名、代码、方法和其他匹配项。 在以下屏幕截图中，针对 markdown 的搜索过程在解决方案中找到了 MarkdownMetaExtractor.cs 文件、`MarkdownMetaExtractor` 类和两个方法：

:::image type="content" source="media/visual-studio-search-files.png" alt-text="Visual Studio 搜索框":::

你还可以进行“驼峰大小写”搜索。 在以下屏幕截图中，针对 FSS 的搜索过程找到了 FolderSizeScanner 文件、类和方法  ：

:::image type="content" source="media/visual-studio-search-camel.png" alt-text="Visual Studio 搜索框":::

## <a name="see-also"></a>请参阅

- [Visual Studio 命令](reference/visual-studio-commands.md)