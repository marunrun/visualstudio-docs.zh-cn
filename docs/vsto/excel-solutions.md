---
title: Excel 解决方案
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], application-level add-ins
- Office solutions [Office development in Visual Studio], Excel
- solutions [Office development in Visual Studio], Excel
- add-ins [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], about Excel solutions
- Excel [Office development in Visual Studio]
- documents [Office development in Visual Studio], Excel
- Office documents [Office development in Visual Studio, Excel
- projects [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], document-level customizations
- user interfaces [Office development in Visual Studio], Excel
- Office development in Visual Studio, Excel solutions
- document-level customizations [Office development in Visual Studio], Excel
- Office projects [Office development in Visual Studio], Excel
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 532689afe4e07c3151be6eac923f2b591aa34f46
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253626"
---
# <a name="excel-solutions"></a>Excel 解决方案
  Visual Studio 提供可用于创建 Microsoft Office Excel 的文档级自定义项和 VSTO 外接程序的项目模板。 你可以使用这些解决方案自动化 Excel、扩展 Excel 功能以及自定义 Excel 用户界面 (UI)。 有关文档级自定义项和 VSTO 外接程序之间的差异的详细信息，请参阅[Office 解决方案&#40;开发&#41;概述 VSTO](../vsto/office-solutions-development-overview-vsto.md)。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 本主题提供以下信息：

- [自动化 Excel](#automating)。

- [开发 Excel 的文档级自定义项](#doclevel)。

- [开发 Excel 的 VSTO 外接程序](#applevel)。

- [自定义 Excel 的用户界面](#UI)。

## <a name="automating"></a>自动化 Excel
 Excel 对象模型公开了许多能用于自动化 Excel 的模型。 例如，可以以编程方式创建图表、设置格工作表格式，以及设置范围和单元格的值。 有关详细信息，请参阅[Excel 对象模型概述](../vsto/excel-object-model-overview.md)。

 当开发 Visual Studio 中的 Excel 解决方案时，还可以使用解决方案中的 *主机项* 和 *主机控件* 。 这些是可以扩展 Excel 对象模型中常用对象的对象，例如 <xref:Microsoft.Office.Interop.Excel.Worksheet> 和 <xref:Microsoft.Office.Interop.Excel.Range> 对象。 扩展的对象行为类似于其所基于的 Excel 对象，但它们可以将其他事件和数据绑定功能添加到对象。 有关详细信息，请参阅[使用扩展对象实现 Excel 自动化](../vsto/automating-excel-by-using-extended-objects.md)。

## <a name="doclevel"></a>开发 Excel 的文档级自定义项
 Microsoft Office Excel 的文档级自定义项包含与特定工作簿相关联的程序集。 该程序集通常可通过自定义 UI 和自动化 Excel 扩展工作簿。 不同于与 Excel 自身相关联的 VSTO 外接程序，在自定义项中实现的功能仅当相关联的工作簿在 Excel 中打开时才可用。

 若要为 Excel 创建文档级自定义项目，请使用 Visual Studio 的 "**新建项目**" 对话框中的 excel 工作簿或 excel 模板项目模板。 有关详细信息，请参阅[如何：在 Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)中创建 Office 项目。

 有关文档级自定义项工作方式的详细信息，请参阅[文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)。

### <a name="excel-customization-programming-model"></a>Excel 自定义项编程模型
 当创建 Excel 的文档级项目时，Visual Studio 将生成可作为解决方案基础的几个类： `ThisWorkbook`、 `Sheet1`、 `Sheet2`和 `Sheet3`。 这些类表示与你的解决方案关联的工作簿和工作表，并为编写代码提供起点。

 有关这些生成的类和可在文档级项目中使用的其他功能的详细信息，请参阅[程序文档级自定义项](../vsto/programming-document-level-customizations.md)。

## <a name="applevel"></a>开发 Excel 的 VSTO 外接程序
 Microsoft Office Excel 的 VSTO 外接程序包含由 Excel 加载的程序集。 该程序集通常可通过自定义 UI 和自动化 Excel 扩展 Excel。 不同于与特定工作簿关联的文档级自定义项，在 VSTO 外接程序中实现的功能不局限于任何单个工作簿。

 若要创建 Excel 的 VSTO 外接程序项目，请使用 Visual Studio 的 "**新建项目**" 对话框中的 excel 工作簿或 excel 模板项目模板。 有关详细信息，请参阅[如何：在 Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)中创建 Office 项目。

 有关 VSTO 外接程序工作原理的常规信息，请参阅 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)。

### <a name="excel-add-in-programming-model"></a>Excel 外接程序编程模型
 创建 Excel VSTO 外接程序项目时，Visual Studio 将生成一个名为 `ThisAddIn`的类，这是你的解决方案的基础。 此类提供了编写代码的起点，并且还将 Excel 的对象模型公开到 VSTO 外接程序。

 有关可以在 VSTO 外`ThisAddIn`接程序中使用的类和其他 Visual Studio 功能的详细信息，请参阅[Program vsto 外接程序](../vsto/programming-vsto-add-ins.md)。

## <a name="UI"></a>自定义 Excel 的用户界面
 有几种自定义 Excel 的用户界面的方法。 某些选项适用于所有项目类型，而其他选项仅适用于 VSTO 外接程序或文档级自定义项。

### <a name="options-for-all-project-types"></a>适用于所有项目类型的选项
 下表列出了可用于文档级自定义项和 VSTO 外接程序的自定义选项。

|任务|更多相关信息|
|----------|--------------------------|
|自定义功能区。|[功能区概述](../vsto/ribbon-overview.md)|
|将 Windows 窗体控件或扩展的 Excel 控件添加到文档级自定义项的自定义工作簿中的工作表，或添加到 VSTO 外接程序的任何打开的工作簿中。|[如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)<br /><br /> [如何：向工作表添加图表控件](../vsto/how-to-add-chart-controls-to-worksheets.md)<br /><br /> [如何：将 ListObject 控件添加到工作表](../vsto/how-to-add-listobject-controls-to-worksheets.md)<br /><br /> [如何：将 NamedRange 控件添加到工作表](../vsto/how-to-add-namedrange-controls-to-worksheets.md)|

### <a name="options-for-document-level-customizations"></a>文档级自定义项的选项
 下表列出了仅适用于文档级自定义项的自定义选项。

|任务|更多相关信息|
|----------|--------------------------|
|将操作窗格添加到工作簿。|[操作窗格概述](../vsto/actions-pane-overview.md)<br /><br /> [如何：向 Word 文档或 Excel 工作簿添加操作窗格](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)|
|将映射到 XML 节点的扩展范围控件添加到工作表。|[如何：将 XMLMappedRange 控件添加到工作表](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)|

### <a name="options-for-vsto-add-ins"></a>适用于 VSTO 外接程序的选项
 下表列出了仅适用于 VSTO 外接程序的自定义选项。

|任务|更多相关信息|
|----------|--------------------------|
|创建自定义任务窗格。|[自定义任务窗格](../vsto/custom-task-panes.md)|

### <a name="related-topics"></a>相关主题

| 标题 | 描述 |
| - | - |
| [Excel 对象模型概述](../vsto/excel-object-model-overview.md) | 概述由 Excel 对象模型提供的主类型。 |
| [使用扩展对象实现 Excel 自动化](../vsto/automating-excel-by-using-extended-objects.md) | 提供有关扩展对象（由 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]提供）的信息，这些信息可用于 Excel 解决方案。 |
| [Excel 解决方案的全球化和本地化](../vsto/globalization-and-localization-of-excel-solutions.md) | 包含有关 Excel 解决方案的特殊注意事项的信息，Excel 解决方案将在具有适用于 Windows 的非英语设置的计算机上运行。 |
| [Office 文档上的 Windows 窗体控件概述](../vsto/windows-forms-controls-on-office-documents-overview.md) | 介绍如何将 Windows 窗体控件添加到 Excel 工作表。 |
| [演练：创建您的第一个 Excel 文档级自定义项](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md) | 演示如何创建 Excel 的基本文档级自定义项。 |
| [演练：创建你的第一个 Excel VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md) | 演示如何为 Excel 创建基本 VSTO 外接程序。 |
| [演练：在运行时在 VSTO 外接程序项目中向工作表添加控件](../vsto/walkthrough-adding-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project.md) | 演示如何使用 VSTO 外接程序在运行时向工作表添加 Windows 窗体按钮、 <xref:Microsoft.Office.Tools.Excel.NamedRange>和 <xref:Microsoft.Office.Tools.Excel.ListObject> 。 |
| [了解共同创作和外接程序](./understanding-coauthoring-and-addins.md) | 描述可能需要对解决方案进行的调整以适应共同创作。 |
| [Office 开发中的 Excel 2010](http://go.microsoft.com/fwlink/?LinkId=199011) | 提供有关开发 Excel 解决方案的文章和参考文档的链接。 这些链接并不特定于使用 Visual Studio 的 Office 开发。 |
