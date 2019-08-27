---
title: 如何：使用表达式编辑器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.ExpressionTextBox.UI
ms.assetid: b5f961dd-6dda-41a9-9cae-0383d479ef3d
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: cc876426c18184c966c277e8dafb5a373da332b7
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63408385"
---
# <a name="how-to-use-the-expression-editor"></a>如何：使用表达式编辑器
表达式编辑器是许多工作流活动中使用的 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 控件，用于输入和计算这些表达式。 表达式编辑器提供全面的 IDE 编辑体验，包括 IntelliSense、着色、ParamInfo、错误波形曲线和其他功能。 编译器在表达式输入后对它进行验证。 如果表达式无效，则显示一个错误图标。 此外可以为打开编辑器**表达式编辑器**对话框。  
  
 表达式是绑定到自变量或属性的文本值或 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 代码。 表达式包含与操作进行组合以生成新值的值元素（如变量、常量、文本、属性）。 表达式使用 VB.NET 语法编写，即使应用程序使用 C# 编程也如此。 这意味着，大小写并不重要，则执行比较，使用单等号 （=） 符号而非 （"= ="）、 布尔运算符是单词"和"和"而不是符号"& &"和"&#124;&#124;"，并**执行任何操作**而不是使用**null**。 有关详细信息表达式和运算符中的[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]和一些示例，请参阅[运算符和表达式在 Visual Basic 中的](http://go.microsoft.com/fwlink/?LinkId=186818)。  
  
 **表达式编辑器**行为，如下所示：  
  
- 当焦点不在表达式编辑器上时，该编辑器看上去像一个常规 TextBlock 控件。  
  
- 当焦点在表达式编辑器上时，该编辑器的外观和行为都类似于表达式编辑器控件。 当它失去焦点后，看上去又像一个常规 TextBlock 了。  
  
- 如果在重新承载的工作流设计器中将焦点置于表达式编辑器，则该编辑器的行为类似于 TextBox。 当在重新承载的工作流设计器中失去焦点后，表达式编辑器看上去又像一个常规 TextBlock 了。  
  
> [!NOTE]
> 表达式编辑器的 IntelliSense 仅在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 内可用。 在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 和重新承载的方案中，编译器在表达式输入后对它进行验证，如果该表达式无效，则表达式编辑器将显示一个错误图标。  
  
### <a name="using-the-expression-editor"></a>使用表达式编辑器  
  
1. 在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中，打开一个新的或现有的工作流项目。  
  
2. 向工作流添加诸如 <xref:System.Activities.Statements.Assign> 之类的活动。  
  
    > [!NOTE]
    > 多种工作流活动具有表达式编辑器。 表达式 TextBlock 还显示在变量设计器、自变量设计器和动态自变量设计器中。 <xref:System.Activities.Statements.Assign> 活动用作一个示例。  
  
3. 在 <xref:System.Activities.Statements.Assign> 活动的活动设计器中单击左侧表达式编辑器。  
  
     灰色水印字符串 **\<到>** 并 **\<输入 VB 表达式>** 是默认文本字符串中的表达式编辑器<xref:System.Activities.Statements.Assign>活动。  
  
4. 输入表达式。 如果您输入一个字符串，请确保在该字符串两端加上引号。 如果你选择将表达式自变量绑定到一个变量，请不要使用引号。  
  
     完成后，请选中表达式编辑器外的一个区域以便将焦点移到设计器的其他部分。 这将使编译器如前所述验证该表达式。  
  
     输入/编辑表达式的另一个方法是在属性网格中单击属性名旁的省略号。 这将打开**表达式编辑器**为对话框。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Activities.Presentation.View.ExpressionTextBox>