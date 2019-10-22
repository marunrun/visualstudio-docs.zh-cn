---
title: 使用扩展对象实现 Excel 自动化
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], automating
- automation [Office development in Visual Studio], Excel
- host controls, Excel
- Excel [Office development in Visual Studio], host controls
- extended objects [Office development in Visual Studio], Excel
- host controls [Office development in Visual Studio], Excel
- automating Excel
- host items [Office development in Visual Studio], Excel
- controls [Office development in Visual Studio], Excel host controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 65734f5397bae8c35fb8e312041d0600b8fa84e9
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254337"
---
# <a name="automate-excel-by-using-extended-objects"></a>使用扩展对象实现 Excel 自动化
  当开发 Visual Studio 中的 Excel 解决方案时，可以使用解决方案中的 *主机项* 和 *主机控件*。 这些对象可扩展 Excel 对象模型（即由 Excel 的主互操作程序集公开的对象模型）中某些常用对象，例如 <xref:Microsoft.Office.Interop.Excel.Worksheet> 和 <xref:Microsoft.Office.Interop.Excel.Range> 对象。 扩展的对象行为类似于其所基于的 Excel 对象，但它们可以将其他功能（如“新建事件”）和数据绑定功能添加到对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 虽然使用主机项和主机控件所在的上下文对于每种类型的解决方案有所不同，但它们均可用于 VSTO 外接程序和文档级自定义项。 有关详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

## <a name="excel-host-items"></a>Excel 主机项
 Excel 项目可授予你访问几个主机项的权限：

- <xref:Microsoft.Office.Tools.Excel.Worksheet>。 此主机项包含，表示项目中的工作表。 它还可充当托管控件（包括主机控件和 Windows 窗体控件），的容器并且还可保留有关其界面上的控件的信息。 有关详细信息，请参阅[工作表主机项](../vsto/worksheet-host-item.md)。

- <xref:Microsoft.Office.Tools.Excel.Workbook>。 此主机项表示你项目中的工作簿，可充当工作簿中所有工作表共享的组件的容器。 有关详细信息，请参阅[工作簿主机项](../vsto/workbook-host-item.md)。

- <xref:Microsoft.Office.Tools.Excel.ChartSheet>。 此主机项表示只包含一个图表并公开事件的 Excel 中的工作表。

     当在设计时将图表工作表作为 Microsoft Office Excel 文档级自定义项目中的新工作表进行添加时，Visual Studio 将自动创建 <xref:Microsoft.Office.Tools.Excel.ChartSheet> 主机项。

     尽管 <xref:Microsoft.Office.Tools.Excel.ChartSheet> 主机项是 Excel 中的一个工作表，但不能向该图表工作表添加任何控件。 如果想在包含图表的工作表上添加其他控件，请勿使用图表工作表。 相反，你可以通过使用 <xref:Microsoft.Office.Tools.Excel.Chart> 主机控件将图表作为工作表上嵌入的对象进行放置。 有关详细信息，请参阅[图表控件](../vsto/chart-control.md)。

## <a name="excel-host-controls"></a>Excel 主机控件
 有多个可用于 Excel 的主机控件，这些控件有助于你创建、组织和自动处理工作簿和工作表。 这些主机控件可提供本机 Excel 对象模型中的相应控件所无法提供的事件和数据绑定功能。

 有关可以在 Excel 项目中使用的主机控件的详细信息，请参阅以下主题：

- [图表控件](../vsto/chart-control.md)

- [ListObject 控件](../vsto/listobject-control.md)

- [NamedRange 控件](../vsto/namedrange-control.md)

- [XmlMappedRange 控件](../vsto/xmlmappedrange-control.md)

## <a name="see-also"></a>请参阅
- [如何：用数据填充 ListObject 控件](../vsto/how-to-fill-listobject-controls-with-data.md)
- [如何：向工作表添加图表控件](../vsto/how-to-add-chart-controls-to-worksheets.md)
- [如何：将 ListObject 控件添加到工作表](../vsto/how-to-add-listobject-controls-to-worksheets.md)
- [如何：将 NamedRange 控件添加到工作表](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [如何：将 XMLMappedRange 控件添加到工作表](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)
- [如何：调整 NamedRange 控件的大小](../vsto/how-to-resize-namedrange-controls.md)
- [如何：调整 ListObject 控件的大小](../vsto/how-to-resize-listobject-controls.md)
- [如何：向 ListObject 控件添加新行时验证数据](../vsto/how-to-validate-data-when-a-new-row-is-added-to-a-listobject-control.md)
- [如何：将 ListObject 列映射到数据](../vsto/how-to-map-listobject-columns-to-data.md)
- [演练：针对 NamedRange 控件的事件进行编程](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)
- [在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
