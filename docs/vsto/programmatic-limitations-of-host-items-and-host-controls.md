---
title: 宿主项和宿主控件的编程限制
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, host controls
- application development [Office development in Visual Studio], host items
- Office applications [Office development in Visual Studio], host items
- host items [Office development in Visual Studio], programmatic limitations
- Excel [Office development in Visual Studio], host items
- host controls [Office development in Visual Studio], creating
- document-level customizations [Office development in Visual Studio], host controls
- Office applications [Office development in Visual Studio], host controls
- documents [Office development in Visual Studio], host controls
- controls [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], passing to methods and properties
- application development [Office development in Visual Studio], host controls
- Excel [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], programmatic limitations
- documents [Office development in Visual Studio], host items
- Office documents [Office development in Visual Studio, host items
- Word [Office development in Visual Studio], host items
- document-level customizations [Office development in Visual Studio], host items
- Word [Office development in Visual Studio], host controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 97b94291a3fd057e82bd79aa4f6c3220020bc24a
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255805"
---
# <a name="programmatic-limitations-of-host-items-and-host-controls"></a>宿主项和宿主控件的编程限制
  每个宿主项和宿主控件的行为都类似于相应的本机 Microsoft Office Word 或 Microsoft Office Excel 对象，并且具有附加功能。 但是，在运行时宿主项和宿主控件的行为与本机 Office 对象之间存在一些本质区别。

 有关宿主项和宿主控件的常规信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="programmatically-create-host-items"></a>以编程方式创建宿主项
 使用 Word 或 Excel 对象模型在运行时以编程方式创建或打开文档、工作簿或工作表时，该项不是宿主项。 相反，新的对象是本机 Office 对象。 例如，如果使用 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> 方法在运行时创建新的 Word 文档，它将是一个本机 <xref:Microsoft.Office.Interop.Word.Document> 对象而不是 <xref:Microsoft.Office.Tools.Word.Document> 宿主项。 同样，当你使用 <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> 方法在运行时创建新工作表时，会得到本机 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象而不是 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项。

 在文档级项目中，不能在运行时创建宿主项。 在文档级项目中，只能在设计时创建宿主项。 有关详细信息，请参阅[文档宿主项](../vsto/document-host-item.md)、[工作簿主机项](../vsto/workbook-host-item.md)和[工作表主机项](../vsto/worksheet-host-item.md)。

 在 VSTO 外接程序项目中，可以在运行时创建 <xref:Microsoft.Office.Tools.Word.Document>、 <xref:Microsoft.Office.Tools.Excel.Workbook>或 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项。 有关详细信息，请参阅[在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

## <a name="programmatically-create-host-controls"></a>以编程方式创建宿主控件
 可以在运行时以编程方式向 <xref:Microsoft.Office.Tools.Word.Document> 或 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项添加宿主控件。 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

 不能向本机 <xref:Microsoft.Office.Interop.Word.Document> 或 <xref:Microsoft.Office.Interop.Excel.Worksheet>添加宿主控件。

> [!NOTE]
> 不能以编程方式向工作表或文档添加以下宿主控件： <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>、 <xref:Microsoft.Office.Tools.Word.XMLNode>和 <xref:Microsoft.Office.Tools.Word.XMLNodes>。

## <a name="understand-type-differences-between-host-items-host-controls-and-native-office-objects"></a>了解宿主项、宿主控件和本机 Office 对象之间的类型差异
 对于每个宿主项和宿主控件，都有基础本机 Microsoft Office Word 或 Microsoft Office Excel 对象。 您可以通过使用主机项或主机控件的 InnerObject 属性来访问基础对象。 但是，没有办法将本机 Office 对象强制转换为其对应的宿主项或宿主控件。 如果尝试将本机 Office 对象强制转换为宿主项或宿主控件的类型，将引发 <xref:System.InvalidCastException> 。

 有几种应用场景，宿主项和宿主控件的类型与基础本机 Office 对象之间的差异可能会影响你的代码。

### <a name="pass-host-controls-to-methods-and-properties"></a>将宿主控件传递给方法和属性
 在 Word 中，不能将宿主控件传递给需要将本机 Word 对象作为参数的方法或属性。 必须使用主机控件的 InnerObject 属性来返回基础本机 Word 对象。 例如，可以通过将 <xref:Microsoft.Office.Interop.Word.Bookmark> 宿主控件的 <xref:Microsoft.Office.Tools.Word.Bookmark.InnerObject%2A> 属性传递给方法，从而将 <xref:Microsoft.Office.Tools.Word.Bookmark> 对象传递给方法。

 在 Excel 中，当方法或属性需要基础 Excel 对象时，必须使用宿主控件的 InnerObject 属性将宿主控件传递给方法或属性。

 下面的示例创建一个 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件，并将其传递给 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> 方法。 该代码使用命名范围的 <xref:Microsoft.Office.Tools.Excel.NamedRange.InnerObject%2A> 属性来返回 <xref:Microsoft.Office.Interop.Excel.Range> 方法所需的基础 Office <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> 。

 [!code-csharp[Trin_VstcoreHostControlsExcel#28](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#28)]
 [!code-vb[Trin_VstcoreHostControlsExcel#28](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#28)]

### <a name="return-types-of-native-office-methods-and-properties"></a>返回本机 Office 方法和属性的类型
 宿主项的大多数方法和属性将返回宿主项所依据的基础本机 Office 对象。 例如，Excel 中 <xref:Microsoft.Office.Tools.Excel.NamedRange.Parent%2A> 宿主控件的 <xref:Microsoft.Office.Tools.Excel.NamedRange> 属性将返回 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象而不是 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项。 同样，Word 中 <xref:Microsoft.Office.Tools.Word.RichTextContentControl.Parent%2A> 宿主控件的 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 属性也将返回 <xref:Microsoft.Office.Interop.Word.Document> 对象而不是 <xref:Microsoft.Office.Tools.Word.Document> 宿主项。

### <a name="access-collections-of-host-controls"></a>访问宿主控件的集合
 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 不为每种类型的宿主控件提供单独的集合。 相反，使用主机项的 Controls 属性循环访问文档或工作表上的所有托管控件（主机控件和 Windows 窗体控件），然后查找与所需的主机控件类型匹配的项。 下面的代码示例检查 Word 文档中的每个控件，并确定控件是否为 <xref:Microsoft.Office.Tools.Word.Bookmark>。

 [!code-csharp[Trin_VstcoreHostControlsWord#10](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#10)]
 [!code-vb[Trin_VstcoreHostControlsWord#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#10)]

 有关宿主项的 Controls 属性的详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

 Word 和 Excel 对象模型包括公开文档和工作表中本机控件的集合的属性。 不能使用这些属性来访问托管控件。 例如，不能使用 <xref:Microsoft.Office.Tools.Word.Bookmark> 的 <xref:Microsoft.Office.Interop.Word._Document.Bookmarks%2A> 属性或 <xref:Microsoft.Office.Interop.Word.Document> 的 <xref:Microsoft.Office.Tools.Word.Document.Bookmarks%2A> 属性来枚举文档中的每个 <xref:Microsoft.Office.Tools.Word.Document>宿主控件。 这些属性仅包括文档中的 <xref:Microsoft.Office.Interop.Word.Bookmark> 控件；不包括文档中的 <xref:Microsoft.Office.Tools.Word.Bookmark> 宿主控件。

## <a name="see-also"></a>请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)
- [使用扩展对象实现 Excel 自动化](../vsto/automating-excel-by-using-extended-objects.md)
- [工作表宿主项](../vsto/worksheet-host-item.md)
- [工作簿宿主项](../vsto/workbook-host-item.md)
- [文档宿主项](../vsto/document-host-item.md)
