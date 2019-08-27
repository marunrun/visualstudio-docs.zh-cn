---
title: 如何：以编程方式使用 Word 中的内置对话框
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: f8037e4d91aa7706c7ffd7b9f32778dfeac79488
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62961636"
---
# <a name="how-to-programmatically-use-built-in-dialog-boxes-in-word"></a>如何：以编程方式使用 Word 中的内置对话框
  在使用 Microsoft Office Word，有些的时候需要显示用户输入的对话框。 尽管可以创建你自己，但可能还想要采用的使用在 Word 中，内置对话框框中公开的方法<xref:Microsoft.Office.Interop.Word.Dialogs>的集合<xref:Microsoft.Office.Interop.Word.Application>对象。 这使您能够访问 200 的内置对话框框中，以枚举表示。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="display-dialog-boxes"></a>显示的对话框
 若要显示一个对话框，使用的值之一<xref:Microsoft.Office.Interop.Word.WdWordDialog>枚举，以创建<xref:Microsoft.Office.Interop.Word.Dialog>对象，表示你想要显示的对话框。 然后，调用<xref:Microsoft.Office.Interop.Word.Dialog.Show%2A>方法的<xref:Microsoft.Office.Interop.Word.Dialog>对象。

 下面的代码示例演示如何显示**文件打开**对话框。 若要使用此示例中，可以从运行`ThisDocument`或`ThisAddIn`在项目中的类。

 [!code-vb[Trin_VstcoreWordAutomation#100](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#100)]
 [!code-csharp[Trin_VstcoreWordAutomation#100](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#100)]

### <a name="access-dialog-box-members-that-are-available-through-late-binding"></a>可通过后期绑定访问对话框框成员
 某些属性和方法在 Word 中的对话框是只能通过后期绑定。 在 Visual Basic 中项目的位置**Option Strict**处于打开状态，必须使用反射来访问这些成员。 有关详细信息，请参阅[在 Office 解决方案中的后期绑定](../vsto/late-binding-in-office-solutions.md)。

 下面的代码示例演示如何使用**名称**的属性**文件打开**对话框中，在 Visual Basic 中的项目的位置**Option Strict**是关闭或在 Visual C#项目面向[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]。 若要使用此示例中，可以从运行`ThisDocument`或`ThisAddIn`在项目中的类。

 [!code-vb[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#122)]
 [!code-csharp[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#122)]

 下面的代码示例演示如何使用反射来访问**名称**的属性**文件打开**对话框中，在 Visual Basic 中的项目的位置**Option Strict**是上。 若要使用此示例中，可以从运行`ThisDocument`或`ThisAddIn`在项目中的类。

 [!code-vb[Trin_VstcoreWordAutomation#102](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#102)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式使用在隐藏模式下的 Word 对话框](../vsto/how-to-programmatically-use-word-dialog-boxes-in-hidden-mode.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [Option strict 语句](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [反射 (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [反射 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
