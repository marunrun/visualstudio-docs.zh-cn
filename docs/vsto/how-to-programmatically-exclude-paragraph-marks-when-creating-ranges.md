---
title: 以编程方式创建范围时排除段落标记
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], excluding paragraphs
- ranges, excluding paragraph marks in Word
- documents [Office development in Visual Studio], paragraph marks
- paragraphs, controlling structure
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 852dc6c51215e00c1fdc1571f51940a44f727794
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402145"
---
# <a name="how-to-programmatically-exclude-paragraph-marks-when-creating-ranges"></a>如何：以编程方式排除段落标记创建范围时
  当你创建基于段落的 <xref:Microsoft.Office.Interop.Word.Range> 对象时，所有非打印字符（如段落标记）都将纳入范围。 可将源段落的文本插入到目标段落。 如果不希望将目标段落拆分为单独的段落，则必须先从源段落中删除段落标记。 此外，由于段落标记中存储着段落格式设置信息，所以当你将范围插入到现有段落时可能需要删除它。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 以下示例过程声明两个字符串变量，检索活动文档中的第一个和第二个段落的内容，然后交换它们的内容。 随后，该示例将演示如何通过使用 <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> 方法并在段落中插入文本，从范围中删除段落标记。

## <a name="to-control-paragraph-structure-when-inserting-text"></a>在插入文本时控制段落结构

1. 为第一个和第二个段落创建两个范围变量，并使用 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> 属性检索其内容。

     下面的代码示例可用于文档级自定义项。

     [!code-vb[Trin_VstcoreWordAutomation#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#27)]
     [!code-csharp[Trin_VstcoreWordAutomation#27](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#27)]

     以下代码示例可用于应用程序级 VSTO 外接程序。 此代码运用了活动文档。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#27)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#27](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#27)]

2. 分配 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> 属性，在两个段落间交换文本。

     [!code-vb[Trin_VstcoreWordAutomation#28](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#28)]
     [!code-csharp[Trin_VstcoreWordAutomation#28](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#28)]

3. 依次选择每个范围并暂停，在消息框中显示结果。

     [!code-vb[Trin_VstcoreWordAutomation#29](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#29)]
     [!code-csharp[Trin_VstcoreWordAutomation#29](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#29)]

4. 使用 `firstRange` 方法调整 <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> ，使 `firstRange`中不再含有段落标记。

     [!code-vb[Trin_VstcoreWordAutomation#30](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#30)]
     [!code-csharp[Trin_VstcoreWordAutomation#30](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#30)]

5. 替换第一个段落中的剩余文本，向该范围的 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> 属性分配一个新字符串。

     [!code-vb[Trin_VstcoreWordAutomation#31](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#31)]
     [!code-csharp[Trin_VstcoreWordAutomation#31](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#31)]

6. 替换 `secondRange`中的文本，包括段落标记。

     [!code-vb[Trin_VstcoreWordAutomation#32](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#32)]
     [!code-csharp[Trin_VstcoreWordAutomation#32](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#32)]

7. 选择 `firstRange` 并暂停以便在消息框中显示结果，然后对 `secondRange`执行相同操作。

     由于已将 `firstRange` 重定义为排除段落标记，所以保留了该段落的原始格式。 但是，在 `secondRange`中的段落标记上插入了句子，从而删除了单独的段落。

     [!code-vb[Trin_VstcoreWordAutomation#33](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#33)]
     [!code-csharp[Trin_VstcoreWordAutomation#33](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#33)]

     两个区域的原始内容均保存为字符串，因此你可以将文档还原到其原始状态。

8. 重新调整`firstRange`若要使用包括段落标记<xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A>一个字符位置的方法。

     [!code-vb[Trin_VstcoreWordAutomation#34](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#34)]
     [!code-csharp[Trin_VstcoreWordAutomation#34](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#34)]

9. 删除 `secondRange`。 此操作将第三个段落还原到其原始位置。

     [!code-vb[Trin_VstcoreWordAutomation#35](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#35)]
     [!code-csharp[Trin_VstcoreWordAutomation#35](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#35)]

10. 还原 `firstRange`中的原始段落文本。

     [!code-vb[Trin_VstcoreWordAutomation#36](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#36)]
     [!code-csharp[Trin_VstcoreWordAutomation#36](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#36)]

11. 使用 <xref:Microsoft.Office.Interop.Word.Range.InsertAfter%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Range> 方法，将第二个段落的原始内容插入到 `firstRange`之后，并选择 `firstRange`。

     [!code-vb[Trin_VstcoreWordAutomation#37](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#37)]
     [!code-csharp[Trin_VstcoreWordAutomation#37](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#37)]

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="to-control-paragraph-structure-when-inserting-text-in-document-level-customizations"></a>在文档级自定义项中插入文本时控制段落结构

1. 下面的示例显示针对文档级自定项的完整方法。 若要使用此代码，请从项目中的 `ThisDocument` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomation#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#26)]
     [!code-csharp[Trin_VstcoreWordAutomation#26](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#26)]

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="to-control-paragraph-structure-when-inserting-text-in-a-vsto-add-in"></a>VSTO 外接程序中插入文本时控制段落结构

1. 下面的示例显示 VSTO 外接程序的完整的方法。 若要使用此代码，请从项目中的 `ThisAddIn` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#26)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#26](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#26)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式扩展文档中的范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [如何：以编程方式折叠范围或在文档中的选定内容](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [如何：以编程方式向 Word 文档中插入文本](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [如何：以编程方式重置 Word 文档中的范围](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [如何：以编程方式定义和在文档中选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
