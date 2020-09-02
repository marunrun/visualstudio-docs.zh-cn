---
title: Office 解决方案中的后期绑定
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- objects [Office development in Visual Studio], casting
- types [Office development in Visual Studio], casting
- automation [Office development in Visual Studio], casting objects
- casting, object to specific type
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 62224006d04e0a1e7447053e868dd9946f00c97e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62583934"
---
# <a name="late-binding-in-office-solutions"></a>Office 解决方案中的后期绑定
  Office 应用程序的对象模型中的某些类型提供可通过后期绑定功能获得的功能。 例如，某些方法和属性可以根据 Office 应用程序的上下文返回不同类型的对象，并且某些类型可以在不同的上下文中公开不同的方法或属性。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Visual Basic **选项 Strict** 处于关闭状态的项目和面向或的 Visual c # 项目 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 可以直接与使用这些后期绑定功能的类型配合使用。

## <a name="implicit-and-explicit-casting-of-object-return-values"></a>对象返回值的隐式和显式强制转换
 Microsoft Office 主互操作程序集中的许多方法和属性 (Pia) 返回 <xref:System.Object> 值，因为它们可以返回多个不同类型的对象。 例如， <xref:Microsoft.Office.Tools.Excel.Workbook.ActiveSheet%2A> 属性返回， <xref:System.Object> 因为其返回值可以是 <xref:Microsoft.Office.Interop.Excel.Worksheet> 或 <xref:Microsoft.Office.Interop.Excel.Chart> 对象，具体取决于活动工作表的内容。

 当方法或属性返回时 <xref:System.Object> ，必须显式将) Visual Basic 中的 (转换为 **选项 Strict** 所在 Visual Basic 项目中的正确类型。 不需要 <xref:System.Object> 在 **选项 Strict** 处于关闭状态 Visual Basic 项目中显式转换返回值。

 在大多数情况下，引用文档列出了返回的成员的返回值的可能类型 <xref:System.Object> 。 转换或强制转换对象可在代码编辑器中为对象启用 IntelliSense。

 有关 Visual Basic 中的转换的信息，请参阅 &#40;Visual Basic&#41;和[CType 函数 &#40;](/dotnet/visual-basic/language-reference/functions/ctype-function)Visual Basic&#41;中的[隐式和显式转换](/dotnet/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions)。

### <a name="examples"></a>示例
 下面的代码示例演示如何将对象强制转换为 Visual Basic 项目中的特定类型，其中 **Option Strict** 为 on。 在此类型的项目中，必须将属性显式转换 <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A> 为 <xref:Microsoft.Office.Interop.Excel.Range> 。 此示例需要一个文档级 Excel 项目，其中包含一个名为的工作表类 `Sheet1` 。

 [!code-vb[Trin_VstcoreProgramming#9](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb#9)]

 下面的代码示例演示如何将对象隐式转换为 Visual Basic 项目中的一个特定类型，其中 **Option Strict** 为 off，或为面向的 Visual c # 项目 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 。 在这些类型的项目中， <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A> 属性隐式强制转换为 <xref:Microsoft.Office.Interop.Excel.Range> 。 此示例需要一个文档级 Excel 项目，其中包含一个名为的工作表类 `Sheet1` 。

 [!code-vb[Trin_VstcoreProgramming#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb#10)]
 [!code-csharp[Trin_VstcoreProgramming#10](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/Sheet1.cs#10)]

## <a name="access-members-that-are-available-only-through-late-binding"></a>仅可通过后期绑定访问的成员
 Office Pia 中的某些属性和方法只能通过后期绑定提供。 在 **选项 Strict** 处于关闭状态的 Visual Basic 项目或面向或的 Visual c # 项目中 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] ，您可以使用这些语言的后期绑定功能访问后期绑定成员。 在 **选项 Strict** 处于 Visual Basic 的项目中，必须使用反射来访问这些成员。

### <a name="examples"></a>示例
 下面的代码示例演示如何访问 Visual Basic 项目中 **Option Strict** 为 off 或面向的 Visual c # 项目中的后期绑定成员 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 。 此示例访问 Word 中 "**文件打开**" 对话框的后期绑定**名称**属性。 若要使用此示例，请从 `ThisDocument` `ThisAddIn` Word 项目中的或类中运行它。

 [!code-vb[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#122)]
 [!code-csharp[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#122)]

 下面的代码示例演示如何使用反射来完成 Visual Basic 项目中的相同任务，其中 **Option Strict** 为 on。

 [!code-vb[Trin_VstcoreWordAutomation#102](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#102)]

## <a name="see-also"></a>另请参阅
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [使用类型动态 &#40;C&#35; 编程指南&#41;](/dotnet/csharp/programming-guide/types/using-type-dynamic)
- [Option Strict 语句](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [反射 (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [反射 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
