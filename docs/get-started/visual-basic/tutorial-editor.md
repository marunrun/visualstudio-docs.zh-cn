---
title: Visual Basic 开发人员编辑功能简介
description: 这一 10 分钟的 Visual Studio 代码编辑器简介演示了如何使用 Visual Studio 更轻松地编写、导航和理解 Visual Basic 代码。
ms.custom: seodec18, get-started
ms.date: 11/20/2018
ms.technology: vs-ide-general
ms.topic: tutorial
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 695b1600aedb30a9e75a7829af4bac400f069922
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "75584603"
---
# <a name="learn-to-use-the-code-editor"></a>了解如何使用代码编辑器

在这个 10 分钟的 Visual Studio 代码编辑器简介中，我们会向文件添加代码，了解 Visual Studio 编写、导航和了解代码的简便方法。

::: moniker range="vs-2017"

> [!TIP]
> 如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

> [!TIP]
> 如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

本文假定你已熟悉 Visual Basic。 如果不熟悉，建议先浏览 [Visual Studio 中的 Visual Basic 入门](../../get-started/visual-basic/tutorial-console.md)。

> [!TIP]
> 若要继续执行本文中的操作，请确保为 Visual Studio 选择了 Visual Basic 设置。 有关为集成开发环境 (IDE) 选择设置的信息，请参阅[选择环境设置](visual-studio-ide.md#select-environment-settings)。

## <a name="create-a-new-code-file"></a>创建新代码文件

先创建一个新文件并向其添加一些代码。

::: moniker range="vs-2017"

1. 打开 Visual Studio。

::: moniker-end

::: moniker range=">=vs-2019"

1. 打开 Visual Studio。 按 Esc  或单击“开始”窗口中的“继续但无需代码”  以打开开发环境。

::: moniker-end

2. 在菜单栏上的“文件”  菜单中，选择“新建文件”  。

3. 在“新建文件”对话框的“常规”类别中，选择“Visual Basic 类”，然后选择“打开”     。

   编辑器中将打开主干为 Visual Basic 类的新文件。 （你可能已经注意到，无需创建完整的 Visual Studio 项目来获取代码编辑器提供的某些权益，例如语法高亮。 仅需一个代码文件即可！）

   ![Visual Studio 中的 Visual Basic 代码文件](media/tutorial-editor.png)

## <a name="use-code-snippets"></a>使用代码片段

Visual Studio 提供了实用的代码片段，可用于快速方便地生成常用代码块  。 [代码片段](../../ide/code-snippets.md)可用于不同编程语言，包括 Visual Basic、C# 和 C++。 让我们将 Visual Basic Sub 代码片段添加到文件中  。

1. 将光标放在内容为 `End Class` 的行上方，并输入 sub  。

   随即将出现一个弹出对话框，其中包含有关 `Sub` 关键字以及如何插入 Sub 代码片段的信息  。

   ![Visual Studio 中代码片段的 IntelliSense](media/tutorial-intellisense-snippet.png)

1. 按 Tab 两次，插入代码片段  。

   将 Sub 过程 `MySub()` 的大纲添加到文件中。

对于不同编程语言，可用的代码片段不同。 可以通过选择“编辑” > “IntelliSense” > “插入代码片段”（或按 Ctrl+K、Ctrl+X）查看 Visual Basic 的可用代码片段     +    。 对于 Visual Basic，代码片段可用于以下类别：

![Visual Basic 代码片段列表](media/tutorial-code-snippet-list.png)

有一些代码片段用于确定计算机上是否存在文件或用于写入文本文件、读取注册表值、执行 SQL 查询、创建 [For Each...Next 语句](/dotnet/visual-basic/language-reference/statements/for-each-next-statement)等。

## <a name="comment-out-code"></a>为代码添加注释

工具栏是 Visual Studio 菜单栏下的一行按钮，有助于提高编码效率。 例如，可以切换到 IntelliSense 完成模式、增加或减少缩进，或者注释掉不想编译的代码。 （[IntelliSense](../../ide/using-intellisense.md) 有许多功能，其功能之一是可用作显示匹配方法列表的编码辅助工具。）在本部分中，我们将标注出部分代码。

![编辑工具栏按钮](media/tutorial-editor-toolbar.png)

1. 将以下代码粘贴到 `MySub()` 过程主体中。

   ```vb
   ' _words is a string array that we'll sort alphabetically
   Dim _words = New String() {
   "the",
   "quick",
   "brown",
   "fox",
   "jumps"
   }

   Dim morewords = New String() {
   "over",
   "the",
   "lazy",
   "dog"
   }

   Dim query = From word In _words
               Order By word.Length
               Select word
   ```

1. 我们现在没有使用 `morewords` 数组，但稍后可能会用到，所以我们不想彻底删除它。 那我们就来为这些行加上注释。 选择整个 `morewords` 定义直到结束花括号，然后选择工具栏上的“为选定行添加注释”  。 如果想要使用键盘，请按 Ctrl+K, Ctrl+C     。

   ![“添加注释”按钮](media/tutorial-comment-out.png)

   Visual Basic 注释字符 `'` 添加到了每个所选行的开始处，从而为代码添加注释。

## <a name="collapse-code-blocks"></a>折叠代码块

可以折叠部分代码，只关注感兴趣的部分。 作为演练，现在可将 `_words` 数组折叠为一行代码。 在内容为 `Dim _words = New String() {` 的行的边距中选择内部带有减号的小灰色框。 如果使用的是键盘，也可将光标置于数组定义中的任意位置，然后按 Ctrl+M、Ctrl+M     。

![“大纲显示折叠”按钮](media/tutorial-collapse.png)

代码块折叠到第一行，后跟省略号 (`...`)。 若要再次展开代码块，请单击现在带有加号的相同灰色框，或者再次按 Ctrl+M，Ctrl+M     。 此功能被称为[大纲显示](../../ide/outlining.md)，在折叠长方法或整个类时特别有用。

## <a name="view-symbol-definitions"></a>查看符号定义

通过 Visual Studio 编辑器可轻松查看类型、方法等的定义。一种方法是导航到包含定义的文件，例如通过选择“转到定义”，转到引用符号的任何位置  。 使用“[速览定义](../../ide/go-to-and-peek-definition.md#peek-definition)”速度更快，不会干扰你处理文件。 我们来快速查看一下 `String` 类型的定义。

1. 右键单击字 `String`，然后选择内容菜单上的“速览定义”  。 或者，按 Alt+F12   。

   此时会出现一个弹出窗口，其中包含 `String` 类的定义。 可在弹出窗口中滚动，甚至还可从速览的代码中查看另一类型的定义。

   ![“速览定义”窗口](media/tutorial-peek-definition.png)

1. 选择弹出窗口右上方的“x”小框，关闭“速览定义”窗口。

## <a name="use-intellisense-to-complete-words"></a>使用 IntelliSense 完成单词

编写代码时，[IntelliSense](../../ide/using-intellisense.md) 是非常宝贵的资源。 它可显示某个类型的可用成员信息，或某个方法不同重载的参数详情。 还可用于完成单词，从而在输入大量字符后消除字符带来的歧义。 添加代码行，将有序字符串呈现到控制台窗口，这是程序输出的标准位置。

1. 在 `query` 变量下，开始键入以下代码：

   ```vb
   For Each str In qu
   ```

   IntelliSense 会显示有关 `query` 符号的“快速信息”  。

   ![Visual Studio 中的 IntelliSense 文字自动完成](media/tutorial-intellisense-completion-list.png)

1. 若要使用 IntelliSense 文字自动完成功能插入单词 `query` 的剩余部分，请按 Tab  。

1. 完成后，代码块如以下代码所示。

   ```vb
   For Each str In query
       Console.WriteLine(str)
   Next
   ```

## <a name="refactor-a-name"></a>重构名称

没有谁能一次就得到正确的代码，代码中可能必须要更改的一项内容是变量或方法的名称。 我们来试试 Visual Studio 的[重构](../../ide/refactoring-in-visual-studio.md)功能，将 `_words` 变量重命名为 `words`。

1. 将光标置于 `_words` 变量的定义上，然后从右键菜单或上下文菜单中选择“重命名”  。

   此时编辑器右上角会弹出一个“重命名”对话框  。

1. 保持变量 `_words` 为选中状态，然后为“words”输入所需名称  。 请注意，查询中对 `words` 的引用也会自动重命名。 请在“重命名”弹出框中选中“包含注释”复选框，然后按 Enter 或“应用”     。

   ![“重命名”对话框](media/tutorial-rename.png)

1. 按 Enter 或单击“应用”   。

   出现的两处 `words` 均被重命名，代码注释中对 `words` 的引用也被重命名。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [了解项目和解决方案](tutorial-projects-solutions.md)

## <a name="see-also"></a>请参阅

- [代码片段](../../ide/code-snippets.md)
- [导航代码](../../ide/navigating-code.md)
- [大纲显示](../../ide/outlining.md)
- [转到定义和速览定义](../../ide/go-to-and-peek-definition.md)
- [重构](../../ide/refactoring-in-visual-studio.md)
- [使用 IntelliSense](../../ide/using-intellisense.md)
