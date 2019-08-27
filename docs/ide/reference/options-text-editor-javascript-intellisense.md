---
title: 选项，文本编辑器，JavaScript，IntelliSense
ms.date: 10/29/2018
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Intellisense.References
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Intellisense.General
- VS.ToolsOptionsPages.Text_Editor.TypeScript.IntelliSense.General
ms.assetid: b4a9816d-cf87-4dc6-a8d4-1591d6a48103
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e3d030e028332bd57afe66eee31c888713721212
ms.sourcegitcommit: ce1ab8a25c66a83e60eab80ed8e1596fe66dd85c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2019
ms.locfileid: "68605981"
---
# <a name="options-dialog-box-text-editor--javascript--intellisense"></a>“选项”对话框：“文本编辑器”\>“JavaScript”\>“IntelliSense”

使用 **“选项”** 对话框的 **“IntelliSense”** 页可以修改影响 IntelliSense for JavaScript 行为的设置。 可以通过选择菜单栏上的“工具” > “选项”，然后展开“文本编辑器” > “JavaScript/TypeScript” > “IntelliSense”来访问“IntelliSense”页       。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

**“IntelliSense”** 页包含以下部分：

## <a name="statement-completion"></a>语句结束

可以使用这些选项更改 IntelliSense 语句结束的行为。

### <a name="uielement-list"></a>UIElement 列表

**仅使用 Tab 或 Enter 键提交**

选中此复选框时，JavaScript 代码编辑器仅将在你选择“Tab”或“Enter”键后，才会附加完成列表中选定项目的语句   。 取消选中此复选框时，其他字符（如句点、逗号、冒号、左括号和左大括号 ({)） - 也可以附加具有选定项的语句。

## <a name="references"></a>reference

可以使用这些选项来指定位于不同 JavaScript 项目类型的范围内的 IntelliSense .js 文件类型。 IntelliSense 引用通常用于为全局对象提供 IntelliSense 支持。 还可以使用此页对必须在运行时加载的脚本设置加载顺序以及添加 IntelliSense 扩展文件。

### <a name="uielement-list"></a>UIElement 列表

**引用组**

此选项指定引用组类型。 支持三个引用组：

可以使用预定义的引用组指定特定 IntelliSense .js 文件位于不同 JavaScript 项目的范围内。 提供四个引用组：

- 隐式 (Windows *version*)，用于使用 JavaScript 的 [!INCLUDE[win8_appname_long](../../debugger/includes/win8_appname_long_md.md)] 应用。 包含在该组中的文件位于代码编辑器中打开的每个 .js 文件的范围内，用于使用 JavaScript 的 [!INCLUDE[win8_appname_long](../../debugger/includes/win8_appname_long_md.md)] 应用。

- 隐式 (Web)，用于 HTML5 项目。 包含在该组中的文件位于代码编辑器中为这些项目类型打开的每个 .js 文件的范围中。

- 专用工作线程引用组，用于 HTML5 Web 工作线程。 该组中指定的文件位于显式引用专用工作线程引用组的 .js 文件的范围中。

- 一般类型，用于其他 JavaScript 项目类型。

**包含的文件**

此选项指定文件加载到语言服务上下文的顺序。 可以使用 **“移除”** 、 **“上移”** 和 **“下移”** 按钮配置此顺序。 为使 IntelliSense 正常工作，依赖于另一文件的文件必须在另一文件加载后加载。

> [!CAUTION]
> 如果在两个或更多隐式引用中无条件定义了一个对象，则将使用此列表中的最后一个引用来定义此对象。

**添加对组的引用**

使用此选项，可通过浏览到相应文件来添加其他 IntelliSense .js 文件。

**下载杂项文件项目中文件的远程引用(如 http://)**

选中此复选框时，如果有 JavaScript 文件在项目上下文外部打开，则 Visual Studio 会下载在文件中引用的远程 JavaScript 文件，以提供 IntelliSense 信息。 如果选择此选项，当你在 JavaScript 文件中包括这些文件作为引用时，将下载这些文件。

> [!NOTE]
> 对于 Web 项目，默认下载你的项目中所引用的远程文件。

## <a name="see-also"></a>请参阅

- [JavaScript IntelliSense](../../ide/javascript-intellisense.md)