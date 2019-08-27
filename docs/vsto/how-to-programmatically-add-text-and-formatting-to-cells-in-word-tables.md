---
title: 添加文本 （&） 以编程方式向 Word 表单元格格式设置
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- cells, adding text and formatting
- text [Office development in Visual Studio], adding to Word tables
- formatting [Office development in Visual Studio]
- tables [Office development in Visual Studio], adding text and formatting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: cdab1877cf2114f7828dbd65786cf8758d77d0f3
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402015"
---
# <a name="how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables"></a>如何：以编程方式添加的文本和格式向 Word 表中的单元格
  每个表都包含一个单元格集合。 每个单独的 <xref:Microsoft.Office.Interop.Word.Cell> 对象都表示表中的一个单元格。 你可以通过表中每个单元格的位置对其进行引用。 此示例引用位于表中第一行和第一列的单元格；将文本添加到单元格；并应用格式设置。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-add-text-and-formatting-to-cells"></a>若要将文本和格式设置添加到单元格

1. 通过单元格在表中的位置对其进行引用，将文本添加到单元，并应用格式设置。

     下面的代码示例可用于文档级自定义项。 若要使用此示例，请从项目的 `ThisDocument` 类中运行它。

     [!code-vb[Trin_VstcoreWordAutomation#97](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#97)]
     [!code-csharp[Trin_VstcoreWordAutomation#97](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#97)]

     以下代码示例可用于 VSTO 外接程序。 本示例使用活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行它。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#97](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#97)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#97](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#97)]

## <a name="see-also"></a>请参阅
- [如何：以编程方式创建 Word 表](../vsto/how-to-programmatically-create-word-tables.md)
- [如何：以编程方式向 Word 表中添加行和列](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)
- [如何：以编程方式填充 Word 表使用文档属性](../vsto/how-to-programmatically-populate-word-tables-with-document-properties.md)
