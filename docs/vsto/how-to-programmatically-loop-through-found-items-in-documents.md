---
title: 如何：以编程方式遍历在文档中找到的项
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- loops, through found items in documents
- documents [Office development in Visual Studio], searching
- text [Office development in Visual Studio], searching in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 22f8035cc7c1b09e7fd54f3c10842237ee6273b9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812405"
---
# <a name="how-to-programmatically-loop-through-found-items-in-documents"></a>如何：以编程方式遍历在文档中找到的项
  <xref:Microsoft.Office.Interop.Word.Find>类具有<xref:Microsoft.Office.Interop.Word.Find.Found%2A>属性，它返回**true**每当找到搜索的项。 你可以使用 <xref:Microsoft.Office.Interop.Word.Range> 方法循环访问在 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 中找到的所有实例。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-loop-through-found-items"></a>循环访问找到的项

1. 声明 <xref:Microsoft.Office.Interop.Word.Range> 对象。

    下面的代码示例可用于文档级自定义项。

    [!code-vb[Trin_VstcoreWordAutomation#79](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#79)]
    [!code-csharp[Trin_VstcoreWordAutomation#79](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#79)]

    以下代码示例可用于 VSTO 外接程序。 本示例使用活动文档。

    [!code-vb[Trin_VstcoreWordAutomationAddIn#79](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#79)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#79](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#79)]

2. 循环使用 <xref:Microsoft.Office.Interop.Word.Find.Found%2A> 属性来搜索文档中字符串的所有匹配项，每次找到该字符串时整数变量递增 1。

    [!code-vb[Trin_VstcoreWordAutomation#80](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#80)]
    [!code-csharp[Trin_VstcoreWordAutomation#80](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#80)]

3. 在消息框中显示找到字符串的次数。

    [!code-vb[Trin_VstcoreWordAutomation#81](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#81)]
    [!code-csharp[Trin_VstcoreWordAutomation#81](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#81)]

   以下示例显示了完整方法。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="to-loop-through-items-in-a-document-level-customization"></a>循环访问文档级自定义项中的项

1. 下面的示例显示文档级自定项的完整代码。 若要使用此代码，请从项目中的 `ThisDocument` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomation#78](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#78)]
     [!code-csharp[Trin_VstcoreWordAutomation#78](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#78)]

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="to-loop-through-items-in-a-vsto-add-in"></a>循环访问 VSTO 外接程序中的项

1. 下面的示例显示 VSTO 外接程序的完整代码。 若要使用此代码，请从项目中的 `ThisAddIn` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#78](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#78)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#78](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#78)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式搜索和替换文档中的 rext](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [如何：以编程方式在 Word 中设置搜索选项](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [如何：以编程方式定义和在文档中选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式搜索后还原选定内容](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
