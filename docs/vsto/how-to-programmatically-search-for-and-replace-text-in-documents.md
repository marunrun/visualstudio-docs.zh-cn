---
title: 以编程方式查找和替换文档中的文本
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], searching
- text searches, replacing text
- text searches, documents
- text [Office development in Visual Studio], searching in documents
- text [Office development in Visual Studio], text searches
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 18a50d6d4ef52a0c50be0b72b4cab5706da4e2db
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547038"
---
# <a name="how-to-programmatically-search-for-and-replace-text-in-documents"></a>如何：以编程方式在文档中搜索和替换文本
  <xref:Microsoft.Office.Interop.Word.Find> 对象是 <xref:Microsoft.Office.Interop.Word.Selection> 和 <xref:Microsoft.Office.Interop.Word.Range> 对象的成员，可使用其中任何一个来搜索 Microsoft Office Word 文档中的文本。 替换命令是查找命令的扩展。

 使用 <xref:Microsoft.Office.Interop.Word.Find> 对象循环访问 Microsoft Office Word 文档并搜索特定文本、格式或样式，使用 <xref:Microsoft.Office.Interop.Word.Find.Replacement%2A> 属性替换任何找到的项。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="use-a-selection-object"></a>使用 Selection 对象
 使用 <xref:Microsoft.Office.Interop.Word.Selection> 对象查找文本时，指定的任何搜索条件均只能应用于当前选定的文本。 如果 <xref:Microsoft.Office.Interop.Word.Selection> 是插入点，则搜索文档。 找到符合搜索条件的项时，将自动将其选中。

 请务必注意，<xref:Microsoft.Office.Interop.Word.Find> 条件是累积性的，这意味着会将条件添加到之前的搜索条件。 搜索前使用 <xref:Microsoft.Office.Interop.Word.Find.ClearFormatting%2A> 方法清除之前的搜索的格式。

### <a name="to-find-text-using-a-selection-object"></a>使用 Selection 对象查找文本

1. 将搜索字符串分配给变量。

    [!code-vb[Trin_VstcoreWordAutomation#68](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#68)]
    [!code-csharp[Trin_VstcoreWordAutomation#68](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#68)]

2. 清除之前的搜索的格式。

    [!code-vb[Trin_VstcoreWordAutomation#69](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#69)]
    [!code-csharp[Trin_VstcoreWordAutomation#69](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#69)]

3. 执行搜索，并显示消息框和结果。

    [!code-vb[Trin_VstcoreWordAutomation#70](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#70)]
    [!code-csharp[Trin_VstcoreWordAutomation#70](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#70)]

   以下示例显示完整的方法。

   [!code-vb[Trin_VstcoreWordAutomation#67](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#67)]
   [!code-csharp[Trin_VstcoreWordAutomation#67](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#67)]

## <a name="use-a-range-object"></a>使用 Range 对象
 使用 <xref:Microsoft.Office.Interop.Word.Range> 对象使你能够搜索文本，而无需在用户界面中显示任何内容。 <xref:Microsoft.Office.Interop.Word.Find>如果找到与搜索条件匹配的文本，则对象返回**True** ; 否则，返回**False** 。 如果找到了文本，则它还重新定义 <xref:Microsoft.Office.Interop.Word.Range> 对象以匹配搜索条件。

### <a name="to-find-text-using-a-range-object"></a>使用 Range 对象查找文本

1. 定义 <xref:Microsoft.Office.Interop.Word.Range> 对象，该对象包含文档中的第二个段落。

    下面的代码示例可用于文档级自定义项。

    [!code-vb[Trin_VstcoreWordAutomation#72](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#72)]
    [!code-csharp[Trin_VstcoreWordAutomation#72](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#72)]

    以下代码示例可用于 VSTO 外接程序。 本示例使用活动文档。

    [!code-vb[Trin_VstcoreWordAutomationAddIn#72](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#72)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#72](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#72)]

2. 使用 <xref:Microsoft.Office.Interop.Word.Range.Find%2A> 对象的属性 <xref:Microsoft.Office.Interop.Word.Range> ，首先清除任何现有的格式设置选项，然后搜索字符串 "**查找我**"。

    [!code-vb[Trin_VstcoreWordAutomation#73](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#73)]
    [!code-csharp[Trin_VstcoreWordAutomation#73](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#73)]

3. 在消息框中显示搜索结果，然后选择 <xref:Microsoft.Office.Interop.Word.Range> 以使其可见。

    [!code-vb[Trin_VstcoreWordAutomation#74](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#74)]
    [!code-csharp[Trin_VstcoreWordAutomation#74](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#74)]

    如果搜索失败，则选中第二段；如果成功，则显示搜索条件。

   下面的示例显示文档级自定项的完整代码。 若要使用此示例，请从项目的 `ThisDocument` 类中运行代码。

   [!code-vb[Trin_VstcoreWordAutomation#71](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#71)]
   [!code-csharp[Trin_VstcoreWordAutomation#71](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#71)]

   下面的示例显示 VSTO 外接程序的完整代码。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

   [!code-vb[Trin_VstcoreWordAutomationAddIn#71](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#71)]
   [!code-csharp[Trin_VstcoreWordAutomationAddIn#71](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#71)]

## <a name="search-for-and-replace-text-in-documents"></a>搜索和替换文档中的文本
 下面的代码搜索当前所选内容，并将找到**的字符串的**所有匹配项替换为**找到**的字符串。

### <a name="to-search-for-and-replace-text-in-documents"></a>在文档中搜索并替换文本

1. 将以下示例代码添加到项目的 `ThisDocument` 或 `ThisAddIn` 类中。

     [!code-vb[Trin_VstcoreWordAutomation#75](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#75)]
     [!code-csharp[Trin_VstcoreWordAutomation#75](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#75)]

     <xref:Microsoft.Office.Interop.Word.Find> 类具有 <xref:Microsoft.Office.Interop.Word.Find.ClearFormatting%2A> 方法，而 <xref:Microsoft.Office.Interop.Word.Replacement> 类也具有自己的 <xref:Microsoft.Office.Interop.Word.Replacement.ClearFormatting%2A> 方法。 执行查找和替换操作时，必须同时使用这两个对象的 ClearFormatting 方法。 如果仅在 <xref:Microsoft.Office.Interop.Word.Find> 对象上使用该方法，则可能会在替换文本中得到意外的结果。

2. 使用 <xref:Microsoft.Office.Interop.Word.Find> 对象的 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 方法来替换每个找到的项。 若要指定要替换的项，请使用*replace*参数。 此参数可能是以下 <xref:Microsoft.Office.Interop.Word.WdReplace> 值之一：

    - <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceAll> 将替换所有找到的项。

    - <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceNone> 不会替换任何找到的项。

    - <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceOne> 将替换找到的第一个项。

## <a name="see-also"></a>另请参阅
- [如何：以编程方式在 Word 中设置搜索选项](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [如何：以编程方式遍历在文档中找到的项](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [如何：以编程方式在文档中定义和选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式在搜索后还原选定内容](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
