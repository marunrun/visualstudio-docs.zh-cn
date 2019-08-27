---
title: 如何：以编程方式隐藏文档中的文本
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], hiding text
- text [Office development in Visual Studio], hiding in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1da471ff1911cdda4a62ef9c150236b3a225342f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812763"
---
# <a name="how-to-programmatically-hide-text-in-documents"></a>如何：以编程方式隐藏文档中的文本
  通过将 <xref:Microsoft.Office.Interop.Word._Font.Hidden%2A> 属性设置为某个特定范围文本的 <xref:Microsoft.Office.Interop.Word.Range.Font%2A> 。

 例如，可以暂时隐藏中的文本<xref:Microsoft.Office.Tools.Word.Bookmark>（在文档级自定义项） 或<xref:Microsoft.Office.Interop.Word.Bookmark>（VSTO 外接程序中） 之前将文档发送到打印机。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-hide-text-in-a-bookmark-control-while-printing-the-document"></a>打印文档时在 Bookmark 控件中隐藏文本

1. 创建一个过程，它会隐藏特定范围内的所有文本。

     [!code-vb[Trin_VstcoreWordAutomation#105](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#105)]
     [!code-csharp[Trin_VstcoreWordAutomation#105](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#105)]

2. 创建一个过程，它会取消隐藏特定范围内的所有文本。

     [!code-vb[Trin_VstcoreWordAutomation#106](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#106)]
     [!code-csharp[Trin_VstcoreWordAutomation#106](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#106)]

3. 将书签的范围传递到 `HideText` 方法，打印文档，然后将相同范围传递到 `UnhideText` 方法。

     下面的代码示例可用于文档级自定义项。 若要使用此示例，请从项目的 `ThisDocument` 类中运行它。

     [!code-vb[Trin_VstcoreWordAutomation#107](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#107)]
     [!code-csharp[Trin_VstcoreWordAutomation#107](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#107)]

     以下代码示例可用于 VSTO 外接程序。 本示例使用活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行它。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#107](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#107)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#107](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#107)]

## <a name="compile-the-code"></a>编译代码
 此代码示例假定文档包含<xref:Microsoft.Office.Tools.Word.Bookmark>控件 （在文档级自定义项） 或<xref:Microsoft.Office.Interop.Word.Bookmark>控件 （在 VSTO 外接程序），名为`bookmark1`。

## <a name="see-also"></a>请参阅
- [如何：以编程方式打印文档](../vsto/how-to-programmatically-print-documents.md)
- [如何：以编程方式定义和在文档中选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式重置 Word 文档中的范围](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [如何：以编程方式更新书签文本](../vsto/how-to-programmatically-update-bookmark-text.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
