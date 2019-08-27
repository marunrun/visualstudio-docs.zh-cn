---
title: 如何：以编程方式在 Word 中设置搜索选项
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- settings, Word search options
- documents [Office development in Visual Studio], search options
- Word, searching options
- searching, Word options
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6e3b66bfd7f3f5d0ef0f4893efeb81c80df5d4ae
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62961870"
---
# <a name="how-to-programmatically-set-search-options-in-word"></a>如何：以编程方式在 Word 中设置搜索选项
  有两种方法可以在 Microsoft Office Word 文档中设置的选择的搜索选项：

- 设置各个属性的<xref:Microsoft.Office.Interop.Word.Find>对象。

- 使用的自变量<xref:Microsoft.Office.Interop.Word.Find.Execute%2A>方法的<xref:Microsoft.Office.Interop.Word.Find>对象。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="use-properties-of-a-find-object"></a>使用查找对象的属性
 下面的代码设置的属性<xref:Microsoft.Office.Interop.Word.Find>对象以在当前所选内容中搜索文本。 请注意搜索条件，如搜索进、 自动换行，和文本要搜索的属性<xref:Microsoft.Office.Interop.Word.Find>对象。

 设置的属性的每个<xref:Microsoft.Office.Interop.Word.Find>因为您必须指定相同的属性中的参数编写 C# 代码时，对象不是很有用<xref:Microsoft.Office.Interop.Word.Find.Execute%2A>方法。 因此，本示例包含仅 Visual Basic 代码。

### <a name="to-set-search-options-using-a-find-object"></a>若要设置使用 Find 对象的搜索选项

1. 设置的属性<xref:Microsoft.Office.Interop.Word.Find>对象的文本在选定内容向前搜索**找到我**。

     [!code-vb[Trin_VstcoreWordAutomation#76](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#76)]

## <a name="use-execute-method-arguments"></a>使用 Execute 方法自变量
 下面的代码使用<xref:Microsoft.Office.Interop.Word.Find.Execute%2A>方法的<xref:Microsoft.Office.Interop.Word.Find>对象以在当前所选内容中搜索文本。 请注意，作为参数传递的搜索条件，如搜索进、 自动换行和文本搜索，<xref:Microsoft.Office.Interop.Word.Find.Execute%2A>方法。

### <a name="to-set-search-options-using-execute-method-arguments"></a>若要设置搜索选项使用 Execute 方法自变量

1. 将搜索条件作为参数传递<xref:Microsoft.Office.Interop.Word.Find.Execute%2A>方法以在选定的文本内容向前搜索**找到我**。

     [!code-vb[Trin_VstcoreWordAutomation#77](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#77)]
     [!code-csharp[Trin_VstcoreWordAutomation#77](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#77)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式搜索和替换文档中的文本](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [如何：以编程方式遍历在文档中找到的项](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [如何：以编程方式搜索后还原选定内容](../vsto/how-to-programmatically-restore-selections-after-searches.md)
