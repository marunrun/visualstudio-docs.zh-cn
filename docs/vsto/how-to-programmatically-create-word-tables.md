---
title: 如何：以编程方式创建 Word 表
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], adding tables
- tables [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 24a365ba239e4d87e179bfecd664aa31aef0f359
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62574906"
---
# <a name="how-to-programmatically-create-word-tables"></a>如何：以编程方式创建 Word 表
  <xref:Microsoft.Office.Interop.Word.Tables> 集合是 <xref:Microsoft.Office.Interop.Word.Document>、<xref:Microsoft.Office.Tools.Word.Document>、<xref:Microsoft.Office.Interop.Word.Selection> 和 <xref:Microsoft.Office.Interop.Word.Range> 类的成员，这意味着可以在上述任一上下文中创建表格。 使用 <xref:Microsoft.Office.Interop.Word.Tables> 集合的 <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> 方法在指定范围内添加表格。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="create-tables-in-document-level-customizations"></a>在文档级自定义项中创建表

### <a name="to-add-a-table-to-a-document"></a>若要将表添加到文档

- 使用 <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> 方法在文档开头添加一个三行四列的表格。

   若要使用下面的代码示例，请从项目的 `ThisDocument` 类中运行它。

   [!code-vb[Trin_VstcoreWordAutomation#86](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#86)]
   [!code-csharp[Trin_VstcoreWordAutomation#86](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#86)]

  在创建表格时，表格会自动添加到 <xref:Microsoft.Office.Tools.Word.Document> 主机项的 <xref:Microsoft.Office.Interop.Word.Tables> 集合中。 然后，可以使用 <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> 属性按照项编号引用该表格，如以下代码所示。

### <a name="to-refer-to-a-table-by-item-number"></a>按照项编号引用表格

1. 使用 <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> 属性并提供要引用的表格的项编号。

    若要使用下面的代码示例，请从项目的 `ThisDocument` 类中运行它。

    [!code-vb[Trin_VstcoreWordAutomation#87](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#87)]
    [!code-csharp[Trin_VstcoreWordAutomation#87](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#87)]

   每个 <xref:Microsoft.Office.Interop.Word.Table> 对象还具有一个 <xref:Microsoft.Office.Interop.Word.Table.Range%2A> 属性，该属性可用于设置格式属性。

### <a name="to-apply-a-style-to-a-table"></a>将样式应用到表格

1. 使用 <xref:Microsoft.Office.Interop.Word.Table.Style%2A> 属性将其中一个 Word 内置样式应用到表格。

     若要使用下面的代码示例，请从项目的 `ThisDocument` 类中运行它。

     [!code-vb[Trin_VstcoreWordAutomation#88](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#88)]
     [!code-csharp[Trin_VstcoreWordAutomation#88](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#88)]

## <a name="create-tables-in-vsto-add-ins"></a>在 VSTO 外接程序中创建表

### <a name="to-add-a-table-to-a-document"></a>若要将表添加到文档

- 使用 <xref:Microsoft.Office.Interop.Word.Tables.Add%2A> 方法在文档开头添加一个三行四列的表格。

   下面的代码示例是向活动文档添加一个表格。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行它。

   [!code-vb[Trin_VstcoreWordAutomationAddIn#86](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#86)]
   [!code-csharp[Trin_VstcoreWordAutomationAddIn#86](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#86)]

  在创建表格时，表格会自动添加到 <xref:Microsoft.Office.Interop.Word.Document> 的 <xref:Microsoft.Office.Interop.Word.Tables> 集合中。 然后，可以使用 <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> 属性按照项编号引用该表格，如以下代码所示。

### <a name="to-refer-to-a-table-by-item-number"></a>按照项编号引用表格

1. 使用 <xref:Microsoft.Office.Interop.Word.Tables.Item%2A> 属性并提供要引用的表格的项编号。

    下面的代码示例使用活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行它。

    [!code-vb[Trin_VstcoreWordAutomationAddIn#87](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#87)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#87](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#87)]

   每个 <xref:Microsoft.Office.Interop.Word.Table> 对象还具有一个 <xref:Microsoft.Office.Interop.Word.Table.Range%2A> 属性，该属性可用于设置格式属性。

### <a name="to-apply-a-style-to-a-table"></a>将样式应用到表格

1. 使用 <xref:Microsoft.Office.Interop.Word.Table.Style%2A> 属性将其中一个 Word 内置样式应用到表格。

     下面的代码示例使用活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行它。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#88](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#88)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#88](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#88)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式添加的文本和格式向 Word 表中的单元格](../vsto/how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)
- [如何：以编程方式向 Word 表中添加行和列](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)
- [如何：以编程方式填充 Word 表使用文档属性](../vsto/how-to-programmatically-populate-word-tables-with-document-properties.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
