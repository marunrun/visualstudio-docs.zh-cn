---
title: '重构 (c # ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.csharp.refactoring.preview
- vs.csharp.refactoring.issues
- vs.csharp.refactoring.buildwarning
- VS.PreviewChanges
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#]
ms.assetid: a39e656a-f81f-4c87-b484-a23168ff1dfc
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0415222645dce2f65e91b5b1c55a5a118cc26697
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667501"
---
# <a name="refactoring-c"></a>重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

重构是在编写代码后通过更改代码的内部结构而不更改代码的外部行为来改进代码的过程。

 Visual c # 在 **重构** 菜单上提供了以下重构命令：

- [提取方法重构 (C#)](../csharp-ide/extract-method-refactoring-csharp.md)

- [重命名重构 (C#)](../csharp-ide/rename-refactoring-csharp.md)

- [封装字段重构 (C#)](../csharp-ide/encapsulate-field-refactoring-csharp.md)

- [提取接口重构 (C#)](../csharp-ide/extract-interface-refactoring-csharp.md)

- [移除参数重构 (C#)](../csharp-ide/remove-parameters-refactoring-csharp.md)

- [重新排列参数重构 (C#)](../csharp-ide/reorder-parameters-refactoring-csharp.md)

## <a name="multi-project-refactoring"></a>多项目重构
 对于同一个解决方案中的项目，Visual Studio 支持多项目重构。 跨文件引用的所有重构操作都更正相同语言的所有项目中的引用。 这适用于任何项目到项目的引用。 例如，如果你有一个引用类库的控制台应用程序，则在使用重构操作) 重命名类库类型 (时 `Rename` ，还会更新对控制台应用程序中的类库类型的引用。

## <a name="changes-preview"></a>更改预览
 许多重构操作为您提供了一个机会，使您可以在提交到这些更改之前，查看重构操作对您的代码执行的所有引用更改。 对于这些重构操作，" **预览引用更改** " 选项将显示在 "重构" 对话框中。 选择该选项并接受重构操作后，将显示 " **预览更改" 对话框** 。 请注意，" **预览更改** " 对话框具有两个视图。 底部视图将显示您的代码，其中包含由重构操作导致的所有引用更新。 在 "**预览更改**" 对话框中按 "**取消**" 将停止重构操作，并且不会对代码进行任何更改。

## <a name="refactoring-warnings"></a>重构警告
 如果编译器没有完全了解你的程序，并且重构引擎可能不会更新所有相应的引用，则会显示警告对话框。 使用此警告对话框，还可以在提交更改之前预览 " **预览更改** " 对话框中的代码。

> [!NOTE]
> 如果某个方法包含语法错误 (IDE 使用红色波浪下划线) ，则重构引擎将不会更新该方法内某个元素的任何引用。 下面的示例阐释了这一行为。

 默认情况下，如果在未预览引用更改的情况下执行重构操作，并且在程序中检测到编译错误，则开发环境会显示此警告对话框。

 如果执行具有启用了 **预览引用更改** 的重构操作并在程序中检测到编译错误，则开发环境将在 " **预览更改** " 对话框底部显示以下警告消息，而不是显示 " **重构警告** " 对话框：

 **你的项目或它的某个依赖项当前未生成。引用可能不会更新。**

 此重构警告仅适用于提供 " **预览引用更改** " 选项的重构操作。

## <a name="error-tolerant-refactoring-and-verification-results"></a>容错重构和验证结果
 重构具有容错能力。 换言之，您可以在无法生成的项目中执行重构。 但是，在这种情况下，重构过程可能不会正确地更新不明确的引用。

 如果重构引擎检测到编译错误，或发现重构操作无意中导致代码引用绑定到与最初绑定的内容不同的内容，则 " **验证结果** " 对话框可以通知您)  (重新绑定。

 若要打开验证结果功能，请在 " **工具** " 菜单上单击 " **选项**"。 在 " **选项** " 对话框中，展开 " **文本编辑器**"，然后展开 " **c #**"。 单击 " **高级** "，然后选中 " **验证重构结果** " 复选框。

 " **验证结果** " 对话框区分两种类型的重新绑定问题。

### <a name="references-whose-definition-will-no-longer-be-the-renamed-symbol"></a>其定义将不再是已重命名符号的引用
 当引用不再引用已重命名的符号时，会发生这种重新绑定问题。 例如，考虑以下代码：

```csharp
class Example
{
    private int a;
    public Example(int b)
    {
        a = b;
    }
}
```

 如果使用重构进行重命名 `a` `b` ，则会出现此对话框。 对已重命名的变量的引用 `a` 现在绑定到传递给构造函数的参数，而不是绑定到该字段。

### <a name="references-whose-definition-will-now-become-the-renamed-symbol"></a>其定义现在将变为重命名符号的引用
 如果以前未引用重命名符号的引用现在引用重命名符号，则会发生这种重新绑定问题。 例如，考虑以下代码：

```csharp
class Example
{
    private static void Method(object a) { }
    private static void OtherMethod(int a) { }
    static void Main(string[] args)
    {
        Method(5);
    }
}
```

 如果使用重构进行重命名 `OtherMethod` `Method` ，则会出现此对话框。 现在，中的引用 `Main` 是指接受参数的重载方法， `int` 而不是接受参数的重载方法 `object` 。

## <a name="see-also"></a>另请参阅
 [使用适用于 c # 的 Visual Studio 开发环境](../csharp-ide/using-the-visual-studio-development-environment-for-csharp.md)[如何：还原 c # 重构代码段](../ide/how-to-restore-csharp-refactoring-snippets.md)