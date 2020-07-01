---
title: 如何：以编程方式在搜索后还原选定内容
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- searches, restoring selection after
- documents [Office development in Visual Studio], restoring selections
- selections, restoring after a search
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 30daa81c33070db3f9418b45b84b4acc6e243dc9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547090"
---
# <a name="how-to-programmatically-restore-selections-after-searches"></a>如何：以编程方式在搜索后还原选定内容
  如果查找并替换文档中的文本，则可能需要在搜索完成后还原用户的原始选择。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 示例过程中的代码使用了两个 <xref:Microsoft.Office.Interop.Word.Range> 对象。 一个存储当前的 <xref:Microsoft.Office.Interop.Word.Selection> ，另一个设置要用作搜索范围的整个文档。

## <a name="to-restore-the-users-original-selection-after-a-search"></a>在搜索后还原用户的原始选择

1. <xref:Microsoft.Office.Interop.Word.Range>为文档和当前选择创建对象。

    [!code-vb[Trin_VstcoreWordAutomation#83](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#83)]
    [!code-csharp[Trin_VstcoreWordAutomation#83](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#83)]

2. 执行搜索和替换操作。

    [!code-vb[Trin_VstcoreWordAutomation#84](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#84)]
    [!code-csharp[Trin_VstcoreWordAutomation#84](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#84)]

3. 选择要还原用户的原始选择范围的起始范围。

    [!code-vb[Trin_VstcoreWordAutomation#85](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#85)]
    [!code-csharp[Trin_VstcoreWordAutomation#85](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#85)]

   以下示例显示完整的方法。

## <a name="example"></a>示例
 [!code-vb[Trin_VstcoreWordAutomation#82](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#82)]
 [!code-csharp[Trin_VstcoreWordAutomation#82](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#82)]

## <a name="see-also"></a>另请参阅
- [如何：以编程方式在文档中搜索和替换文本](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [如何：以编程方式在 Word 中设置搜索选项](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [如何：以编程方式遍历在文档中找到的项](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
