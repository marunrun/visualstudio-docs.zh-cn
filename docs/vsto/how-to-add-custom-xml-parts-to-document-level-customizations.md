---
title: 如何：向文档级自定义项添加自定义 XML 部件
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document-level customizations [Office development in Visual Studio], custom XML parts
- Office documents [Office development in Visual Studio, custom XML parts
- Word [Office development in Visual Studio], custom XML parts
- Excel [Office development in Visual Studio], custom XML parts
- custom XML parts [Office development in Visual Studio], adding
- documents [Office development in Visual Studio], custom XML parts
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 92148a6f084a4cc04b4587781e750e4fd0df133f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85538328"
---
# <a name="how-to-add-custom-xml-parts-to-document-level-customizations"></a>如何：向文档级自定义项添加自定义 XML 部件
  你可以通过在文档级自定义中创建自定义 XML 部件将 XML 数据存储在 Microsoft Office Excel 工作表或 Microsoft Office Word 文档中。 有关详细信息，请参阅 [自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

> [!NOTE]
> Visual Studio 不提供 Microsoft Office PowerPoint 的文档级项目。 有关使用 VSTO 外接程序向 PowerPoint 演示文稿添加自定义 XML 部件的信息，请参阅 [如何：使用 Vsto 外接程序向文档添加自定义 xml 部件](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)。

### <a name="to-add-a-custom-xml-part-to-an-excel-workbook"></a>向 Excel 工作簿添加自定义 XML 部件

1. 向工作簿中的 <xref:Microsoft.Office.Core.CustomXMLPart> 集合添加新 <xref:Microsoft.Office.Core.CustomXMLParts> 对象。 <xref:Microsoft.Office.Core.CustomXMLPart> 包含你希望存储在工作簿中的 XML 字符串。

     [!code-csharp[Trin_AddCustomXmlPartExcelDocLevel#1](../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartExcelDocLevel/ThisWorkbook.cs#1)]
     [!code-vb[Trin_AddCustomXmlPartExcelDocLevel#1](../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartExcelDocLevel/ThisWorkbook.vb#1)]

2. 将 `AddCustomXmlPartToWorkbook` 方法添加到 Excel 文档级项目中的 `ThisWorkbook` 类。

3. 从项目中的其他代码调用该方法。 例如，若要在用户打开工作簿时创建自定义 XML 部件，则从 `ThisWorkbook_Startup` 事件处理程序调用该方法。

### <a name="to-add-a-custom-xml-part-to-a-word-document"></a>向 Word 文档添加自定义 XML 部件

1. 向文档中的 <xref:Microsoft.Office.Core.CustomXMLPart> 集合添加新的 <xref:Microsoft.Office.Core.CustomXMLParts> 对象。 <xref:Microsoft.Office.Core.CustomXMLPart> 包含你希望存储在文档中的 XML 字符串。

     [!code-vb[Trin_AddCustomXmlPartWordDocLevel#1](../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartWordDocLevel/ThisDocument.vb#1)]
     [!code-csharp[Trin_AddCustomXmlPartWordDocLevel#1](../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartWordDocLevel/ThisDocument.cs#1)]

2. 将 `AddCustomXmlPartToDocument` 方法添加到 Word 文档级项目中的 `ThisDocument` 类。

3. 从项目中的其他代码调用该方法。 例如，若要在用户打开文档时创建自定义 XML 部件，则从 `ThisDocument_Startup` 事件处理程序调用该方法。

## <a name="robust-programming"></a>可靠编程
 为简单起见，此示例使用在方法中定义为局部变量的 XML 字符串。 通常，应从外部源（如文件或数据库）获取 XML。

## <a name="see-also"></a>另请参阅
- [自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)
- [如何：使用 VSTO 外接程序将自定义 XML 部件添加到文档](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)
