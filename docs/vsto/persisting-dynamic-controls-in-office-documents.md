---
title: 持久保存在 Office 文档中的动态控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Office documents [Office development in Visual Studio, host controls
- controls [Office development in Visual Studio], persisting in the document
- Windows Forms controls [Office development in Visual Studio], persisting in the document
- documents [Office development in Visual Studio], Windows Forms controls
- documents [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], persisting in the document
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8fd44d535cd8a9920ebc3de37d0c483a19dac8f8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62976594"
---
# <a name="persist-dynamic-controls-in-office-documents"></a>持久保存在 Office 文档中的动态控件

保存并关闭文档或工作簿时，不会保留在运行时添加的控件。 具体的行为与宿主控件和 Windows 窗体控件不同。 在这两种情况下，都可以为解决方案添加代码，在用户重新打开该文档时重新创建这些控件。

在运行时添加到文档中的控件称为 *动态控件*。 有关动态控件的详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="persist-host-controls-in-the-document"></a>持久保存在文档中的主机控件

保存并关闭文档后，所有动态宿主控件会从文档中删除。 只会留下基础本机 Office 对象。 例如， <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> 宿主控件将变成 <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName>。 本机 Office 对象未连接到宿主控件事件，并且不具备宿主控件的数据绑定功能。

下表列出了文档中保留的每种宿主控件的本机 Office 对象。

|宿主控件类型|本机 Office 对象类型|
|-----------------------|-------------------------------|
|<xref:Microsoft.Office.Tools.Excel.Chart>|<xref:Microsoft.Office.Interop.Excel.Chart>|
|<xref:Microsoft.Office.Tools.Excel.ListObject>|<xref:Microsoft.Office.Interop.Excel.ListObject>|
|<xref:Microsoft.Office.Tools.Excel.NamedRange>|<xref:Microsoft.Office.Interop.Excel.Range>|
|<xref:Microsoft.Office.Tools.Word.Bookmark>|<xref:Microsoft.Office.Interop.Word.Bookmark>|
|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DatePickerContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DropDownListContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.GroupContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PictureContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PlainTextContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|<xref:Microsoft.Office.Interop.Word.ContentControl>|

### <a name="re-create-dynamic-host-controls-when-documents-are-opened"></a>打开文档时重新创建动态宿主控件

用户每次打开文档时，可以重新创建动态宿主控件来代替现有的本机控件。 打开文档时，用这种方式创建宿主控件可模拟用户可能经历的体验。

若要为 Word 重新创建宿主控件或<xref:Microsoft.Office.Tools.Excel.NamedRange>或<xref:Microsoft.Office.Tools.Excel.ListObject>为 Excel 中，使用托管控件`Add` \<*控件类*> 方法<xref:Microsoft.Office.Tools.Excel.ControlCollection?displayProperty=fullName>或<xref:Microsoft.Office.Tools.Word.ControlCollection?displayProperty=fullName>对象。 使用包含本机 Office 对象参数的方法。

例如，如果想要在打开文档时从现有的本机 <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> 中创建 <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName> 宿主控件，应使用 <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddListObject%2A> 方法并传入现有的 <xref:Microsoft.Office.Interop.Excel.ListObject>。 下面的代码示例演示了如何在 Excel 的文档级项目中进行此操作。 该代码会重新创建动态 <xref:Microsoft.Office.Tools.Excel.ListObject> ，它基于 <xref:Microsoft.Office.Interop.Excel.ListObject> 类中名为 `MyListObject` 的现有 `Sheet1` 创建。

[!code-csharp[Trin_ExcelWorkbookDynamicControls#6](../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/Sheet1.cs#6)]
[!code-vb[Trin_ExcelWorkbookDynamicControls#6](../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/Sheet1.vb#6)]

### <a name="re-create-chart"></a>重新创建图表

若要重新创建<xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName>宿主控件，必须首先删除本机<xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName>，然后重新创建<xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName>使用<xref:Microsoft.Office.Tools.Excel.ControlCollection.AddChart%2A>方法。 没有任何`Add` \<*控制类*> 方法，可用于创建新<xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName>基于现有<xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName>。

如果不首先删除本机<xref:Microsoft.Office.Interop.Excel.Chart>，然后重新创建时，将创建第二个重复的图表<xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName>。

## <a name="persist-windows-forms-controls-in-documents"></a>持久保存在文档中的 Windows 窗体控件

保存并关闭文档后， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 会自动从文档中删除所有动态创建的 Windows 窗体控件。 但是，对于文档级和 VSTO 外接程序项目，此行为有所不同。

在文档级自定义项中，控件及其基础 ActiveX 包装（用于在文档上承载控件）会在下次打开该文档时被删除。 没有迹象表明这里曾经存在控件。

在 VSTO 外接程序中，控件会被删除，但 ActiveX 包装仍保留在文档中。 用户下次打开文档时，还可以看到 ActiveX 包装。 在 Excel 中，ActiveX 包装会显示上次保存文档时显示的控件图像。 在 Word 中，不会显示 ActiveX 包装，除非用户单击它们，在这种情况下，会在控件边框上显示一圈虚线。 有几种方法可以删除 ActiveX 包装。 有关详细信息，请参阅[外接程序中删除 ActiveX 包装](#removingActiveX)。

### <a name="re-create-windows-forms-controls-when-documents-are-opened"></a>打开文档时重新创建 Windows 窗体控件

当用户重新打开文档时，可以重新创建已删除的 Windows 窗体控件。 为此，必须执行下列任务：

1. 保存或关闭文档时，存储关于大小、位置和控件状态的信息。 文档级自定义项，可以将数据保存到文档中的数据缓存。 在 VSTO 外接程序中，可以将数据保存到文档中的自定义 XML 部件中。

2. 打开文档时，在引发的事件中重新创建控件。 在文档级项目中，可以在 `Sheet`*n*`_Startup` 或 `ThisDocument_Startup` 事件处理程序中执行此操作。 在 VSTO 外接程序项目中，可以在 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookOpen> 或 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> 事件的事件处理程序中执行此操作。

### <a name="removingActiveX"></a> 在外接程序中删除 ActiveX 包装

通过使用 VSTO 外接程序可将动态 Windows 窗体控件添加到文档中，可以防止出现在该文档中通过以下方式打开下一次控件的 ActiveX 包装。

#### <a name="remove-activex-wrappers-when-the-document-is-opened"></a>打开文档时删除 ActiveX 包装

若要删除所有 ActiveX 包装，请调用 `GetVstoObject` 方法为表示新打开文档的 <xref:Microsoft.Office.Interop.Word.Document> 或 <xref:Microsoft.Office.Interop.Excel.Workbook> 生成宿主项。 例如，若要从 Word 文档中删除所有 ActiveX 包装，可以调用 `GetVstoObject` 方法来为 <xref:Microsoft.Office.Interop.Word.Document> 对象生成宿主项，该对象会传递给 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> 事件的事件处理程序。

知道只能在安装 VSTO 外接程序的计算机上打开文档时，此过程非常有用。 如果该文档可能会传递给其他未安装 VSTO 外接程序的用户，请考虑在关闭文档之前删除控件。

下面的代码示例演示如何在打开文档时调用 `GetVstoObject` 方法。

[!code-vb[Trin_WordAddInDynamicControls#11](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#11)]
[!code-csharp[Trin_WordAddInDynamicControls#11](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#11)]

尽管`GetVstoObject`方法主要用于生成在运行时的新主机项，此方法调用的特定文档的第一个时间也将清除从文档的所有 ActiveX 包装。 有关如何使用详细信息`GetVstoObject`方法，请参阅[扩展 Word 文档和 Excel 工作簿中运行时在 VSTO 加载项](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

如果 VSTO 外接程序中创建动态控件打开文档时，VSTO 外接程序将调用`GetVstoObject`方法过程来创建控件的一部分。 此方案中，不需要添加对 `GetVstoObject` 方法的单独调用来删除 ActiveX 包装。

#### <a name="remove-the-dynamic-controls-before-the-document-is-closed"></a>关闭文档之前删除动态控件

在关闭文档之前，VSTO 外接程序可以从文档中显式删除每个动态控件。 对于可能传递给其他未安装 VSTO 外接程序的用户的文档而言，此过程非常有用。

以下代码示例演示了如何在文档关闭时，从 Word 文档中删除所有 Windows 窗体控件。

[!code-vb[Trin_WordAddInDynamicControls#10](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#10)]
[!code-csharp[Trin_WordAddInDynamicControls#10](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#10)]

## <a name="see-also"></a>请参阅

- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
