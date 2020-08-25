---
title: JavaScript 开发人员编辑功能简介
description: 此 Visual Studio 代码编辑器简介演示了如何使用 Visual Studio 更轻松地编写、导航和理解 JavaScript 代码。
ms.date: 12/13/2018
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: a033c0fe1fd80edc7959c5f49993714982ecc805
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238175"
---
# <a name="learn-to-use-the-code-editor-for-javascript"></a>了解如何使用 JavaScript 版代码编辑器

这一简短的 Visual Studio 代码编辑器简介演示了如何使用 Visual Studio 更轻松地编写、导航和理解 C# 代码。

> [!TIP]
> 如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页免费安装。 根据所展开的应用开发的类型，可能需要使用 Visual Studio 安装 Node.js 开发工作负荷  。 若要详细了解如何获取 TypeScript 的语言服务，请参阅 [TypeScript 支持](../javascript/javascript-in-vs-2019.md#typescript-support)。

本文假定你已熟悉 JavaScript 开发。 如果不熟悉，建议先浏览教程（如[创建 Node.js 和 Express 应用](../javascript/tutorial-nodejs.md)）。

## <a name="add-a-new-project-file"></a>添加新的项目文件

可以使用 IDE 向项目添加新文件。

1. 打开 Visual Studio 中的项目后，右键单击解决方案资源管理器（右窗格）中的文件夹或项目节点，然后选择“添加” > “新建项目” 。

1. 在“新建文件”对话框的“常规”类别下，选择要添加的文件类型，如“JavaScript 文件”，然后选择“打开”   。

    将新文件添加到项目中，并在编辑器中打开。

## <a name="use-intellisense-to-complete-words"></a>使用 IntelliSense 完成单词

编写代码时，IntelliSense 是非常宝贵的资源。 它可显示某个类型的可用成员信息，或某个方法不同重载的参数详情。 在下面的代码中，键入 `Router()` 时，会显示可以传递的参数类型。 这称为签名帮助。

![使用 IntelliSense](../javascript/media/write-code-signature-checking.png)

还可用于完成单词，从而在输入大量字符后消除字符带来的歧义。 如果将光标放在下列代码中的 `data` 字符串之后并键入 `get`，则 IntelliSense 将显示之前在代码中定义的函数，或者在已添加到项目中的第三方库中定义的函数。

![使用 IntelliSense](../javascript/media/write-code-intellisense.png)

鼠标悬停在编程元素上时，IntelliSense 还可以显示关于类型的信息。

语言服务可以使用 TypeScript d.ts 文件和 JSDoc 注释来提供 IntelliSense 信息。 对于大多数常见的 JavaScript 库，d.ts 文件是自动获取的。 有关如何获取 IntelliSense 信息的更多详情，请参见 [JavaScript IntelliSense](../ide/javascript-intellisense.md?toc=/visualstudio/javascript/toc.json)

## <a name="check-syntax"></a>检查语法

语言服务使用 ESLint 提供语法检查和 linting。 如果需要在编辑器中设置语法检查选项，请选择“工具” > “选项” > “JavaScript/TypeScript” > “Linting”   。 linting 选项指向全局 ESLint 配置文件。

在下面的代码中，表达式用绿色突出显示了语法（绿色波浪）。 将鼠标悬停在语法突出显示上。

![查看语法错误](../javascript/media/write-code-syntax-checking.png)

这条消息的最后一行指示语言服务需要一个逗号 (`,`)。 绿色波浪表示警告。 红色波浪表示错误。

在下方窗格中，可以单击“错误列表”选项卡，查看警告信息和说明，以及文件名和行号。

![查看错误列表](../javascript/media/write-code-error-list.png)

可以通过在 `"data"` 之前添加逗号 (`,`) 来修复此代码。

有关 linting 的更多信息，请参阅 [Linting](https://github.com/microsoft/JSTSdocs/blob/master/articles/editor/linting.md)。

## <a name="comment-out-code"></a>为代码添加注释

工具栏是 Visual Studio 菜单栏下的一行按钮，有助于提高编码效率。 例如，可以切换 IntelliSense 完成模式（[IntelliSense](../ide/using-intellisense.md) 是一种编码辅助工具，可显示匹配方法列表以及其他内容），增加或减少行缩进，或标注出不想编译的代码。 在本部分中，我们将标注出部分代码。

在编辑器中选择一行或多行代码，然后在工具栏上选择“注释掉所选行”按钮![“注释掉”按钮](../javascript/media/write-code-comment-out.png)。 如果想要使用键盘，请按 Ctrl+K, Ctrl+C   。

JavaScript 注释字符 `//` 添加到了每个所选行的开始处，从而为代码添加注释。

## <a name="collapse-code-blocks"></a>折叠代码块

如果需要让某些代码区域显得整洁，可以将其折叠。 在函数第一行的边距中选择内部带有减号的小灰色框。 如果使用的是键盘，也可将光标置于构造函数代码中的任意位置，然后按 Ctrl+M、Ctrl+M   。

![“大纲显示折叠”按钮](../javascript/media/write-code-collapse-code.png)

代码块折叠到第一行，后跟省略号 (`...`)。 若要再次展开代码块，请单击现在带有加号的相同灰色框，或者再次按 Ctrl+M，Ctrl+M   。 此功能被称为[大纲显示](../ide/outlining.md)，在折叠长函数或整个类时特别有用。

## <a name="view-definitions"></a>查看定义

通过 Visual Studio 编辑器可轻松查看类型、函数等的定义。一种方法是导航到包含定义的文件，例如通过选择“转到定义”，转到引用计划元素的任何位置。 使用“[速览定义](../ide/go-to-and-peek-definition.md#peek-definition)”速度更快，不会干扰你处理文件。 现在来速览下面示例中 `render` 方法的定义。

右键单击 `render`，然后选择内容菜单上的“速览定义”。 或者，按 Alt+F12 。

   此时会出现一个弹出窗口，其中包含 `render` 方法的定义。 可在弹出窗口中滚动，甚至还可从速览的代码中查看另一类型的定义。

   ![“速览定义”窗口](../javascript/media/write-code-peek-definition.png)

选择弹出窗口右上方的“x”小框，关闭“速览定义”窗口。

## <a name="use-code-snippets"></a>使用代码片段

Visual Studio 提供了实用的代码片段，可用于快速方便地生成常用代码块。 [代码片段](../ide/code-snippets.md)可用于不同编程语言，包括 JavaScript。 现在向代码文件添加 `for` 循环。

将光标放在要插入代码片段的位置，右键单击并选择“代码片段” > “插入代码片段” 。

![Visual Studio 中的代码片段](../javascript/media/write-code-insert-snippet.png)

编辑器中显示“插入代码片段”框。 选择“常规”，然后双击列表中的“for”项 。

![Visual Studio 中 for 循环的代码片段](../javascript/media/write-code-insert-snippet-for-loop.png)

这会向代码中添加 `for` 循环代码片段：

```javascript
for (var i = 0; i < length; i++) {

}
```

依次选择“编辑” > “IntelliSense” > “插入代码片段”，然后选择语言的文件夹，即可查看该语言的可用代码片段  。

## <a name="see-also"></a>请参阅

- [代码片段](../ide/code-snippets.md)
- [导航代码](../ide/navigating-code.md)
- [大纲显示](../ide/outlining.md)
- [转到定义和速览定义](../ide/go-to-and-peek-definition.md)
- [重构](../ide/refactoring-in-visual-studio.md)
- [使用 IntelliSense](../ide/using-intellisense.md)
