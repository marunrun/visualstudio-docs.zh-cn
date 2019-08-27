---
title: 工作表主机项
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- host items [Office development in Visual Studio], Worksheet
- Excel [Office development in Visual Studio], worksheets
- Worksheet host items
- worksheets, events
- Worksheet host items, events
- Excel worksheets
- worksheets, Excel
- worksheets
- events [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e4a5287648d515d1aca340ab55d5f21b494610b5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62814726"
---
# <a name="worksheet-host-item"></a>工作表主机项
  <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项这种类型从 Excel 的主互操作程序集扩展 <xref:Microsoft.Office.Interop.Excel.Worksheet> 类型。 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项提供与 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象完全相同的属性、方法和事件，但它还公开其他事件并充当宿主控件和 Windows 窗体控件的容器。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 在文档级项目中，可以在设计时将 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项添加到项目。 在 VSTO 外接程序项目中，您可以生成<xref:Microsoft.Office.Tools.Excel.Worksheet>主机在运行时的项。

## <a name="understand-worksheet-host-items-in-document-level-projects"></a>了解文档级项目中的工作表宿主项
 为 Excel 创建文档级项目时，Visual Studio 会自动在项目中创建三个 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项。 这些工作表的默认名称分别为 `Sheet1`、 `Sheet2`和 `Sheet3`。 如果基于现有工作簿创建项目，则宿主项的数目取决于工作簿中工作表的数目。

 利用这些工作表类，你可以访问 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项的成员，以在自定义项中执行基本任务，例如修改工作表的内容。 也可以使用这些类将控件添加到工作表。 通过组合不同的控件集并编写代码，可将控件绑定到数据、从用户处收集信息并响应用户操作。 有关详细信息，请参阅[程序文档级自定义项](../vsto/programming-document-level-customizations.md)。

 工作表类提供了一个位置，你可以在该位置开始编写项目中的代码。 因为该类提供与 Excel 主互操作程序集中的 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象完全相同的属性、方法和事件，所以也可以使用这些类访问 Excel 的对象模型。 有关详细信息，请参阅[Excel 对象模型概述](../vsto/excel-object-model-overview.md)。

 在文档级项目中，通过将新工作表添加到设计器中的工作簿，可以在设计时将其他 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项添加到项目。

### <a name="rename-worksheets"></a>重命名工作表
 在文档级项目中，可在 Visual Studio 设计器中对工作表进行重命名，但此操作只会更改工作表的显示名称。 编程名称仍是工作表的默认名称。 如果在“属性”  窗口中对工作表进行重命名，则只会更改编程名称。

### <a name="limitations-of-the-worksheet-host-item-in-document-level-projects"></a>文档级项目中的工作表主机项的限制
 你不能创建新<xref:Microsoft.Office.Tools.Excel.Worksheet>主机在运行时在文档级项目中的项。 如果在运行时创建新的 Excel 工作表，它将是类型<xref:Microsoft.Office.Interop.Excel.Worksheet>。 因为它不是宿主项，所以它不能包含任何宿主控件或 Windows 窗体控件。 有关在运行时创建的文档的详细信息，请参阅[如何：以编程方式将新工作表添加到工作簿](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)。

## <a name="understand-worksheet-host-items-in-vsto-add-in-projects"></a>了解 VSTO 外接程序项目中的工作表宿主项
 在应用程序级项目中，可以在运行时为 Excel 中打开的任何工作表生成 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项。 可以使用 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项将控件添加到关联的工作表，或处理在 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象中不可用的事件。

 若要生成 <xref:Microsoft.Office.Tools.Excel.Worksheet> 宿主项，请使用 `GetVstoObject` 方法。 有关详细信息，请参阅[扩展 Word 文档和 Excel 工作簿中运行时在 VSTO 加载项](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

## <a name="see-also"></a>请参阅
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [扩展 Word 文档和 Excel 工作簿在 VSTO 外接在运行时](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [工作簿主机项](../vsto/workbook-host-item.md)
- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
