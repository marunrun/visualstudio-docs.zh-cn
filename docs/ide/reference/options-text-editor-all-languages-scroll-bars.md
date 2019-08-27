---
title: “选项”->“文本编辑器”->“所有语言”->“滚动条”
ms.date: 10/25/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.All_Languages.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.Basic.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.CSharp.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.CoffeeScript.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.CSS.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.Dockerfile.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.F%2523.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.HQL.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.HTML.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.HTMLX.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.JavaScript.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.TypeScript.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.JSON.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.LESS.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.ResJSON.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.SCSS.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.SQL_Server_Tools.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.StreamAnalytics.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.T-SQL90.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.U-SQL.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.XAML.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.XML.ScrollBars
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd7be5aea136c901241ca66af485e76a39cd0ee5
ms.sourcegitcommit: 5694c5236fa32ba7f5bc1236a853f725ec7557e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2019
ms.locfileid: "68681316"
---
# <a name="options-text-editor-all-languages-scroll-bars"></a>“选项”->“文本编辑器”->“所有语言”->“滚动条”
使用此对话框可更改代码编辑器滚动条的默认行为。 若要显示这些选项，请选择“工具”菜单中的“选项”   。 在“文本编辑器”中，展开“所有语言”子文件夹，然后选择“滚动条”    。

> [!CAUTION]
> 在此页面用于设置所有开发语言的默认选项。 重置此对话框中的一个选项会将所有语言的“滚动条”选项重置为在此处选择的任何选项。 若要只为一种语言更改文本编辑器选项，请展开该语言的子文件夹并选择其选项页。

## <a name="show-horizontal-scroll-bar"></a>显示水平滚动条

勾选此项后，会显示一个水平滚动条，用户可以左右滚动，查看编辑器查看区域外的元素。 如果水平滚动条不可用，可以使用光标键滚动。

## <a name="show-vertical-scroll-bar"></a>显示垂直滚动条

勾选此项后，会显示一个垂直滚动条，用户可以上下滚动，查看编辑器查看区域外的元素。 如果垂直滚动条不可用，可以使用 Page Up、Page Down 键和光标键滚动。

## <a name="display"></a>显示

### <a name="show-annotations-over-vertical-scroll-bar"></a>在垂直滚动条上显示标注

选择垂直滚动条是否显示以下标注：

- 更改
- 标记
- 错误
- 插入点位置

> [!TIP]
> “显示标记”  选项包括断点和书签。

试试吧！请打开一个大型代码文件，并替换文件中多处出现的某文本。 滚动条将显示替换的效果，从而在替换了不应替换的内容时可撤回更改。

请参阅有关编辑代码时的各种颜色和符号含义的[增强型滚动条](https://blogs.msdn.microsoft.com/cdnstudents/2014/01/21/visual-studio-tips-and-tricks-enhanced-scroll-bar/)博客文章。

## <a name="behavior"></a>行为

滚动条有两种模式：滚动条模式和地图模式。

### <a name="use-bar-mode-for-vertical-scroll-bar"></a>使用垂直滚动条的条状模式

滚动条模式  在滚动条上显示注释指示器。 单击滚动条会向上或向下滚动页面，但不会跳到文件中的相应位置。

### <a name="use-map-mode-for-vertical-scroll-bar"></a>使用垂直滚动条的缩略图模式

当你在地图模式  下单击滚动条上的某个位置后，光标会跳到文件中的相应位置，而不只是向上或向下滚动页面。 代码行以缩图形式显示在滚动条上。 可选择地图列的宽度，具体方法是在“源代码概述”  中设置值。 若要在将指针悬停在地图之上时放大预览代码，请选择“显示预览工具提示”  选项。 折叠区域进行了不同的阴影化处理，双击阴影即可展开此类区域。

> [!TIP]
> 在地图模式下，可禁用代码缩图，具体方法是将“源代码概述”  设置为“关”  。 如果已选择“显示预览工具提示”  ，仍可在将指针悬停在滚动条之上时预览相应位置的代码，并且在你单击滚动条后光标仍会跳到文件中的相应位置。

## <a name="see-also"></a>请参阅

- [如何：自定义滚动条](../how-to-track-your-code-by-customizing-the-scrollbar.md)
