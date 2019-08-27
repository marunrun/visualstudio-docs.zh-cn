---
title: 扩展 Word 文档和 Excel 工作簿在 VSTO 外接在运行时
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- GetVstoObject method
- application-level add-ins [Office development in Visual Studio], adding controls to documents
- host items [Office development in Visual Studio], creating at run time in add-ins
- application-level add-ins [Office development in Visual Studio], extending Word documents
- application-level add-ins [Office development in Visual Studio], extending Excel workbooks
- controls [Office development in Visual Studio], adding at run time
- HasVstoObject method
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2058029bfc188cd3284768e3d1782f7cda96c5c1
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402110"
---
# <a name="extend-word-documents-and-excel-workbooks-in-vsto-add-ins-at-runtime"></a>扩展 Word 文档和 Excel 工作簿在 VSTO 外接在运行时
  你可以通过下列方式使用 VSTO 外接程序来自定义 Word 文档和 Excel 工作簿：

- 将托管控件添加到任意打开的文档或工作表。

- 将 Excel 工作表上的现有列表对象转换为扩展 <xref:Microsoft.Office.Tools.Excel.ListObject> ，后者可公开事件并能通过使用 Windows 窗体数据绑定模型绑定到数据。

- 访问由 Word 和 Excel 公开的用于特定文档、工作簿和工作表的应用程序级事件。

  若要使用此功能，你生成在运行时扩展文档或工作簿的对象。

  **适用于：** 在本文中的信息适用于 VSTO 外接程序项目类型提供的以下应用程序：Excel 和 Word。 有关详细信息，请参阅[按 Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)。

## <a name="generate-extended-objects-in-vsto-add-ins"></a>在 VSTO 外接程序中生成扩展的对象
 *扩展对象* 是由 Visual Studio Tools for Office Runtime 提供的类型的实例，该运行时可将功能添加到存在于 Word 或 Excel 对象模型中的本机对象（称为 *本机 Office 对象*）。 若要生成 Word 或 Excel 对象的扩展对象，请使用 `GetVstoObject` 方法。 第一次调用`GetVstoObject`方法指定的 Word 或 Excel 对象，它将返回扩展指定的对象的新对象。 每次调用方法并指定相同 Word 或 Excel 对象时，它将返回相同的扩展对象。

 扩展对象的类型具有与本机 Office 对象的类型相同的名称，但该类型是在 <xref:Microsoft.Office.Tools.Excel> 或 <xref:Microsoft.Office.Tools.Word> 命名空间中定义的。 例如，如果调用 `GetVstoObject` 方法来扩展 <xref:Microsoft.Office.Interop.Word.Document> 对象，则该方法将返回 <xref:Microsoft.Office.Tools.Word.Document> 对象。

 `GetVstoObject` 方法应主要用于 VSTO 外接程序项目。 你还可以在文档级项目中使用这些方法，但它们的行为有所不同，并且用途更少。

 若要确定是否为特定的本机 Office 对象生成了扩展对象，请使用 `HasVstoObject` 方法。 有关详细信息，请参阅[确定是否扩展了 Office 对象](#HasVstoObject)。

### <a name="generate-host-items"></a>生成主机项
 当你使用`GetVstoObject`来扩展文档级别对象 (即<xref:Microsoft.Office.Interop.Excel.Workbook>， <xref:Microsoft.Office.Interop.Excel.Worksheet>，或<xref:Microsoft.Office.Interop.Word.Document>)，返回的对象称为*主机项*。 主机项是可以包含其他对象的类型，包括其他扩展对象和控件。 它类似于在 Word 或 Excel 主互操作程序集中相应的类型，但它具有附加功能。 有关主机项的详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

 生成主机项后，可将其用于将托管控件添加到文档、工作簿或工作表中。 有关详细信息，请参阅[添加托管控件添加到文档和工作表](#AddControls)。

#### <a name="to-generate-a-host-item-for-a-word-document"></a>若要生成 Word 文档的主机项

- 以下代码示例演示了如何生成活动文档的主机项。

     [!code-vb[Trin_WordAddInDynamicControls#8](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#8)]
     [!code-csharp[Trin_WordAddInDynamicControls#8](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#8)]

#### <a name="to-generate-a-host-item-for-an-excel-workbook"></a>若要生成 Excel 工作簿的主机项

- 以下代码示例演示了如何生成活动工作簿的主机项。

     [!code-vb[Trin_ExcelAddInDynamicControls#2](../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb#2)]
     [!code-csharp[Trin_ExcelAddInDynamicControls#2](../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs#2)]

#### <a name="to-generate-a-host-item-for-an-excel-worksheet"></a>若要生成 Excel 工作表的主机项

- 以下代码示例演示了如何为项目中的活动工作表生成主机项。

     [!code-vb[Trin_ExcelAddInDynamicControls#1](../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb#1)]
     [!code-csharp[Trin_ExcelAddInDynamicControls#1](../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs#1)]

### <a name="generate-listobject-host-controls"></a>生成 ListObject 主机控件
 当使用 `GetVstoObject` 方法扩展 <xref:Microsoft.Office.Interop.Excel.ListObject> 时，该方法将返回一个 <xref:Microsoft.Office.Tools.Excel.ListObject>。 <xref:Microsoft.Office.Tools.Excel.ListObject>具有的所有原始功能<xref:Microsoft.Office.Interop.Excel.ListObject>。 它还具有其他功能，并可以通过使用 Windows 窗体数据绑定模型绑定到数据。 有关详细信息，请参阅[ListObject 控件](../vsto/listobject-control.md)。

#### <a name="to-generate-a-host-control-for-a-listobject"></a>若要为 ListObject 生成主机控件

- 以下代码示例演示了如何为项目中活动工作表内第一个 <xref:Microsoft.Office.Tools.Excel.ListObject> 生成 <xref:Microsoft.Office.Interop.Excel.ListObject> 。

     [!code-vb[Trin_ExcelAddInDynamicControls#3](../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb#3)]
     [!code-csharp[Trin_ExcelAddInDynamicControls#3](../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs#3)]

### <a name="AddControls"></a> 将托管的控件添加到文档和工作表
 在生成 <xref:Microsoft.Office.Tools.Word.Document> 或 <xref:Microsoft.Office.Tools.Excel.Worksheet>后，你可以将控件添加到这些扩展对象表示的文档或工作表。 若要添加控件，请使用`Controls`的属性<xref:Microsoft.Office.Tools.Word.Document>或<xref:Microsoft.Office.Tools.Excel.Worksheet>。 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

 可以添加 Windows 窗体控件或 *主机控件*。 主机控件是由包装 Word 或 Excel 主互操作程序集中一个相应控件的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 所提供的控件。 主机控件公开的所有基础本机 Office 对象的行为。 它还会引发事件，并可以通过使用 Windows 窗体数据绑定模型绑定到数据。 有关详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

> [!NOTE]
> 不能通过使用 VSTO 外接程序将 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 控件添加到工作表，或是将 <xref:Microsoft.Office.Tools.Word.XMLNode> 或 <xref:Microsoft.Office.Tools.Word.XMLNodes> 控件添加到文档。 不能以编程方式添加这些主机控件。 有关详细信息，请参阅[主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

### <a name="persist-and-remove-controls"></a>保存和删除控件
 当你将托管控件添加到文档或工作表中时，在保存文档并将其关闭时，不会保留这些控件。 所有主机控件都将被删除，仅留下基础本机 Office 对象。 例如，一个 <xref:Microsoft.Office.Tools.Excel.ListObject> 将变成 <xref:Microsoft.Office.Interop.Excel.ListObject>。 所有 Windows 窗体控件也将被删除，但控件的 ActiveX 包装会留在文档中。 你必须在 VSTO 外接程序中包括清理控件的代码，或包括在下次打开该文档时重新创建这些控件的代码。 有关详细信息，请参阅[持久保存在 Office 文档中的动态控件](../vsto/persisting-dynamic-controls-in-office-documents.md)。

## <a name="access-application-level-events-on-documents-and-workbooks"></a>访问应用程序级别事件上的文档和工作簿
 本机 Word 和 Excel 对象模型中的某些文档、工作簿和工作表事件仅在应用程序级引发。 例如，在 Word 中打开文档时会引发 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> 事件，但是此事件是在 <xref:Microsoft.Office.Interop.Word.Application> 类而不是 <xref:Microsoft.Office.Interop.Word.Document> 类中定义的。

 当在 VSTO 外接程序中仅使用本机 Office 对象时，必须处理这些应用程序级的事件，然后编写附加代码以确定引发该事件的文档是否为你已自定义的文档。 主机项可提供这些文档级事件，因此，更易于处理特定文档的事件。 你可以生成一个主机项，然后处理该主机项的事件。

### <a name="example-that-uses-native-word-objects"></a>使用本机 Word 对象示例
 以下代码示例演示了如何处理 Word 文档的应用程序级事件。 `CreateDocument` 方法可创建一个新文档，然后定义一个 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> 事件处理程序，以防止保存此文档。 事件是引发的一个应用程序级别事件<xref:Microsoft.Office.Interop.Word.Application>对象和事件处理程序必须比较`Doc`参数与`document1`对象，以确定如果`document1`表示已保存的文档。

 [!code-vb[Trin_WordAddInDynamicControls #12](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#12)]
 [!code-csharp[Trin_WordAddInDynamicControls#12](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#12)]

### <a name="examples-that-use-a-host-item"></a>使用主机项的示例
 以下代码示例通过处理 <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> 主机项的 <xref:Microsoft.Office.Tools.Word.Document> 事件简化了此过程。 `CreateDocument2`方法在这些示例将生成<xref:Microsoft.Office.Tools.Word.Document>该项`document2`对象，然后定义<xref:Microsoft.Office.Tools.Word.Document.BeforeSave>防止保存该文档的事件处理程序。 事件处理程序调用时，才`document2`会保存，并且可以取消保存操作而无需执行任何额外操作来验证保存了哪个文档。

 以下代码示例演示了此任务。

 [!code-vb[Trin_WordAddInDynamicControls #13](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#13)]
 [!code-csharp[Trin_WordAddInDynamicControls#13](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#13)]

## <a name="HasVstoObject"></a> 确定是否扩展了 Office 对象
 若要确定是否为特定的本机 Office 对象生成了扩展对象，请使用 `HasVstoObject` 方法。 此方法返回 **，则返回 true**如果已生成了扩展的对象。

 使用 `Globals.Factory.HasVstoMethod` 方法。 在希望为扩展对象测试的本机 Word 或 Excel 对象中传递，如 <xref:Microsoft.Office.Interop.Word.Document> 或 <xref:Microsoft.Office.Interop.Excel.Worksheet>。

 当希望仅在指定 Office 对象包括扩展对象的情况下运行代码时，可以使用 `HasVstoObject` 方法。 例如，如果您有 Word VSTO 外接程序中处理<xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave>事件从文档中删除托管的控件，则在保存前，请使用`HasVstoObject`方法，以确定是否已扩展文档。 如果尚未扩展该文档，它不能管理控件和事件处理程序可以返回而不尝试进行清理文档上的控件。

## <a name="see-also"></a>请参阅
- [VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
