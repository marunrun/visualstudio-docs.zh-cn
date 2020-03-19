---
title: 为其他语言添加编辑器支持
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax colorization
- IntelliSense
- IDE, navigation
- documents [Visual Studio], navigation
- TextMate bundle
- TextMate language grammar
- language support
ms.assetid: d78c43ee-4ef2-42e5-984e-d137de4e7e92
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d4fafaf9356d8862808e1ac6ad125207d71769b5
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75590873"
---
# <a name="add-visual-studio-editor-support-for-other-languages"></a>为其他语言添加 Visual Studio 编辑器支持

了解 Visual Studio 编辑器如何在不同计算机语言间进行读取和导航，以及如何添加其他语言的 Visual Studio 编辑器支持。

## <a name="syntax-colorization-statement-completion-and-navigate-to-support"></a>语法着色、语句完成和“导航到”支持

Visual Studio 编辑器中的功能（如语法着色、语句完成（也称作 IntelliSense）和“导航到”等）可帮助你更轻松地写入、读取和编辑代码  。 以下屏幕截图举例说明在 Visual Studio 中编辑 Perl 脚本。 语法自动着色。 例如，代码中的注解用绿色标记，代码、路径、语句分别用黑色、红色和蓝色标记。 Visual Studio 编辑器对支持的任何语言自动着色。 此外，当开始输入已知语言关键字或对象时，语句完成会显示可能的语句和对象列表。 语句完成有助于更快速、更轻松地写入代码。

![Perl 脚本中的语法着色](../ide/media/vside_perledit.png)

对于以下使用 [TextMate 语法](https://manual.macromates.com/en/language_grammars)的语言，Visual Studio 当前提供语法着色和基本语句完成支持。 如果你最喜爱的语言不在表中，别担心，可以添加它。

|||||||
|-|-|-|-|-|-|
|Bat|F#|Java|Markdown|Rust|Visual Basic|
|Clojure|Go|JavaDoc|Objective-C|ShaderLab|C#|
|CMake|Groovy|JSON|Perl|ShellScript|Visual C++|
|CoffeeScript|HTML|LESS|Python|SQL|VBNet|
|CSS|INI|LUA|R|Swift|XML|
|Docker|Jade|品牌|Ruby|TypeScript|YAML|

除语法着色和基本语句完成外，Visual Studio 还具有一种称为[导航到](https://blogs.msdn.microsoft.com/benwilli/2015/04/09/visual-studio-tip-3-use-navigate-to/)的功能。 可使用此功能快速搜索代码文件、文件路径和代码符号。 Visual Studio 为以下语言提供“导航到”支持。

- C#

- C++

- TypeScript

- JavaScript

- Visual Basic

- Go

- Java

- PHP

所有这些文件类型均有上述功能，即使尚未安装对某种语言的支持也是如此。 安装某种语言的专门支持可能会提供其他语言支持，例如 IntelliSense 或其他高级语言功能（如灯泡）。

## <a name="add-support-for-non-supported-languages"></a>添加对不受支持语言的支持

Visual Studio 通过 [TextMate 语法](https://manual.macromates.com/en/language_grammars)在编辑器中提供语言支持。 如果你喜欢的编程语言当前在 Visual Studio 编辑器中不受支持，请先在 Web 上搜索&mdash;可能存在该语言的 TextMate 包。 如果还是找不到，可通过创建语言语法和片段的 TextMate 包模型自行添加对该语言的支持。

在以下文件夹中添加 Visual Studio 的任何新 TextMate 语法：

*%userprofile%\\.vs\Extensions*

如适用，请在此基路径下添加下列文件夹：

|文件夹名|说明|
|-----------------|-----------------|
|\\ *\<language name>*|语言文件夹。 用语言的名称替换 *\<language name>* 。 例如， *\Matlab*。|
|*\Syntaxes*|语法文件夹。 包含语言的 .json 语法文件，如 Matlab.json   。|
|*\Snippets*|代码段文件夹。 包含语言的代码段。|

在 Windows 中，%userprofile% 解析为路径 c:\Users  user name> *\\\<* 。 如果系统上不存在“Extensions”  文件夹，则需要创建它。 如果该文件夹已存在，它将被隐藏。

> [!TIP]
> 如果在编辑器中打开了任何文件，则需要在添加 TextMate 语法之后关闭并重新打开它们，以查看语法高亮显示。

有关如何创建 TextMate 语法的详细信息，请参阅 [TextMate - 语言语法简介](https://developmentality.wordpress.com/2011/02/08/textmate-introduction-to-language-grammars/)和[如何创建 Textmate 包的语言语法和自定义主题说明](https://benparizek.com/notebook/notes-on-how-to-create-a-language-grammar-and-custom-theme-for-a-textmate-bundle)。

## <a name="see-also"></a>另请参阅

- [添加语言服务器协议扩展](../extensibility/adding-an-lsp-extension.md)
- [演练：创建代码片段](../ide/walkthrough-creating-a-code-snippet.md)
- [演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)
