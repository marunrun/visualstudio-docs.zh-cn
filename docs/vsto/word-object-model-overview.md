---
title: Word 对象模型概述
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word object model
- Word [Office development in Visual Studio], object model
- object models [Office development in Visual Studio], Office
- object models [Office development in Visual Studio], Word
- objects [Office development in Visual Studio], Office object models
- Office object models
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f1b8ae7c56cf6f7cb20dd237c9106498a752e267
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254969"
---
# <a name="word-object-model-overview"></a>Word 对象模型概述
  在 Visual Studio 中开发 Word 解决方案时，会与 Word 对象模型进行交互。 此对象模型包含 Word 的主互操作程序集中所提供的类和接口，并在 <xref:Microsoft.Office.Interop.Word> 命名空间中进行定义。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 本主题概要介绍 Word 对象模型。 有关可了解整个 Word 对象模型的详细信息的资源，请参阅[使用 word 对象模型文档](#WordOMDocumentation)。

 有关使用 Word 对象模型执行特定任务的信息，请参阅下列主题：

- [使用文档](../vsto/working-with-documents.md)

- [处理文档中的文本](../vsto/working-with-text-in-documents.md)

- [使用表](../vsto/working-with-tables.md)

## <a name="understanding"></a>了解 Word 对象模型
 Word 提供了数百个可与之交互的对象。 这些对象采用严格遵循用户界面的层次结构进行组织。 <xref:Microsoft.Office.Interop.Word.Application> 对象位于层次结构的顶部。 此对象表示 Word 的当前实例。 <xref:Microsoft.Office.Interop.Word.Application> 对象包含 <xref:Microsoft.Office.Interop.Word.Document>、 <xref:Microsoft.Office.Interop.Word.Selection>、 <xref:Microsoft.Office.Interop.Word.Bookmark>和 <xref:Microsoft.Office.Interop.Word.Range> 对象。 上述每个对象均具有很多方法和属性，可用于操作对象和与之进行交互。

 下图显示了 Word 对象模型层次结构中这些对象的一个视图。

 ![Word 对象模型图](../vsto/media/wrwordobjectmodel.gif "Word 对象模型图")

 初看起来，对象似乎重叠在一起。 例如， <xref:Microsoft.Office.Interop.Word.Document> 和 <xref:Microsoft.Office.Interop.Word.Selection> 对象都是 <xref:Microsoft.Office.Interop.Word.Application> 对象的成员，但 <xref:Microsoft.Office.Interop.Word.Document> 对象也是 <xref:Microsoft.Office.Interop.Word.Selection> 对象的成员。 <xref:Microsoft.Office.Interop.Word.Document> 和 <xref:Microsoft.Office.Interop.Word.Selection> 对象都包含 <xref:Microsoft.Office.Interop.Word.Bookmark> 和 <xref:Microsoft.Office.Interop.Word.Range> 对象。 因为有多种方法可以访问相同类型的对象，所以存在重叠。 例如，你将格式设置应用于 <xref:Microsoft.Office.Interop.Word.Range> 对象；但你可能想要访问当前选定内容、某一特定段落，某一节或整个文档的范围。

 下列各节简要介绍了顶级对象以及它们彼此交互的方式。 这些对象包括下列五种：

- 应用程序对象

- 文档对象

- Selection 对象

- Range 对象

- Bookmark 对象

  除 Word 对象模型以外，Visual Studio 中的 Office 项目还提供可扩展 Word 对象模型中的一些对象的 *主机项* 和 *主机控件* 。 主机项和主机控件的行为类似于它们扩展的 Word 对象，但它们还具有其他功能（如数据绑定功能）和额外事件。 有关详细信息，请参阅[使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)和[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

### <a name="application-object"></a>应用程序对象
 <xref:Microsoft.Office.Interop.Word.Application> 对象表示 Word 应用程序，并且是所有其他对象的父级。 其成员通常作为一个整体应用于 Word。 你可以使用其属性和方法来控制 Word 环境。

 在 VSTO 外接程序项目中，可以通过使用 <xref:Microsoft.Office.Interop.Word.Application> 类的 `Application` 字段来访问 `ThisAddIn` 对象。 有关详细信息，请参阅[PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

 在文档级项目中，可以通过使用 <xref:Microsoft.Office.Interop.Word.Application> 类的 <xref:Microsoft.Office.Tools.Word.Document.Application%2A> 属性来访问 `ThisDocument` 对象。

### <a name="document-object"></a>文档对象
 <xref:Microsoft.Office.Interop.Word.Document> 对象是 Word 编程的中心。 它表示一个文档及其所有内容。 当你打开文档或创建新文档时，将创建新的 <xref:Microsoft.Office.Interop.Word.Document> 对象，并将其添加到 <xref:Microsoft.Office.Interop.Word.Documents> 对象的 <xref:Microsoft.Office.Interop.Word.Application> 集合。 具有焦点的文档被称为活动文档。 它由 <xref:Microsoft.Office.Interop.Word._Application.ActiveDocument%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Application> 属性表示。

 Visual Studio 中的 Office 开发工具通过提供 <xref:Microsoft.Office.Interop.Word.Document> 类型来扩展 <xref:Microsoft.Office.Tools.Word.Document> 对象。 此类型是一个 *主机项* ，使你可以访问 <xref:Microsoft.Office.Interop.Word.Document> 对象的所有功能，并增添了其他事件以及添加托管控件的能力。

 在创建文档级项目时，可以通过使用项目中生成的 <xref:Microsoft.Office.Tools.Word.Document> 类访问 `ThisDocument` 成员。 通过使用 <xref:Microsoft.Office.Tools.Word.Document> 类中代码的 **Me** 或 **this** 关键字、或通过使用 `ThisDocument` 类外部的代码的 `Globals.ThisDocument` ，即可访问 `ThisDocument` 对象。 有关详细信息，请参阅[程序文档级自定义项](../vsto/programming-document-level-customizations.md)。 例如，若要在文档中选择第一个段落，请使用下列代码。

 [!code-vb[Trin_VstcoreWordAutomation#120](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#120)]
 [!code-csharp[Trin_VstcoreWordAutomation#120](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#120)]

 在 VSTO 外接程序项目中，可以在运行时生成 <xref:Microsoft.Office.Tools.Word.Document> 主机项。 可以使用生成的主机项将控件添加到关联文档。 有关详细信息，请参阅[在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

### <a name="selection-object"></a>Selection 对象
 <xref:Microsoft.Office.Interop.Word.Selection> 对象表示当前所选的区域。 在 Word 用户界面中执行操作（如文本加粗）时，可以选择或突出显示文本，然后应用格式设置。 文档中始终存在 <xref:Microsoft.Office.Interop.Word.Selection> 对象。 如果未选中任何内容，则它表示插入点。 此外，选定内容可包含多个不相邻的文本块。

### <a name="range-object"></a>Range 对象
 <xref:Microsoft.Office.Interop.Word.Range> 对象表示文档中的相邻区域，并由起始字符位置和结束字符位置进行定义。 并不仅限于单个 <xref:Microsoft.Office.Interop.Word.Range> 对象。 你可以在同一文档中定义多个 <xref:Microsoft.Office.Interop.Word.Range> 对象。 <xref:Microsoft.Office.Interop.Word.Range> 对象具有以下特性：

- 它可以只包含单独的插入点，也可包含一个文本范围或整个文档。

- 它包括非打印字符，如空格、制表符和段落标记。

- 它可以是当前选定内容所表示的区域，也可以表示不同于此内容的区域。

- 它在文档中不可见，这与选定内容不同，后者总是可见。

- 它不随文档一起保存，且仅在代码运行时才存在。

  当在某个范围的末尾插入文本时，Word 会自动扩展该范围以包括插入的文本。

### <a name="content-control-objects"></a>内容控件对象
 <xref:Microsoft.Office.Interop.Word.ContentControl> 提供一种用于控制 Word 文档内文本和其他类型的内容的输入和呈现的方法。 <xref:Microsoft.Office.Interop.Word.ContentControl> 可以显示多种不同类型的 UI，它们进行了优化以在 Word 文档中使用，如多信息文本控件、日期选取器或组合框。 你还可以使用 <xref:Microsoft.Office.Interop.Word.ContentControl> 来防止用户编辑文档或模板的某些节。

 Visual Studio 会将 <xref:Microsoft.Office.Interop.Word.ContentControl> 对象扩展到几个不同的主机控件。 虽然 <xref:Microsoft.Office.Interop.Word.ContentControl> 对象能显示可用于内容控件的所有不同类型的 UI，Visual Studio 还是为每个内容控件提供了一个不同的类型。 例如，你可以使用 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 来创建多信息文本控件，或者可以使用 <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> 来创建日期选取器。 这些主机控件的行为与本机 <xref:Microsoft.Office.Interop.Word.ContentControl>的类似，但它们还具有其他事件和数据绑定功能。 有关详细信息，请参阅[内容控件](../vsto/content-controls.md)。

### <a name="bookmark-object"></a>Bookmark 对象
 <xref:Microsoft.Office.Interop.Word.Bookmark> 对象表示文档中的相邻区域，同时具有起始位置和结束位置。 你可以使用书签标记文档中的某个位置，也可将其作为文档中文本的容器。 <xref:Microsoft.Office.Interop.Word.Bookmark> 对象可以包含插入点，也可以与整个文档一样大。 <xref:Microsoft.Office.Interop.Word.Bookmark> 具有下列特征，以将其与 <xref:Microsoft.Office.Interop.Word.Range> 对象区别开来：

- 你可以在设计时命名书签。

- <xref:Microsoft.Office.Interop.Word.Bookmark> 对象随文档一起保存，因此在代码停止运行或文档关闭时不会被删除。

- 通过将 <xref:Microsoft.Office.Interop.Word.View.ShowBookmarks%2A> 属性来访问 <xref:Microsoft.Office.Interop.Word.View> 属性设置为 **false** 或 **true**。

  Visual Studio 通过提供 <xref:Microsoft.Office.Interop.Word.Bookmark> 主机控件来扩展 <xref:Microsoft.Office.Tools.Word.Bookmark> 对象。 <xref:Microsoft.Office.Tools.Word.Bookmark> 主机控件的行为与本机 <xref:Microsoft.Office.Interop.Word.Bookmark>的类似，但它们还具有其他事件和数据绑定功能。 你可以将数据绑定到文档上的书签控件，操作方式与将数据绑定到 Windows 窗体上文本框控件的方式相同。 有关详细信息，请参阅[书签控件](../vsto/bookmark-control.md)。

## <a name="WordOMDocumentation"></a>使用 Word 对象模型文档
 有关 Word 对象模型的完整信息，可以参考 Word 主互操作程序集 (PIA) 引用和 Visual Basic for Applications (VBA) 对象模型引用。

### <a name="primary-interop-assembly-reference"></a>主互操作程序集引用
 Word PIA 参考文档介绍了 Word 的主互操作程序集中的类型。 此文档可从以下位置获得：[Word 2010 主互操作程序集引用](http://go.microsoft.com/fwlink/?LinkId=189588)。

 有关 Word PIA 设计的详细信息（例如 PIA 中类和接口之间的差异以及如何实现 PIA 中的事件），请参阅[Office 主互操作程序集中的类和接口的概述](http://go.microsoft.com/fwlink/?LinkId=189592)。

### <a name="vba-object-model-reference"></a>VBA 对象模型引用
 VBA 对象模型引用在将 Word 对象模型公开到 VBA 代码时对该对象进行了记录。 有关详细信息，请参阅[Word 2010 对象模型引用](http://go.microsoft.com/fwlink/?LinkId=199772)。

 VBA 对象模型引用中的所有对象和成员都与 Word PIA 中的类型和成员相对应。 例如，VBA 对象模型引用中的文档对象对应于 Word PIA 中<xref:Microsoft.Office.Interop.Word.Document>的对象。 虽然 VBA 对象模型引用提供了大多数属性、方法和事件的代码示例，但如果要在用 Visual Studio 创建的 Word 项目中使用本引用中的 VBA 代码，必须将其转换为 Visual Basic 或 Visual C# 代码。

## <a name="see-also"></a>请参阅
- [Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)
- [使用文档](../vsto/working-with-documents.md)
- [处理文档中的文本](../vsto/working-with-text-in-documents.md)
- [使用表](../vsto/working-with-tables.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
