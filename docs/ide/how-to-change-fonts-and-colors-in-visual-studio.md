---
title: 更改主题、字体、文本和对比度以提供辅助功能
description: 了解如何更改 Visual Studio 颜色主题、字体颜色、文本大小和额外的对比度颜色，以提供辅助功能。
ms.date: 08/20/2020
ms.topic: how-to
ms.custom: contperfq1
helpviewer_keywords:
- Visual Studio, color themes
- color themes, Visual Studio
ms.assetid: 60d91ba1-244b-4c43-847f-60b744f1352a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b2410974ed95b1aa8dca3dc3e31a39c39df2d4a0
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801433"
---
# <a name="how-to-change-fonts-colors-and-themes-in-visual-studio"></a>如何：在 Visual Studio 中更改字体、颜色和主题

可以通过多种方式在 Visual Studio 中更改字体和颜色。 例如，可以将默认的蓝色主题更改为深色主题（也称为“深色模式”）。 如果最适合你的需求，还可以选择一个额外的对比度主题。 另外，还可以在 IDE 和代码编辑器中更改默认字体和文本大小。

## <a name="change-the-color-theme"></a>更改颜色主题

下面介绍如何在 Visual Studio 中更改 IDE 框架和工具窗口的颜色主题。

1. 在菜单栏上，依次选择“工具” > “选项” 。

1. 在选项列表中，选择“环境” > “常规” 。

1. 在“颜色主题”列表中，选择默认的“蓝色”主题、“浅色”主题、“深色”主题或“蓝色(额外对比度)”主题。

   ![用于更改颜色主题的“选项”对话框的屏幕截图](media/fonts-colors-theme.png "可用于更改颜色主题的“选项”对话框的屏幕截图")

    > [!NOTE]
    > 当你更改颜色主题时，IDE 中的文本将恢复为默认值，或恢复为之前为该主题自定义的字体和大小。

    :::moniker range="vs-2017"

    > [!TIP]
    > 可以通过安装 [Visual Studio 2017 颜色主题编辑器](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.VisualStudio2017ColorThemeEditor)创建和编辑你自己的 Visual Studio 主题。

    :::moniker-end

    :::moniker range="vs-2019"

    > [!TIP]
    > 可以通过安装 [Visual Studio 颜色主题设计器](https://marketplace.visualstudio.com/items?itemName=ms-madsk.ColorThemeDesigner)创建和编辑你自己的 Visual Studio 主题。

    :::moniker-end

## <a name="change-fonts-and-text-size"></a>更改字体和文本大小

可以更改所有 IDE 框架和工具窗口的字体和文本大小，也可以仅为某些窗口或文本元素更改字体和文本大小。 还可以更改编辑器中的字体和文本大小。

### <a name="to-change-the-font-and-text-size-in-the-ide"></a>更改 IDE 中的字体和文本大小

1. 在菜单栏上，依次选择“工具” > “选项” 。

1. 在选项列表中，选择“环境” > “字体和颜色” 。

1. 在“显示以下对象的设置”列表中，选择“环境”。

   ![用于在 IDE 中更改字体和颜色的“选项”对话框的屏幕截图](media/fonts-colors-environment.png "用于在 IDE 中更改字体和颜色的“选项”对话框的屏幕截图")

    > [!NOTE]
    > 如果仅更改工具窗口的字体，则在“显示以下对象的设置”列表中，选择“所有文本工具窗口” 。

1. 修改“字体”和“大小”选项，以更改 IDE 的字体和文本大小。

1. 在“显示项”中选择合适的项，然后修改“项前景”和“项背景”选项。

### <a name="to-change-the-font-and-text-size-in-the-editor"></a>更改编辑器中的字体和文本大小

1. 在菜单栏上，依次选择“工具” > “选项” 。

1. 在选项列表中，选择“环境” > “字体和颜色” 。

1. 在“显示以下对象的设置”列表中，选择“文本编辑器”。

   ![用于在编辑器中更改字体和颜色的“选项”对话框的屏幕截图](media/fonts-colors-text-editor.png "用于在编辑器中更改字体和颜色的“选项”对话框的屏幕截图")

1. 修改“字体”和“大小”选项，以更改编辑器的字体和文本大小。

1. 在“显示项”中选择合适的项，然后修改“项前景”和“项背景”选项。

有关详细信息，请参阅[更改编辑器的字体和颜色](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md)页。

## <a name="accessibility-options"></a>辅助功能选项

如果视力不好，可以选择颜色主题选项。 可以为计算机上的所有应用和 UI 使用高对比度选项，或使用仅适用于 Visual Studio 的额外对比度选项。

### <a name="use-windows-high-contrast"></a>使用 Windows 高对比度

使用以下任一过程来切换 Windows 高对比度选项：

- 在 Windows 或任何 Microsoft 应用程序中，按左 Alt+左 Shift+PrtScn 键。

- 在 Windows 中，选择“开始” > “设置” > “轻松访问” > “高对比度”。

    > [!WARNING]
    > Windows 高对比度设置会影响计算机上的所有应用程序和 UI。

### <a name="use-visual-studio-extra-contrast"></a>使用 Visual Studio 额外对比度

使用以下过程来切换 Visual Studio 额外对比度选项：

1. 在 Visual Studio 的菜单栏上，选择“工具” > “选项”，然后在“选项”列表中，选择“环境” > “常规”。

1. 在“颜色主题”下拉列表中，选择“蓝色(额外对比度)”主题，然后选择“确定”。

若要详细了解可供使用的其他 Visual Studio 辅助功能选项，请参阅 [Visual Studio 的辅助功能](../ide/reference/accessibility-features-of-visual-studio.md)页。

> [!TIP]
> 如果有你认为可能有用但当前在 Visual Studio 中不可用的颜色或字体辅助功能选项，请通过选择 [Visual Studio 开发者社区](https://developercommunity.visualstudio.com/)中的“建议功能”来告知我们。 有关此论坛及其工作原理的详细信息，请参阅[建议功能](../ide/suggest-a-feature.md)页。

## <a name="next-steps"></a>后续步骤

若要了解有关可更改字体和颜色方案的所有用户界面 (UI) 元素的详细信息，请参阅[字体和颜色、环境、选项对话框](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)页。

## <a name="see-also"></a>请参阅

- [如何：在 Visual Studio 中更改编辑器中的字体和颜色](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md)
- [Visual Studio 代码编辑器的功能](../ide/writing-code-in-the-code-and-text-editor.md)
- [个性化设置 Visual Studio IDE 和编辑器](../ide/quickstart-personalize-the-ide.md)