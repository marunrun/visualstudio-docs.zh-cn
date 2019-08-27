---
title: 获取开始和结束范围中的字符以编程方式
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, retrieving start and end characters
- end characters
- start characters
- documents [Office development in Visual Studio], retrieving ranges
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8e0f04d5f70c99ea3404a95b04a7ea668a37e0f2
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67328951"
---
# <a name="how-to-programmatically-retrieve-start-and-end-characters-in-ranges"></a>如何：以编程方式检索范围中的开始和结束字符
  此示例演示如何检索范围开始和结束位置的字符位置。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-retrieve-start-and-end-characters-of-a-range-in-a-document-level-customization"></a>检索文档级自定义项中范围的开始和结束字符

1. 获取 <xref:Microsoft.Office.Interop.Word.Range.Start%2A> 的值和 <xref:Microsoft.Office.Interop.Word.Range.End%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Range> 属性。 下面的代码示例获取了文档中第二个语句的开始和结束位置。 若要使用此代码示例，请从项目中的 `ThisDocument` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomation#25](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#25)]
     [!code-csharp[Trin_VstcoreWordAutomation#25](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#25)]

## <a name="to-retrieve-start-and-end-characters-of-a-range-by-using-a-vsto-add-in"></a>若要使用 VSTO 外接程序中检索范围的开始和结束字符

1. 获取 <xref:Microsoft.Office.Interop.Word.Range.Start%2A> 的值和 <xref:Microsoft.Office.Interop.Word.Range.End%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Range> 属性。 下面的代码示例获取了活动文档中第二个语句的开始和结束位置。 若要使用此代码示例，请从项目中的 `ThisAddIn` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#25](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#25)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#25](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#25)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式定义和在文档中选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式扩展文档中的范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [如何：以编程方式重置 Word 文档中的范围](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [如何：以编程方式折叠范围或在文档中的选定内容](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [如何：以编程方式排除段落标记创建范围时](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
- [如何：以编程方式统计文档中的字符](../vsto/how-to-programmatically-count-characters-in-documents.md)
