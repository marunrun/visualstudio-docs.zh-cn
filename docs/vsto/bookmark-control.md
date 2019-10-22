---
title: Bookmark 控件
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.Toolbox.Bookmark
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- bookmarks, controlling
- Bookmark control, data binding
- Bookmark control, events
- Bookmark control
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2b8557581e93c8d2ba5a54a13c04d5de74b24f71
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255150"
---
# <a name="bookmark-control"></a>Bookmark 控件
  <xref:Microsoft.Office.Tools.Word.Bookmark> 控件是一个具有唯一名称且用于公开事件的书签，可以绑定到数据。 可以将书签用作占位符以在 Microsoft Office Word 文档中标记项或位置。 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件是 <xref:Microsoft.Office.Interop.Word.Bookmark> 对象和 <xref:Microsoft.Office.Interop.Word.Range> 对象的组合。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 在文档级项目中，你可以在设计时或运行时向文档中添加 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件。 在 VSTO 外接程序项目中，可以在运行时向任何打开的文档添加 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件。 有关详细信息，请参阅[如何：向 Word 文档](../vsto/how-to-add-bookmark-controls-to-word-documents.md)添加书签控件。

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件支持简单数据绑定。 应该使用 <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> 属性将书签绑定到数据源。 书签的默认数据绑定属性是 <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> 属性。

 如果更新绑定数据集中的数据，则该<xref:Microsoft.Office.Tools.Word.Bookmark>控件将显示所做的更改。

 在文档级项目中，还可以使用“数据源” 窗口将数据绑定到书签。 有关详细信息，请参阅[如何：用对象](../vsto/how-to-populate-documents-with-data-from-objects.md)中的数据填充文档。

## <a name="formatting"></a>格式化
 可应用于 <xref:Microsoft.Office.Interop.Word.Bookmark> 的格式设置也可应用于 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件。 此格式包括字体、缩进、间距、编号和样式。

## <a name="assign-text-to-the-bookmark"></a>为书签分配文本
 <xref:Microsoft.Office.Interop.Word.Bookmark?displayProperty=nameWithType> 对象和 <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType> 控件之间的另一个差异在于将文本分配给书签时其行为方式的不同。 如果向零长度 <xref:Microsoft.Office.Interop.Word.Bookmark?displayProperty=nameWithType>分配文本，文本将被追加到书签右侧，且书签的长度保持为零。 但是，如果向零长度 <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType>分配文本，文本将被插入到书签中，且书签的长度将扩展到所插入字符的总数。

 <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType> 控件还具有 <xref:Microsoft.Office.Tools.Word.Bookmark.Text?displayProperty=nameWithType> 属性。 此<xref:Microsoft.Office.Interop.Word.Range.Text?displayProperty=nameWithType>属性与<xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType>控件的<xref:Microsoft.Office.Tools.Word.Bookmark.Range?displayProperty=nameWithType>属性或<xref:Microsoft.Office.Interop.Word.Bookmark.Range?displayProperty=nameWithType> <xref:Microsoft.Office.Interop.Word.Bookmark?displayProperty=nameWithType>对象的属性上可用的属性不同。

|Text 属性|描述|
|-------------------|-----------------|
|<xref:Microsoft.Office.Tools.Word.Bookmark.Text?displayProperty=nameWithType>|使用此属性可以在书签内显示文本，并使书签保留在文档中。 向书签分配文本会扩展书签范围，但不会删除书签。<br /><br /> 例如， `Bookmark1.Text = "Hello world"` 将文本插入书签中，且使书签保持原样。|
|<xref:Microsoft.Office.Interop.Word.Range.Text?displayProperty=nameWithType>|使用此属性可在书签位置处显示文本，并自动删除该书签。 例如， `Bookmark1.Range.Text = "Hello world"` 将文本插入书签中，并删除该书签。|

## <a name="rename-the-control-at-design-time"></a>在设计时重命名控件
 在文档级项目中，将 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件从“工具箱” 拖到文档中时，Visual Studio 会自动为该控件生成一个名称。 可以在“属性” 窗口中更改控件的名称。

## <a name="overlapping-controls"></a>重叠控件
 书签控件可以相互重叠。 相同的文本可以由多个书签共享。 向其中一个重叠书签分配新文本时，该书签将仅包含新文本，并且书签不再重叠。 现在，另一个书签只包含原始重叠书签之间未共享的文本。

 下表说明句子“This is sample text.” 由两个重叠书签共享：

|书签|Text|
|--------------|----------|
|重叠书签|[this is {sample] text.}|
|Bookmark1|This is sample|
|Bookmark2|sample text.|

 如果向 Bookmark1 分配新文本“This is replacement.”，则书签不再重叠并且 对于 Bookmark1，书签不会重叠，并且 Bookmark2 仅保留最初不属于 Bookmark1 的文本。

|书签|Text|
|--------------|----------|
|两个单独的书签|[this is replacement]{ text.}|
|Bookmark1|This is replacement|
|Bookmark2|text.|

如果更改包含其他书签的书签的文本，则不会删除内部书签。 但是，内部书签将变成空书签并移动到外部书签的末尾。

下表说明句子“This is sample text.” 由包含在另一个书签中的书签共享：

|书签|Text|
|--------------|----------|
|重叠书签|[this is {sample} text.]|
|Bookmark1|This is sample text.|
|Bookmark2|示例|

 如果向 Bookmark1 分配新文本“This is replacement.”，则书签不再重叠并且 Bookmark2 变成位于 Bookmark1 末尾的空书签。

|书签|Text|
|--------------|----------|
|两个单独的书签|[这是替换。]{}|
|Bookmark1|This is replacement.|
|Bookmark2|*\<empty>*|

## <a name="events"></a>事件

以下事件可用于 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件：

- <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Word.Bookmark.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Word.Bookmark.Deselected>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.Bookmark.Selected>

- <xref:Microsoft.Office.Tools.Word.Bookmark.SelectionChange>

## <a name="see-also"></a>请参阅

- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)
- [如何：向 Word 文档添加书签控件](../vsto/how-to-add-bookmark-controls-to-word-documents.md)
- [演练：为书签创建快捷菜单](../vsto/walkthrough-creating-shortcut-menus-for-bookmarks.md)
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)