---
title: 工作流设计器-如何：使用表达式编辑器
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.ExpressionTextBox.UI
ms.assetid: b5f961dd-6dda-41a9-9cae-0383d479ef3d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 04c0fdaab87c88028b8c14ca59e93fa93e74be74
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817432"
---
# <a name="how-to-use-the-expression-editor"></a>如何：使用表达式编辑器

表达式编辑器是在许多工作流活动中用于输入和计算表达式的工作流设计器控件。 表达式编辑器提供了一个完整的 IDE 编辑体验，包括 IntelliSense、着色、ParamInfo、错误波形曲线和其他功能。 编译器在表达式输入后对其进行验证。 如果表达式无效，则显示一个错误图标。 编辑器还可以作为 "**表达式编辑器**" 对话框打开。

表达式是绑定到参数或属性的文本值或 Visual Basic 代码。 它们包含值元素（例如变量、常量、文本、属性），这些值元素与操作组合起来产生新值。 表达式使用 VB.NET 语法编写，即使应用程序使用 C# 编程也如此。 这意味着，大小写并不重要，使用单个等号（"=" 而不是 "= ="）执行比较时，布尔运算符是单词 "and" 和 "or"，而不是使用符号 "&&" 和 "| |"，而是不使用**任何**值（而不是**null**）。 有关 Visual Basic 和中的表达式和运算符的详细信息，请参阅[Visual Basic 中的运算符和表达式](/previous-versions/visualstudio/visual-studio-2010/a1w3te48(v=vs.100))。

**表达式编辑器**的行为如下所示：

- 当焦点不在表达式编辑器上时，该编辑器看上去像一个常规 TextBlock 控件。

- 当焦点在表达式编辑器上时，该编辑器的外观和行为都类似于表达式编辑器控件。 失去焦点后，表达式编辑器将再次看起来像是一个普通的 TextBlock。

- 如果在重新承载的工作流设计器中将焦点置于表达式编辑器，则该编辑器的行为类似于 TextBox。 当在重新承载的工作流设计器中失去焦点后，表达式编辑器看上去又像一个常规 TextBlock 了。

> [!NOTE]
> 表达式编辑器的 IntelliSense 仅在 Visual Studio 内可用。 在 Visual Studio 和重新承载方案中，编译器会在输入表达式后对其进行验证，如果表达式无效，则表达式编辑器会显示错误图标。

## <a name="use-the-expression-editor"></a>使用表达式编辑器

1. 在 Visual Studio 中，打开一个新的或现有的工作流项目。

2. 向工作流添加诸如 <xref:System.Activities.Statements.Assign> 之类的活动。

    > [!NOTE]
    > 多种工作流活动具有表达式编辑器。 表达式 TextBlock 还显示在变量设计器、自变量设计器和动态自变量设计器中。 <xref:System.Activities.Statements.Assign> 活动用作一个示例。

3. 在 <xref:System.Activities.Statements.Assign> 活动的活动设计器中单击左侧表达式编辑器。

     灰色水印字符串 **\<To>** 和 **\<Enter a VB Expression>** 是活动中表达式编辑器的默认文本字符串 <xref:System.Activities.Statements.Assign> 。

4. 输入表达式。 如果您输入一个字符串，请确保在该字符串两端加上引号。 如果你选择将表达式自变量绑定到一个变量，请不要使用引号。

     完成后，选择 "表达式编辑器" 之外的区域或区域，将焦点移动到设计器的另一部分。 移位焦点将导致编译器验证表达式，如前文所述。

     输入或编辑表达式的另一种方法是在属性网格中单击属性名称旁边的省略号。 选择省略号会将 "**表达式编辑器**" 作为对话框打开。

## <a name="see-also"></a>请参阅

- <xref:System.Activities.Presentation.View.ExpressionTextBox>
