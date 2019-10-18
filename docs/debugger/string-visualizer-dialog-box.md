---
title: "\"字符串可视化工具\" 对话框 |Microsoft Docs"
ms.date: 10/10/2018
ms.custom: seoapril2019
ms.topic: reference
f1_keywords:
- vs.debug.stringviewer
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JavaScript
helpviewer_keywords:
- string visualizer
- visualizers, string
ms.assetid: 080fd8f1-72b0-461f-8451-3c84d5dc51df
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 10e7e50ffc0cb61bd036bef65c554e8147eecc09
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72430832"
---
# <a name="string-visualizer-dialog-box"></a>“字符串可视化工具”对话框

在 Visual Studio 中进行调试时，可以使用内置字符串可视化工具查看字符串。 字符串可视化工具显示对于数据提示或调试器窗口而言过长的字符串。 它还可以帮助识别格式错误的字符串。

内置的字符串可视化工具包括纯文本、XML、HTML 和 JSON 选项。 你还可以从自动或其他调试器窗口中打开一些其他**类型的内置**可视化工具，如[数据集、DataTable 和 DataView](../debugger/dataset-visualizer-dialog-box.md)对象。

> [!NOTE]
> 如果需要在可视化工具中检查 XAML 或 WPF UI 元素，请参阅或在[调试时检查 xaml 属性](../xaml-tools/inspect-xaml-properties-while-debugging.md)或[如何使用 WPF 树可视化工具](../debugger/how-to-use-the-wpf-tree-visualizer.md)。

要打开字符串可视化工具，必须在调试期间暂停。 将鼠标悬停在具有纯文本、XML、HTML 或 JSON 字符串值的变量上，并选择![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")的放大镜图标。

## <a name="uielement-list"></a>UIElement 列表

**Expression**字段显示要悬停在其上方的变量或表达式。

**值**字段显示字符串值。 空**值**表示所选的可视化工具无法识别该字符串。 例如， **Xml 可视化工具**为不带 XML 标记的文本字符串或 JSON 字符串显示空**值**。 若要查看所选可视化工具无法识别的字符串，请改为选择**文本可视化工具**。 **文本可视化工具**显示纯文本。

### <a name="json-string-data"></a>JSON 字符串数据

格式正确的 JSON 字符串类似于 JSON 可视化工具中的下图。 格式错误的 JSON 可能会显示错误图标（如果无法识别，则为空白）。 若要标识 JSON 错误，请将字符串复制并粘贴到 JSON linting 工具，例如 [JSLint](https://www.jslint.com/)。

![JSON 字符串可视化工具](../debugger/media/dbg-tips-string-visualizer-json.png "JSON 字符串可视化工具")

### <a name="xml-string-data"></a>XML 字符串数据

格式正确的 XML 字符串类似于 XML 可视化工具中的下图。 格式错误的 XML 可能在没有 XML 标记的情况下显示，如果无法识别则显示为空白。

![XML 字符串可视化工具](../debugger/media/dbg-string-visualizers-xml.png "XML 字符串可视化工具")

### <a name="html-string-data"></a>HTML 字符串数据

格式正确的 HTML 字符串的显示方式与在浏览器中的呈现方式相似，如下图所示。 格式错误的 HTML 可能显示为纯文本。

![HTML 字符串可视化工具](../debugger/media/dbg-string-visualizers-html.png "HTML 字符串可视化工具")

## <a name="see-also"></a>请参阅

- [创建自定义可视化C#工具（、Visual Basic）](../debugger/create-custom-visualizers-of-data.md)
- [Visual Studio for Mac 中的数据可视化效果](/visualstudio/mac/data-visualizations)