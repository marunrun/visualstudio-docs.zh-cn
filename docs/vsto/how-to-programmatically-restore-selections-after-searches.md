---
title: 如何：以编程方式搜索后还原选定内容
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 672c66fef5d7400601ce69270b5cd4f525b34c7d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955690"
---
# <a name="how-to-programmatically-restore-selections-after-searches"></a>如何：以编程方式搜索后还原选定内容
  如果您查找和替换文档中的文本，可能想要完成搜索后还原用户的原选定内容。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 示例过程中的代码使用两个<xref:Microsoft.Office.Interop.Word.Range>对象。 其中一个存储当前<xref:Microsoft.Office.Interop.Word.Selection>，且其中一人整篇文档，使用作为搜索范围。

## <a name="to-restore-the-users-original-selection-after-a-search"></a>若要还原后搜索的用户的原选定内容

1. 创建<xref:Microsoft.Office.Interop.Word.Range>文档和当前选择的对象。

    [!code-vb[Trin_VstcoreWordAutomation#83](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#83)]
    [!code-csharp[Trin_VstcoreWordAutomation#83](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#83)]

2. 执行搜索和替换操作。

    [!code-vb[Trin_VstcoreWordAutomation#84](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#84)]
    [!code-csharp[Trin_VstcoreWordAutomation#84](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#84)]

3. 选择要还原用户的原选定内容的开始范围。

    [!code-vb[Trin_VstcoreWordAutomation#85](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#85)]
    [!code-csharp[Trin_VstcoreWordAutomation#85](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#85)]

   以下示例显示完整的方法。

## <a name="example"></a>示例
 [!code-vb[Trin_VstcoreWordAutomation#82](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#82)]
 [!code-csharp[Trin_VstcoreWordAutomation#82](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#82)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式搜索和替换文档中的文本](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [如何：以编程方式在 Word 中设置搜索选项](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [如何：以编程方式遍历在文档中找到的项](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
