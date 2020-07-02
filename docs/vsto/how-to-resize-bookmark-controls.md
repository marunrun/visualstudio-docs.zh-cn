---
title: 如何：调整书签控件的大小
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- Bookmark control, resizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6cc7b26bb767c233ed8699519261d4b5b708306b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545855"
---
# <a name="how-to-resize-bookmark-controls"></a>如何：调整书签控件的大小
  当你将 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件添加到 Microsoft Office Word 文档时，可以设置它的大小。 稍后还可以重设其大小。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 有三种方法可以重设书签的大小：

- 添加或删除 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件中的文本。

   每次在书签中添加文本时，该书签的大小会自动增加以包含新的文本。 删除文本时，书签的大小会自动减小。

- 更改 <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> 控件的 <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> 和 <xref:Microsoft.Office.Tools.Word.Bookmark> 属性。

   如果只将大小更改几个字符，此方法很有用。

- 重新创建 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件。

   如果将对书签的大小或位置作出重大更改，此方法很有用。

  在文档级项目中，你可以在设计时或在运行时向项目中的文档添加 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件。 在 VSTO 外接程序项目中，可以在运行时向任何打开的文档添加 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件。 有关详细信息，请参阅[如何：将书签控件添加到 Word 文档](../vsto/how-to-add-bookmark-controls-to-word-documents.md)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="change-the-start-and-end-properties"></a>更改开始和结束属性

### <a name="to-resize-a-bookmark-in-a-document-level-project-at-design-time"></a>在设计时重设文档级项目中的书签大小

1. 在“属性” **** 窗口中选择书签。

2. 增大或减小 <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> 属性的值。

3. 增大或减小 <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> 属性的值。

### <a name="to-resize-a-bookmark-in-a-document-level-project-at-run-time"></a>在运行时重设文档级项目中的书签大小

1. 修改在运行或设计时创建的 <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> 的 <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> 和 <xref:Microsoft.Office.Tools.Word.Bookmark> 属性。

     下面的代码示例演示添加五个字符到名为 `SampleBookmark`的书签的起始位置。 此代码假定该书签之前的文本至少有五个字符。

     [!code-csharp[Trin_VstcoreHostControlsWord#2](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#2)]
     [!code-vb[Trin_VstcoreHostControlsWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#2)]

     下面的代码示例演示添加五个字符到同一个书签的结束位置。 此代码假定该书签之后的文本至少有五个字符。

     [!code-csharp[Trin_VstcoreHostControlsWord#3](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#3)]
     [!code-vb[Trin_VstcoreHostControlsWord#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#3)]

### <a name="to-resize-a-bookmark-in-a-vsto-add-in-project-at-run-time"></a>在运行时在 VSTO 外接程序项目中调整书签大小

1. 修改在运行时创建的 <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> 的 <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> 和 <xref:Microsoft.Office.Tools.Word.Bookmark> 属性。

     下面的代码示例演示创建包含活动文档第一段中文本的 <xref:Microsoft.Office.Tools.Word.Bookmark> ，然后删除 <xref:Microsoft.Office.Tools.Word.Bookmark>开始和结束位置的 5 个字符。

     [!code-vb[Trin_WordAddInDynamicControls#16](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#16)]
     [!code-csharp[Trin_WordAddInDynamicControls#16](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#16)]

## <a name="recreate-the-bookmark"></a>重新创建书签
 你可以通过添加与现有书签具有相同名称但大小不同的新书签来重设书签的大小。

### <a name="to-recreate-a-bookmark-in-a-document-level-project-at-design-time"></a>在设计时重新创建文档级项目中的书签

1. 选择要包含在新 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件中的文本。

2. 在“插入” **** 菜单上，单击“书签” ****。

3. 在“书签” **** 对话框中，选择想要重设其大小的书签的名称，并单击“添加” ****。

## <a name="see-also"></a>请参阅
- [如何：向 Word 文档添加书签控件](../vsto/how-to-add-bookmark-controls-to-word-documents.md)
- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [如何：调整 NamedRange 控件的大小](../vsto/how-to-resize-namedrange-controls.md)
- [如何：调整 ListObject 控件的大小](../vsto/how-to-resize-listobject-controls.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
