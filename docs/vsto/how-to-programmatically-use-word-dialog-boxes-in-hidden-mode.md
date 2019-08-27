---
title: 如何：以编程方式使用在隐藏模式下的 Word 对话框
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden dialog boxes
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, hidden mode in Word
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e7a422e9548fabefa2066fb439c01e382586cd36
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62961600"
---
# <a name="how-to-programmatically-use-word-dialog-boxes-in-hidden-mode"></a>如何：以编程方式使用在隐藏模式下的 Word 对话框
  可以通过调用 Microsoft Office Word 中的内置对话框而不会向用户显示其执行复杂的操作通过一个方法调用。 您可以执行此操作通过使用<xref:Microsoft.Office.Interop.Word.Dialog.Execute%2A>方法<xref:Microsoft.Office.Interop.Word.Dialog>对象而无需调用<xref:Microsoft.Office.Interop.Word.Dialog.Display%2A>方法。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="examples"></a>示例
 下面的代码示例演示如何使用**页面设置**在隐藏模式下设置多个页面无用户输入的安装属性对话框。 这些示例使用<xref:Microsoft.Office.Interop.Word.Dialog>对象以配置自定义页面大小。 页面设置、 上边距、 下边距等，如的特定设置是后期绑定属性的形式提供<xref:Microsoft.Office.Interop.Word.Dialog>对象。 这些属性是在运行时动态创建的 Word。

 下面的示例演示如何在 Visual Basic 项目中执行此任务在其中**Option Strict**已关闭，且在 Visual C# 项目中面向[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。 在这些项目中，可以在 Visual Basic 和 Visual C# 编译器中使用后期绑定功能。 若要使用此示例中，可以从运行`ThisDocument`或`ThisAddIn`在项目中的类。

 [!code-vb[Trin_VstcoreWordAutomation#123](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#123)]
 [!code-csharp[Trin_VstcoreWordAutomation#123](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#123)]

 下面的示例演示如何在 Visual Basic 项目中执行此任务在其中**Option Strict**上。 在这些项目中，必须使用反射来访问后期绑定属性。 若要使用此示例中，可以从运行`ThisDocument`或`ThisAddIn`在项目中的类。

 [!code-vb[Trin_VstcoreWordAutomation#104](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#104)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式使用 Word 中的内置对话框](../vsto/how-to-programmatically-use-built-in-dialog-boxes-in-word.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [在 Office 解决方案中的后期绑定](../vsto/late-binding-in-office-solutions.md)
- [反射 (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [反射 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
