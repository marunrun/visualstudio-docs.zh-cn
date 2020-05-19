---
title: 在字符串可视化工具中查看字符串 | Microsoft Docs
ms.date: 04/08/2019
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JavaScript
helpviewer_keywords:
- string visualizer
- visualizers, string
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 33e1cbd4b1c754498d7e2bd6c354e874ae8cdad5
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72450392"
---
# <a name="view-strings-in-a-string-visualizer-in-visual-studio"></a>在 Visual Studio 中的字符串可视化工具中查看字符串

在 Visual Studio 中进行调试时，可以使用内置字符串可视化工具查看字符串。 字符串可视化工具显示对于数据提示或调试器窗口而言过长的字符串。 它还可以帮助识别格式错误的字符串。

内置的字符串可视化工具包括纯文本、XML、HTML 和 JSON 选项。 也可以从“自动”或其他调试器窗口中打开一些其他类型的内置可视化工具，例如 [DataSet、DataTable 和 DataView](../debugger/dataset-visualizer-dialog-box.md) 对象。

> [!NOTE]
> 如果需要在可视化工具中检查 XAML 或 WPF UI 元素，请参阅[在调试时检查 XAML 属性](../xaml-tools/inspect-xaml-properties-while-debugging.md)或[如何使用 WPF 树可视化工具](../debugger/how-to-use-the-wpf-tree-visualizer.md)。

## <a name="open-a-string-visualizer"></a>打开字符串可视化工具

要打开字符串可视化工具，必须在调试期间暂停。 将鼠标悬停在具有纯文本、XML、HTML 或 JSON 字符串值的变量上，然后选择放大镜图标 ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")。

![打开字符串可视化工具](../debugger/media/dbg-tips-string-visualizers.png "打开字符串可视化工具")

## <a name="view-string-visualizer-data"></a>查看字符串可视化工具数据

在字符串可视化工具窗口中，“表达式”字段显示要将鼠标悬停在其上的变量或表达式，而“值”字段显示字符串值。

空白值表示所选可视化工具无法识别该字符串。 例如，对于没有 XML 标记的文本字符串或 JSON 字符串，XML 可视化工具会显示空白值。

若要查看所选可视化工具无法识别的字符串，请选择文本可视化工具。 文本可视化工具可显示纯文本。

### <a name="view-json-string-data"></a>查看 JSON 字符串数据

在 JSON 可视化工具中，格式正确的 JSON 字符串类似于下图。 格式错误的 JSON 可能会显示错误图标（如果无法识别，则为空白）。 若要标识 JSON 错误，请将字符串复制并粘贴到 JSON linting 工具，例如 [JSLint](https://www.jslint.com/)。

![JSON 字符串可视化工具](../debugger/media/dbg-tips-string-visualizer-json.png "JSON 字符串可视化工具")

### <a name="view-xml-string-data"></a>查看 XML 字符串数据

在 XML 可视化工具中，格式正确的 XML 字符串类似于下图。 格式错误的 XML 可能在没有 XML 标记的情况下显示，如果无法识别则显示为空白。

![XML 字符串可视化工具](../debugger/media/dbg-string-visualizers-xml.png "XML 字符串可视化工具")

### <a name="view-html-string-data"></a>查看 HTML 字符串数据

格式正确的 HTML 字符串的显示方式与在浏览器中的呈现方式相似，如下图所示。 格式错误的 HTML 可能显示为纯文本。

![HTML 字符串可视化工具](../debugger/media/dbg-string-visualizers-html.png "HTML 字符串可视化工具")

## <a name="see-also"></a>请参阅

- [创建自定义可视化工具（C#、Visual Basic）](../debugger/create-custom-visualizers-of-data.md)
- [Visual Studio for Mac 中的数据可视化效果](/visualstudio/mac/data-visualizations)