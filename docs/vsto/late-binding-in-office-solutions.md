---
title: 在 Office 解决方案中的后期绑定
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62583934"
---
# <a name="late-binding-in-office-solutions"></a>在 Office 解决方案中的后期绑定
  Office 应用程序的对象模型中的某些类型提供可通过后期绑定功能的功能。 例如，一些方法和属性可以返回不同类型的对象，具体取决于 Office 应用程序的上下文和某些类型可以公开不同的方法或不同的上下文中的属性。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Visual Basic 项目的位置**Option Strict**是关闭和 VisualC#项目面向[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]可以直接使用采用这些后期绑定功能的类型。

## <a name="implicit-and-explicit-casting-of-object-return-values"></a>对象的隐式和显式强制转换返回值
 很多方法和属性在 Microsoft Office 主互操作程序集 (Pia) 返回<xref:System.Object>值，因为它们可以返回多个不同类型的对象。 例如，<xref:Microsoft.Office.Tools.Excel.Workbook.ActiveSheet%2A>属性返回<xref:System.Object>因为其返回值可以是<xref:Microsoft.Office.Interop.Excel.Worksheet>或<xref:Microsoft.Office.Interop.Excel.Chart>对象，具体取决于活动工作表是什么。

 当方法或属性返回<xref:System.Object>，你必须显式 （在 Visual Basic) 将对象转换为正确的类型在 Visual Basic 项目位置**Option Strict**上。 不需要显式强制转换<xref:System.Object>在 Visual Basic 项目中返回值， **Option Strict**处于关闭状态。

 在大多数情况下，参考文档列出了可能的返回值类型成员返回<xref:System.Object>。 转换或将对象强制转换为对象代码编辑器中启用 IntelliSense。

 有关在 Visual Basic 中的转换的信息，请参阅[隐式转换和显式转换&#40;Visual Basic&#41; ](/dotnet/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions)并[CType 函数&#40;Visual Basic&#41;](/dotnet/visual-basic/language-reference/functions/ctype-function)。

### <a name="examples"></a>示例
 下面的代码示例演示如何在 Visual Basic 项目中强制转换为特定类型的对象位置**Option Strict**上。 在此类型的项目，必须显式强制转换<xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A>属性设置为<xref:Microsoft.Office.Interop.Excel.Range>。 此示例需要使用一个名为的工作表类的文档级 Excel 项目`Sheet1`。

 [!code-vb[Trin_VstcoreProgramming#9](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb#9)]

 下面的代码示例演示如何隐式转换为特定类型的对象在 Visual Basic 项目中位置**Option Strict**关闭或视觉对象处于C#目标项目[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。 在这些类型的项目，<xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A>属性隐式转换为<xref:Microsoft.Office.Interop.Excel.Range>。 此示例需要使用一个名为的工作表类的文档级 Excel 项目`Sheet1`。

 [!code-vb[Trin_VstcoreProgramming#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb#10)]
 [!code-csharp[Trin_VstcoreProgramming#10](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/Sheet1.cs#10)]

## <a name="access-members-that-are-available-only-through-late-binding"></a>仅通过后期绑定访问成员
 只能通过后期绑定的一些属性和 Office Pia 中的方法。 在 Visual Basic 中项目的位置**Option Strict**已关闭或视觉对象中C#项目面向[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]，可以使用这些语言中的后期绑定功能访问后期绑定成员。 在 Visual Basic 中项目的位置**Option Strict**处于打开状态，必须使用反射来访问这些成员。

### <a name="examples"></a>示例
 下面的代码示例演示如何访问 Visual Basic 项目中的后期绑定成员，其中**Option Strict**关闭或视觉对象处于C#目标项目[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。 此示例访问后期绑定**名称**的属性**文件打开**在 Word 中的对话框。 若要使用此示例中，可以从运行`ThisDocument`或`ThisAddIn`Word 项目中的类。

 [!code-vb[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#122)]
 [!code-csharp[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#122)]

 下面的代码示例演示如何使用反射来完成相同的任务在 Visual Basic 项目中位置**Option Strict**上。

 [!code-vb[Trin_VstcoreWordAutomation#102](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#102)]

## <a name="see-also"></a>请参阅
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [使用类型 dynamic &#40;C&#35;编程指南&#41;](/dotnet/csharp/programming-guide/types/using-type-dynamic)
- [Option Strict 语句](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [反射 (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [反射 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
