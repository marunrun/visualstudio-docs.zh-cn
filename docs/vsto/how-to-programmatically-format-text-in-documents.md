---
title: 如何：以编程方式设置文本格式在文档中
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formatting [Office development in Visual Studio]
- documents [Office development in Visual Studio], formatting text
- text [Office development in Visual Studio], formatting in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b9f0f64f47317b5712c34d8aca4ea6f64191438e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62971129"
---
# <a name="how-to-programmatically-format-text-in-documents"></a>如何：以编程方式设置文本格式在文档中
  你可以使用 <xref:Microsoft.Office.Interop.Word.Range> 对象来格式化 Microsoft Office Word 文档中的文本。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 下面的示例选择文档中的第一个段落并更改字号、字体名称和对齐方式。 然后，它会选择范围并显示一个消息框，以在执行下一段代码前暂停。 下一节调用的 Undo 方法<xref:Microsoft.Office.Tools.Word.Document>主机项 （对于文档级自定义项） 或<xref:Microsoft.Office.Interop.Word.Document>类 （对于 VSTO 外接程序） 三次。 它应用“正文缩进”样式，并显示一个消息框以暂停代码。 然后，该代码调用 <xref:Microsoft.Office.Tools.Word.Document.Undo%2A> 方法一次，并显示一个消息框。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="to-format-text-using-a-document-level-customization"></a>使用文档级自定义项格式化文本

1. 可以在文档级自定义项中使用下面的示例。 若要使用此代码，请从项目中的 `ThisDocument` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomation#62](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#62)]
     [!code-csharp[Trin_VstcoreWordAutomation#62](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#62)]

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="to-format-text-using-a-vsto-add-in"></a>使用 VSTO 外接程序格式化文本

1. 可以在 VSTO 外接程序中使用下面的示例。 本示例使用活动文档。 若要使用此代码，请从项目中的 `ThisAddIn` 类运行它。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#62](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#62)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#62](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#62)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式定义和在文档中选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式向 Word 文档中插入文本](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [如何：以编程方式搜索和替换文档中的文本](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
