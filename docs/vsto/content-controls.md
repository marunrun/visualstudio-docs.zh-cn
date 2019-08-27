---
title: 内容控件
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.Toolbox.DropDownListContentControl
- VST.Toolbox.RichTextContentControl
- VST.Toolbox.PlainTextContentControl
- VST.Toolbox.ComboBoxContentControl
- VST.Toolbox.CCBuildingBlockGalleryContentControl
- VST.Toolbox.DatePickerContentControl
- VST.Toolbox.PictureContentControl
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document building blocks [Office development in Visual Studio]
- restricted permissions [Office development in Visual Studio]
- ComboBoxContentControl class
- PictureContentControl class
- PlainTextContentControl class
- Office documents [Office development in Visual Studio], restricted permissions
- RichTextContentControl class
- content controls [Office development in Visual Studio]
- building block gallery [Office development in Visual Studio]
- controls [Office development in Visual Studio], content controls
- GroupContentControl class
- documents [Office development in Visual Studio], restricted permissions
- DropDownListContentControl class
- DatePickerContentControl class
- data binding [Office development in Visual Studio], content controls
- content controls [Office development in Visual Studio], about content controls
- custom XML parts, content controls
- templates [Office development in Visual Studio], content controls
- BuildingBlockGalleryContentControl class
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4cecbaf834185e66d7d584d58d2abb4dbdf46f9e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445598"
---
# <a name="content-controls"></a>内容控件
  借助内容控件，可设计出具有以下功能的文档和模板：

- 用户界面 (UI)，包含类似于窗体的受控输入。

- 限制条件，防止用户编辑文档或模板中的受保护部分。 有关详细信息，请参阅[通过使用内容控件保护文档的某些部分](#Protection)。

- 与数据源绑定的数据。 有关详细信息，请参阅[将数据绑定到内容控件](#DataBinding)。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

  ![视频链接](../vsto/media/playvideo.gif "链接至视频")相关的视频演示，请参阅[将数据绑定到 Word 2007 内容控件适用于 Office system (3.0) 中使用 Visual Studio Tools](http://go.microsoft.com/fwlink/?LinkId=136785)。

## <a name="overview-of-content-controls"></a>内容控件概述
 内容控件提供了已针对用户输入和打印进行优化的 UI。 将内容控件添加到文档时，该控件通过边框、标题以及能够为用户提供说明的临时文本进行识别。 打印版本的文档中不会出现控件的边框和标题。

 例如，希望用户在文档的某一部分中输入日期时，可以向文档中添加日期选取器内容控件。 用户单击控件时，将出现标准日期选取器 UI。 还可以设置控件的属性，以设置显示的区域日历并指定日期格式。 用户选择日期之后，控件的 UI 会隐藏，而且当用户打印文档时，只会显示日期。

 内容控件还有助于执行以下操作：

- 防止用户编辑或删除文档各部分。 如果文档或模板中包含用户应能读取但无法编辑的信息，或者如果想让用户能够编辑内容控件但不能删除控件，可使用此方法。

- 将文档或模板中的某些部分绑定到数据。 可以将内容控件绑定到数据库字段、[!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] 中的托管对象、文档中存储的 XML 元素以及其他数据源。

  在文档级项目中，可以在设计时或运行时向文档中添加内容控件。 在 VSTO 外接程序项目中，可以在运行时向任何打开的文档中添加内容控件。 有关详细信息，请参阅[如何：向 Word 文档添加内容控件](../vsto/how-to-add-content-controls-to-word-documents.md)。

> [!NOTE]
> 仅在以 Open XML 格式保存的文档中，可以使用内容控件。 不能在 Word 97-2003 文档中保存的文档中使用内容控件 (*.doc*) 格式。

## <a name="types-of-content-controls"></a>类型的内容控件
 有九种不同类型的内容控件可添加到文档中。 大多数内容控件在 <xref:Microsoft.Office.Tools.Word> 命名空间内都具有对应的类型。 还可以使用通用 <xref:Microsoft.Office.Tools.Word.ContentControl> 以表示任一可用的内容控件。 有关演示如何使用每个可用的内容控件的演练，请参阅[演练：使用内容控件创建模板](../vsto/walkthrough-creating-a-template-by-using-content-controls.md)。

### <a name="build-block-gallery"></a>生成块库
 构建基块库可让用户从列表中选择*文档构建基块*要插入到文档。 文档构建基块是为了多次使用而创建的一段内容，例如共同的封面页、格式化表格或标头。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> 类型。 有关构建基块的详细信息，请参阅[What's new for Word 2007 中的开发人员](/previous-versions/office/developer/office-2007/bb266218(v=office.12))。

### <a name="check-box"></a>复选框
 复选框提供了代表二元状态（已选择或已清除）的 UI。

 和其他类型的内容控件不同，[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 不提供表示复选框内容控件的特定类型。 也就是说，没有 `CheckBoxContentControl` 类型。 不过，仍然可以通过编程方式向文档中添加通用 <xref:Microsoft.Office.Tools.Word.ContentControl>，以创建复选框内容控件。 有关详细信息，请参阅[Word 项目中的复选框内容控件](#checkbox)。

### <a name="combo-box"></a>组合框
 组合框显示了用户可以选择的项目列表。 和下拉列表不同，组合框允许用户添加自己的项。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> 类型。

### <a name="date-picker"></a>日期选取器
 日期选取器提供用于选择日期的日历 UI。 最终用户单击控件中的下拉箭头时，就会显示日历。 可以使用区域日历和不同的日期格式。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> 类型。

### <a name="drop-down-list"></a>下拉列表
 下拉列表显示了用户可以选择的项目列表。 和组合框不同的是，下拉列表不允许用户添加或编辑项。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 类型。

### <a name="group"></a>Group
 分组控件定义了文档中用户无法编辑或删除的受保护区域。 分组控件可以包含任何文档项，例如文本、表格、图形和其他内容控件。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Word.GroupContentControl> 类型。

### <a name="picture"></a>Picture
 图片控件显示图像。 可以在设计时或运行时指定图像，用户也可以单击此控件以选择要插入文档中的图像。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Word.PictureContentControl> 类型。

### <a name="rich-text"></a>格式文本
 富文本控件包含文本或其他项，例如表格、图片或其他内容控件。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 类型。

### <a name="plain-text"></a>纯文本
 纯文本控件包含文本。 纯文本控件不能包含其他项，例如表格、图片或其他内容控件。 此外，纯文本控件中的所有文本都具有相同的格式。 例如，将纯文本控件中某一句子的一个字设为斜体时，该控件中的所有文本都将变为斜体。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> 类型。

### <a name="generic-content-control"></a>通用内容控件
 通用内容控件是可以表示任何可用类型的内容控件的 <xref:Microsoft.Office.Tools.Word.ContentControl> 对象。 通过使用 <xref:Microsoft.Office.Tools.Word.ContentControl.Type%2A> 属性，可以更改 <xref:Microsoft.Office.Tools.Word.ContentControl> 对象，使其行为与其他类型的内容控件一样。 例如，若要创建表示纯文本控件的 <xref:Microsoft.Office.Tools.Word.ContentControl> 对象，可以在运行时更改此对象，使它的行为与组合框的一样。

 只能在运行时创建 <xref:Microsoft.Office.Tools.Word.ContentControl> 对象，而无法在设计时创建。 有关详细信息，请参阅[如何：向 Word 文档添加内容控件](../vsto/how-to-add-content-controls-to-word-documents.md)。

## <a name="common-features-of-content-controls"></a>内容控件的常用功能
 大多数内容控件共享一组可用于执行共同任务的成员。 下表描述了使用这些成员可执行的一些任务。

|对于此任务：|执行此操作：|
|--------------------|--------------|
|获取或设置控件中显示的文本。|使用**文本**属性。 **注意：** <xref:Microsoft.Office.Tools.Word.PictureContentControl> 和 <xref:Microsoft.Office.Tools.Word.ContentControl> 类型不具有此属性。|
|获取或设置在用户编辑控件、控件中填充数据源的数据或者控件的内容被删除之前，在控件中显示的临时文本。|使用**PlaceholderText**属性。 **注意：** <xref:Microsoft.Office.Tools.Word.PictureContentControl> 类型没有此属性。|
|获取或设置在用户单击时，显示在内容控件的边框中的标题。|使用**标题**属性。|
|用户编辑控件后，自动删除文档中的控件。 （控件中的文本保留在文档中。）|使用**临时**属性。|
|当用户在内容控件中单击，或者光标以编程方式移动到内容控件中时，运行代码。|处理控件的 <xref:Microsoft.Office.Tools.Word.ContentControlBase.Entering> 事件。|
|当用户在内容控件以外单击，或者光标以编程方式移动到内容控件以外时，运行代码。|处理控件的 <xref:Microsoft.Office.Tools.Word.ContentControlBase.Exiting> 事件。|
|在内容控件由于恢复或撤销操作而被添加到文档之后，运行代码。|处理控件的 <xref:Microsoft.Office.Tools.Word.ContentControlBase.Added> 事件。|
|在正要从文档中删除内容控件之前，运行代码。|处理控件的 <xref:Microsoft.Office.Tools.Word.ContentControlBase.Deleting> 事件。|

## <a name="Protection"></a> 使用内容控件保护文档的某些部分
 当保护文档的某一部分时，将阻止用户更改或删除文档该部分中的内容。 有以下几种可使用内容控件保护文档各部分的方式。

 如果要保护的区域位于内容控件中，则可以使用内容控件的属性来阻止用户编辑或删除控件：

- **LockContents**属性阻止用户编辑的内容。

- **LockContentControl**属性阻止用户删除控件。

  如果要保护的区域不在内容控件中，或者要保护的区域中包含内容控件和其他类型的内容，则可以将整个区域置于 <xref:Microsoft.Office.Tools.Word.GroupContentControl> 中。 与其他内容控件不同，<xref:Microsoft.Office.Tools.Word.GroupContentControl> 不提供任何对用户可见的 UI。 其唯一的目的是定义用户无法编辑的区域。

> [!NOTE]
> 如果创建包含嵌入式内容控件的 <xref:Microsoft.Office.Tools.Word.GroupContentControl>，则不会自动保护嵌入的内容控件。 必须使用**LockContents**每个属性嵌入控件以防止用户编辑其内容。

 有关如何使用内容控件保护文档的某些部分的详细信息，请参阅[如何：使用内容控件保护文档的某些部分](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)。

## <a name="DataBinding"></a> 将数据绑定到内容控件
 可通过将内容控件绑定到数据源，来显示文档中的数据。 数据源更新时，内容控件会反映出更改。 还可以将更改保存回数据源。

 内容控件提供以下数据绑定选项：

- 可以使用与 Windows 窗体相同的数据绑定模型，将内容控件绑定到数据库字段或托管对象。

- 可以将内容控件绑定到的 XML 片段中的元素 (也称为*自定义 XML 部件*) 嵌入在文档中。

  在 Office 解决方案中的主机控件绑定到数据的概述，请参阅[将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

### <a name="use-the-windows-forms-data-binding-model"></a>使用 Windows 窗体数据绑定模型
 大多数内容控件都支持 Windows 窗体使用的简单数据绑定模型。 简单数据绑定意味着将控件绑定到单个数据元素，例如数据表中某一列的值。 有关详细信息，请参阅[数据绑定和 Windows 窗体](/dotnet/framework/winforms/data-binding-and-windows-forms)。

 在文档级项目中，您可以将数据绑定到内容控件通过使用**数据源**窗口中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 有关如何将数据绑定内容控件添加到文档的详细信息，请参阅[如何：用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)和[如何：用对象中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-objects.md)。

 下表列出了可以绑定到在每种数据类型的内容控件**数据源**窗口。

|数据类型|默认内容控件|可以绑定到此数据类型的其他内容控件|
|---------------|-----------------------------|----------------------------------------------------------------|
|<xref:System.Boolean><br /><br /> <xref:System.Byte><br /><br /> <xref:System.Char><br /><br /> <xref:System.Double><br /><br /> <xref:System.Enum><br /><br /> <xref:System.Guid><br /><br /> <xref:System.Int16><br /><br /> <xref:System.Int32><br /><br /> <xref:System.Int64><br /><br /> <xref:System.SByte><br /><br /> <xref:System.Single><br /><br /> <xref:System.String><br /><br /> <xref:System.TimeSpan><br /><br /> <xref:System.UInt16><br /><br /> <xref:System.UInt32><br /><br /> <xref:System.UInt64>|<xref:Microsoft.Office.Tools.Word.PlainTextContentControl>|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DatePickerContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|
|<xref:System.DateTime>|<xref:Microsoft.Office.Tools.Word.DatePickerContentControl>|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PlainTextContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|
|<xref:System.Drawing.Image><br /><br /> <xref:System.Byte> 数组|<xref:Microsoft.Office.Tools.Word.PictureContentControl>|None|

 在文档级和 VSTO 外接程序项目中，可以使用控件中 <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> 属性的 <xref:System.Windows.Forms.ControlBindingsCollection.Add%2A> 方法，以编程方式将内容控件绑定到数据源。 如果这样做，在字符串中传递**文本**到*propertyName*参数的<xref:System.Windows.Forms.ControlBindingsCollection.Add%2A>方法。 **文本**属性是内容控件的默认数据绑定属性。

 内容控件还支持双向数据绑定，在这种绑定形式下，控件中的更改会更新到数据源。 有关详细信息，请参阅[如何：使用主机控件中的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)。

> [!NOTE]
> 内容控件不支持复杂数据绑定。 如果使用 Windows 窗体数据模型将 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 或 <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> 绑定到数据源，用户在单击控件时只能看到单个值。 如果希望将这些控件绑定到可供用户选择的一组数据值，则可以将这些控件绑定到自定义 XML 部件中的元素。

### <a name="bind-content-controls-to-custom-xml-parts"></a>将内容控件绑定到自定义 XML 部件
 可以将某些内容控件绑定到文档中内嵌的自定义 XML 部件的元素。 有关自定义 XML 部件的详细信息，请参阅[自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)。

 若要将内容控件绑定到自定义 XML 部件中的元素，使用**XMLMapping**控件的属性。 以下代码示例演示了如何将 <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> 绑定到 `Product` 节点下的 `Price` 元素，其中该节点位于已添加到文档的自定义 XML 部分中。

```vb
plainTextContentControl1.XMLMapping.SetMapping("/Product/Price")
```

```csharp
plainTextContentControl1.XMLMapping.SetMapping("/Product/Price", String.Empty, null);
```

 有关演示如何将内容控件绑定到更详细地自定义 XML 部件的演练，请参阅[演练：将内容控件绑定到自定义 XML 部件](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md)。

 将内容控件绑定到自定义 XML 部件时，会自动启用双向数据绑定。 当用户编辑控件中的文本时，相应的 XML 元素会自动更新。 同样，如果自定义 XML 部件中的元素值发生更改，则绑定到 XML 元素的内容控件将显示新的数据。

 可以将以下类型的内容控件绑定到自定义 XML 部件：

- <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl>

- <xref:Microsoft.Office.Tools.Word.DatePickerContentControl>

- <xref:Microsoft.Office.Tools.Word.DropDownListContentControl>

- <xref:Microsoft.Office.Tools.Word.PictureContentControl>

- <xref:Microsoft.Office.Tools.Word.PlainTextContentControl>

### <a name="data-bind-events-for-content-controls"></a>将数据绑定的内容控件的事件
 所有内容控件都提供一组可以处理的事件，以执行数据相关的任务，例如在更新数据源之前验证控件中的文本是否符合某些标准。 下表列出了与数据绑定有关的内容控件事件。

|任务|Event|
|----------|-----------|
|在 Word 正要自动更新已绑定到自定义 XML 部件的内容控件中的文本之前，运行代码。|<xref:Microsoft.Office.Tools.Word.ContentControlBase.ContentUpdating>|
|在 Word 正要自动更新已绑定到内容控件的自定义 XML 部件中的数据之前（即在内容控件中的文本更改之后），运行代码。|<xref:Microsoft.Office.Tools.Word.ContentControlBase.StoreUpdating>|
|运行自己的代码，以根据自定义标准验证控件的内容。|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Validating>|
|在成功验证控件的内容之后，运行代码。|<xref:Microsoft.Office.Tools.Word.ContentControlBase.Validated>|

## <a name="limitations-of-content-controls"></a>内容控件的限制
 在 Office 项目中使用内容控件时，请注意以下限制。

### <a name="behavior-differences-between-design-time-and-runtime"></a>在设计时和运行时的行为差异
 Microsoft Office Word 在运行时对内容控件施加的许多限制条件在设计时并不会执行。 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中设计文档级解决方案时，务必仅通过在运行时受支持的方式修改内容控件。

 如果你在设计时修改内容控件的方式是该控件在运行时并不支持的方式，则 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 设计器将不会提醒你注意不受支持的更改。 然而，当你调试或运行项目时，或者在保存并重新打开该项目时，Word 将显示一条错误消息并请求权限以修复文档。 修复文档时，Word 会删除控件中所有不受支持的内容和格式。

 例如在设计时，Word 不会阻止你将表格添加到 <xref:Microsoft.Office.Tools.Word.PlainTextContentControl>。 然而，因为 <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> 对象在运行时不能包含表格，所以在打开文档时 Word 会显示错误消息。

 另请注意，定义内容控件行为的很多属性在设计时不产生任何影响。 例如，如果您设置**LockContents**到内容控件的属性**True**在设计时，您仍可以编辑控件中的文本[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]设计器。 此属性只会在运行时阻止用户编辑控件。

### <a name="event-limitations"></a>事件限制
 内容控件不提供当用户更改控件中的文本或其他项时引发的事件。 例如，当用户选择 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 或 <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> 中的不同项时，不会引发任何事件。

 若要确定用户何时编辑内容控件的内容，可以将该控件绑定到自定义 XML 部件，然后处理 <xref:Microsoft.Office.Tools.Word.ContentControlBase.StoreUpdating> 事件。 当用户更改已绑定到自定义 XML 部件的控件的内容时，引发此事件。 有关演示如何将内容控件绑定到自定义 XML 部件的演练，请参阅[演练：将内容控件绑定到自定义 XML 部件](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md)。

### <a name="checkbox"></a> 在 Word 项目中的复选框内容控件
 Word 2010 引入了一种表示复选框的新型内容控件。 但是，[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]不提供相应的 CheckBoxContentControl 类型，以便在 Office 项目中使用。 若要在 [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 Word 2010 项目中创建复选框内容控件，请使用 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddContentControl%2A> 方法创建 <xref:Microsoft.Office.Tools.Word.ContentControl> 对象，然后将 <xref:Microsoft.Office.Interop.Word.WdContentControlType.wdContentControlCheckBox> 值传递到该方法，以指定复选框内容控件。 下面的代码示例演示如何执行此操作。

 [!code-vb[Trin_ContentControlReference#800](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/checkbox.vb#800)]
 [!code-csharp[Trin_ContentControlReference#800](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/checkbox.cs#800)]

## <a name="see-also"></a>请参阅
- [通过使用扩展的对象自动化 Word](../vsto/automating-word-by-using-extended-objects.md)
- [如何：向 Word 文档添加内容控件](../vsto/how-to-add-content-controls-to-word-documents.md)
- [演练：使用内容控件创建模板](../vsto/walkthrough-creating-a-template-by-using-content-controls.md)
- [Office 解决方案中的数据](../vsto/data-in-office-solutions.md)
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
