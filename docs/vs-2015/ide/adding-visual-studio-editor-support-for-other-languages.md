---
title: 添加其他语言的编辑器支持 |Microsoft Docs
ms.date: 11/15/2016
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
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7138784201a1ac036047e1c8df362727fa393b51
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72620774"
---
# <a name="adding-visual-studio-editor-support-for-other-languages"></a>为其他语言添加 Visual Studio 编辑器支持
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

了解 Visual Studio 编辑器如何在不同计算机语言间进行读取和导航，以及如何添加其他语言的 Visual Studio 编辑器支持。

## <a name="syntax-colorization-statement-completion-and-navigate-to-support"></a>语法着色、语句完成和“导航到”支持
 Visual Studio 编辑器中的功能（如语法着色、语句完成和“定位到”等）可帮助你更轻松地读取、创建和编辑代码。 以下屏幕截图举例说明在 Visual Studio 中编辑 Perl 脚本。 语法自动着色。 例如，代码中的注解用绿色标记，代码、路径、语句分别用黑色、红色和蓝色标记。 Visual Studio 编辑器对支持的任何语言自动着色。 此外，当开始输入已知语言关键字或对象时，语句完成会显示可能的语句和对象列表。 语句完成有助于更快速、更轻松地创建代码。

 ![Perl 脚本中的语法着色](../ide/media/vside-perledit.png "VSIDE_PerlEdit")

 对于以下使用 [TextMate 语法](https://manual.macromates.com/en/language_grammars)的语言，Visual Studio 当前提供语法着色和基本语句完成支持。 如果你最喜爱的语言不在表中，别担心，可以添加它。

|||||||
|-|-|-|-|-|-|
|Bat|F#|Java|Markdown|Rust|Visual Basic|
|Clojure|前往|JavaDoc|Objective-C|ShaderLab|Visual C#|
|CMake|Groovy|JSON|Perl|ShellScript|Visual C++|
|CoffeeScript|HTML|LESS|Python|SQL|VBNet|
|CSS|INI|LUA|R|Swift|XML|
|Docker|Jade|品牌|Ruby|TypeScript|YAML|

 除语法着色和基本语句完成外，Visual Studio 还具有一种称为[导航到](https://blogs.msdn.microsoft.com/benwilli/2015/04/09/visual-studio-tip-3-use-navigate-to/)的功能。 可使用此功能快速搜索代码文件、文件路径和代码符号。 Visual Studio 为以下语言提供“导航到”支持。

- 前往

- Java

- JavaScript

- PHP

- TypeScript

- Visual Basic

- Visual C++

- Visual C#

  所有这些文件类型均有上述功能，即使尚未安装对某种语言的支持也是如此。 安装某种语言的专门支持可能会提供其他语言支持，例如 IntelliSense 或其他高级语言功能（如灯泡）。

## <a name="adding-support-for-non-supported-languages"></a>添加对不受支持语言的支持
 Visual Studio 2015 Update 1 及更高版本通过 [TextMate 语法](https://manual.macromates.com/en/language_grammars)在编辑器中提供语言支持。 如果你喜欢的编程语言当前在 Visual Studio 编辑器中不受支持，请先在 Web 上搜索，可能存在该语言的 TextMate 包。 如果还是找不到，可通过创建语言语法和代码段的 TextMate 包模型在 Visual Studio 2015 Update 1 及更高版本中自行添加对该语言的支持。

 在以下文件夹中添加 Visual Studio 的任何新 TextMate 语法：

 %userprofile%\\.vs\Extensions

 如适用，请在此基路径下添加下列文件夹：

|文件夹名|描述|
|-----------------|-----------------|
|\\ *\<language name>*|语言文件夹。 用语言的名称替换 *\<language name>* 。 例如， **\Matlab**。|
|\Syntaxes|语法文件夹。 包含语言的语法 .json 文件，如 **Matlab.json**。|
|\Snippets|代码段文件夹。 包含语言的代码段。|

 在 Windows 中，%userprofile% 解析为路径：c:\Users\\ *\<user name>* 。 如果系统上不存在扩展文件夹，则需要创建它。 如果该文件夹已存在，它将被隐藏。

 有关如何创建 TextMate 语法的详细信息，请参阅 [TextMate – Introduction to Language Grammars: How to add source code syntax highlighting embedded in HTML](https://developmentality.wordpress.com/2011/02/08/textmate-introduction-to-language-grammars/)（TextMate - 语言语法简介：如何在 HTML 中添加嵌入的源代码语法突出显示）和 [Notes on how to create a Language Grammar and Custom Theme for a Textmate Bundle](https://benparizek.com/notebook/notes-on-how-to-create-a-language-grammar-and-custom-theme-for-a-textmate-bundle)（如何创建 Textmate 包的语言语法和自定义主题说明）。

## <a name="see-also"></a>请参阅
 [Visual Studio 2013 导航到改进](https://blogs.msdn.microsoft.com/mvpawardprogram/2013/10/22/visual-studio-2013-navigate-to-improvements/)[演练：创建代码段](../ide/walkthrough-creating-a-code-snippet.md)[演练：显示语句完成](../extensibility/walkthrough-displaying-statement-completion.md)
