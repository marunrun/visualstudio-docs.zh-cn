---
title: 如何：以编程方式打印 Visio 文档
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], printing Visio documents
- documents [Office development in Visual Studio], printing Visio documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0e31a55e49d42311b5ec5fff82769584cc55ce09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85537795"
---
# <a name="how-to-programmatically-print-visio-documents"></a>如何：以编程方式打印 Visio 文档
  你可以打印完整的 Microsoft Office Visio 文档或仅打印某一特定页。

 有关打印方法的详细信息，请参阅 [Microsoft.Office.Interop.Visio.Document.Print](/office/vba/api/Visio.Document.Print) 方法和 [Microsoft.Office.Interop.Visio.Page.Print](/office/vba/api/Visio.Page.Print) 方法的 VBA 参考文档。

## <a name="print-a-visio-document"></a>打印 Visio 文档

### <a name="to-print-a-complete-document"></a>打印完整的文档

- 调用要打印的 `Microsoft.Office.Interop.Visio.Document.Print` 对象的 `Microsoft.Office.Interop.Visio.Document` 方法。

     下面的代码示例将打印活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#8](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#8)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#8](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#8)]

## <a name="print-a-page-of-a-visio-document"></a>打印 Visio 文档的某一页

### <a name="to-print-a-page-of-a-document"></a>打印文档的某一页

- 调用要打印的 `Microsoft.Office.Interop.Visio.Pages.Print` 对象的 `Microsoft.Office.Interop.Visio.Pages` 方法。

     下面的代码示例打印活动文档的第一页。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#9](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#9)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#9](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#9)]

## <a name="see-also"></a>另请参阅
- [Visio 解决方案](../vsto/visio-solutions.md)
- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)
- [如何：以编程方式创建新的 Visio 文档](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [如何：以编程方式打开 Visio 文档](../vsto/how-to-programmatically-open-visio-documents.md)
- [如何：以编程方式关闭 Visio 文档](../vsto/how-to-programmatically-close-visio-documents.md)
- [如何：以编程方式保存 Visio 文档](../vsto/how-to-programmatically-save-visio-documents.md)
