---
title: 重构 (C#) |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: fa8fbfd8837fb35617b79089fffd11ea3b8d2e93
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444528"
---
# <a name="refactoring-c"></a>重构 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

重构是写入通过更改代码的内部结构，而无需更改代码的外部行为后，改进您的代码的过程。  
  
 Visual C# 上提供以下重构命令**重构**菜单：  
  
- [提取方法重构 (C#)](../csharp-ide/extract-method-refactoring-csharp.md)  
  
- [重命名重构 (C#)](../csharp-ide/rename-refactoring-csharp.md)  
  
- [封装字段重构 (C#)](../csharp-ide/encapsulate-field-refactoring-csharp.md)  
  
- [提取接口重构 (C#)](../csharp-ide/extract-interface-refactoring-csharp.md)  
  
- [移除参数重构 (C#)](../csharp-ide/remove-parameters-refactoring-csharp.md)  
  
- [重新排列参数重构 [C#]](../csharp-ide/reorder-parameters-refactoring-csharp.md)  
  
## <a name="multi-project-refactoring"></a>多项目重构  
 Visual Studio 支持多项目重构用于项目的同一解决方案中。 更正文件中引用的重构操作的所有更正这些引用在同一语言的所有项目。 这适用于任何项目到项目引用。 例如，如果已重命名类库类型时引用的类库的控制台应用程序 (使用`Rename`重构操作)，还将更新对该控制台应用程序中的类库类型的引用。  
  
## <a name="changes-preview"></a>更改预览  
 许多重构操作，提供以供查看的重构操作将对代码执行，对这些更改在提交之前的所有引用更改的机会。 重构操作，这些**预览引用更改**重构对话框中将出现选项。 选择该选项并接受重构操作之后,**预览更改对话框**将出现。 请注意，**预览更改**对话框具有两个视图。 下部的视图将显示使用由于重构操作的所有引用更新你的代码。 按下**取消**上**预览更改**对话框将停止重构操作，并将对你的代码进行任何更改。  
  
## <a name="refactoring-warnings"></a>重构警告  
 如果编译器没有全面了解您的程序，并且可以重构引擎可能不会更新所有适当的引用，将显示警告对话框。 此警告对话框中还提供了您可以预览中的代码有机会**预览更改**对话框之前提交的更改。  
  
> [!NOTE]
> 如果方法包含语法错误 （从而以红色的波浪下划线指示 IDE），然后重构引擎不会更新对该方法中的某个元素的任何引用。 下面的示例阐释了这一点。  
  
 默认情况下，如果您执行重构操作而不预览引用更改和编译错误检测到在应用程序中，然后开发环境将显示此警告对话框。  
  
 如果您执行的重构操作，具有**预览引用更改**启用和编译错误检测到在应用程序中，则在开发环境将在底部显示以下警告消息**预览更改**对话框中的，而不会显示**重构警告**对话框：  
  
 **当前未生成项目或其依赖项之一。引用可能不会更新。**  
  
 此重构的警告功能仅适用于重构提供的操作**预览引用更改**选项。  
  
## <a name="error-tolerant-refactoring-and-verification-results"></a>容错重构和验证结果  
 重构是容错的错误。 换而言之，可以执行一个重构无法生成的项目中。 但是，在这些情况下重构过程可能不明确的引用正确更新。  
  
 **验证结果**对话框可以在重构引擎检测到编译错误或发现重构操作意外导致的代码引用绑定到不同的是什么内容时通知你最初绑定到 （重新绑定问题）。  
  
 若要启用验证结果功能，请在**工具**菜单上，单击**选项**。 在中**选项**对话框框中，展开**文本编辑器**，然后展开**C#**。 单击**高级**，然后选择**验证重构结果**复选框。  
  
 **验证结果**对话框区分两种类型的重新绑定问题之间的差异。  
  
### <a name="references-whose-definition-will-no-longer-be-the-renamed-symbol"></a>其定义将不再是重命名的符号引用  
 引用不再引用已重命名符号时发生这种重新绑定问题。 例如，考虑以下代码：  
  
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
  
 如果使用重构重命名`a`到`b`，会显示此对话框。 引用已重命名变量`a`现在绑定到传递给构造函数而不是绑定到字段的参数。  
  
### <a name="references-whose-definition-will-now-become-the-renamed-symbol"></a>其定义现在将成为已重命名的符号引用  
 以前未引用已重命名符号现在的引用 does 引用已重命名符号时，会发生这种重新绑定问题。 例如，考虑以下代码：  
  
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
  
 如果使用重构重命名`OtherMethod`到`Method`，会显示此对话框。 中的引用`Main`现在是指接受的重载方法`int`参数而不是接受的重载方法`object`参数。  
  
## <a name="see-also"></a>请参阅  
 [使用适用于 C# Visual Studio 开发环境](../csharp-ide/using-the-visual-studio-development-environment-for-csharp.md)   
 [如何：还原 C# 重构代码段](../ide/how-to-restore-csharp-refactoring-snippets.md)