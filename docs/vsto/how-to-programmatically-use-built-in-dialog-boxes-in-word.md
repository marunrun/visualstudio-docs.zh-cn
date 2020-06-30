---
title: 如何：以编程方式使用 Word 中的内置对话框
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, Word
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2c3273b22d98be1c22cf0c8cea2cb57e277b9b48
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537613"
---
# <a name="how-to-programmatically-use-built-in-dialog-boxes-in-word"></a>如何：以编程方式使用 Word 中的内置对话框
  使用 Microsoft Office Word 时，有时需要显示用户输入的对话框。 虽然您可以创建自己的，但您可能还希望采用使用 Word 中的内置对话框（在对象的集合中公开）的方法 <xref:Microsoft.Office.Interop.Word.Dialogs> <xref:Microsoft.Office.Interop.Word.Application> 。 这使您可以访问200的内置对话框，这些对话框以枚举形式表示。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="display-dialog-boxes"></a>显示对话框
 若要显示对话框，请使用枚举的值之一 <xref:Microsoft.Office.Interop.Word.WdWordDialog> 来创建 <xref:Microsoft.Office.Interop.Word.Dialog> 表示要显示的对话框的对象。 然后，调用 <xref:Microsoft.Office.Interop.Word.Dialog.Show%2A> 对象的方法 <xref:Microsoft.Office.Interop.Word.Dialog> 。

 下面的代码示例演示如何显示 "**打开文件**" 对话框。 若要使用此示例，请从 `ThisDocument` 项目的或 `ThisAddIn` 类中运行它。

 [!code-vb[Trin_VstcoreWordAutomation#100](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#100)]
 [!code-csharp[Trin_VstcoreWordAutomation#100](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#100)]

### <a name="access-dialog-box-members-that-are-available-through-late-binding"></a>可通过后期绑定获得的访问对话框成员
 Word 中的某些属性和方法仅通过后期绑定提供。 在**选项 Strict**处于 Visual Basic 的项目中，必须使用反射来访问这些成员。 有关详细信息，请参阅[Office 解决方案中的后期绑定](../vsto/late-binding-in-office-solutions.md)。

 下面的代码示例演示了如何在**选项 Strict**为 off 的项目或面向的 Visual c # 项目中，使用 "**文件打开**" 对话框的 "**名称**" 属性 Visual Basic [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 。 若要使用此示例，请从 `ThisDocument` 项目的或 `ThisAddIn` 类中运行它。

 [!code-vb[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#122)]
 [!code-csharp[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#122)]

 下面的代码示例演示了如何使用反射来访问 "**文件打开**" 对话框的 "**名称**" 属性，该属性位于**Option Strict** Visual Basic 的项目中。 若要使用此示例，请从 `ThisDocument` 项目的或 `ThisAddIn` 类中运行它。

 [!code-vb[Trin_VstcoreWordAutomation#102](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#102)]

## <a name="see-also"></a>另请参阅
- [如何：以编程方式在隐藏模式下使用 Word 对话框](../vsto/how-to-programmatically-use-word-dialog-boxes-in-hidden-mode.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [Option strict 语句](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [反射 (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [反射 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
