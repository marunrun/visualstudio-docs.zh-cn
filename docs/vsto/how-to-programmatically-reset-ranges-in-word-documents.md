---
title: 如何：以编程方式重置 Word 文档中的范围
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], resetting ranges
- ranges, resetting in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 622d807da832c4c07baf8b62c902c2b1d25cc14d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955689"
---
# <a name="how-to-programmatically-reset-ranges-in-word-documents"></a>如何：以编程方式重置 Word 文档中的范围
  使用 <xref:Microsoft.Office.Interop.Word.Range.SetRange%2A> 方法在 Microsoft Office Word 文档中调整现有范围的大小。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-reset-an-existing-range"></a>重置现有范围

1. 设置从文档中的前七个字符开始的初始范围。

     下面的代码示例可用于文档级自定义项。

     [!code-vb[Trin_VstcoreWordAutomation#43](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#43)]
     [!code-csharp[Trin_VstcoreWordAutomation#43](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#43)]

     以下代码示例可用于 VSTO 外接程序。 此代码运用了活动文档。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#43](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#43)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#43](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#43)]

2. 使用 <xref:Microsoft.Office.Interop.Word.Range.SetRange%2A> 设置第二个句子为范围的起始位置，第五个句子为结束位置。

     [!code-vb[Trin_VstcoreWordAutomation#44](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#44)]
     [!code-csharp[Trin_VstcoreWordAutomation#44](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#44)]

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="to-reset-an-existing-range-in-a-document-level-customization"></a>在文档级自定义项中重置现有范围

1. 下面的示例显示文档级自定项的完整示例。 若要使用此代码，请从项目中的 `ThisDocument` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomation#42](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#42)]
     [!code-csharp[Trin_VstcoreWordAutomation#42](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#42)]

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="to-reset-an-existing-range-in-a-vsto-add-in"></a>若要重置现有范围 VSTO 外接程序中

1. 下面的示例显示 VSTO 外接程序的完整的示例。 若要使用此代码，请从项目中的 `ThisAddIn` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#42](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#42)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#42](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#42)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式扩展文档中的范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [如何：以编程方式定义和在文档中选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式检索范围中的开始和结束字符](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [如何：以编程方式折叠范围或在文档中的选定内容](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
