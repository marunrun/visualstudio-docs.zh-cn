---
title: 如何：使用内容控件保护文档的某些部分
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- partial document protection [Office development in Visual Studio]
- content controls [Office development in Visual Studio], protecting documents
- Word [Office development in Visual Studio], partial document protection
- document protection [Office development in Visual Studio]
- Word [Office development in Visual Studio], restricted permissions
- GroupContentControl
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b03521023ea0b4d92bd3125f256d2230de9bba03
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541344"
---
# <a name="how-to-protect-parts-of-documents-by-using-content-controls"></a>如何：使用内容控件保护文档的某些部分
  当你保护文档的一部分时，将阻止用户更改或删除文档该部分中的内容。 通过使用内容控件，有以下几种方法来保护 Microsoft Office Word 文档的各个部分：

- 你可以保护内容控件。

- 你可以保护不在内容控件中的文档的一部分。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="protect-a-content-control"></a><a name="EditDeleteControl"></a>保护内容控件
 可以通过在设计时或运行时设置文档级项目中控件的属性，阻止用户编辑或删除内容控件。

 还可以使用 VSTO 外接程序项目保护在运行时添加到文档中的内容控件。 有关详细信息，请参阅[如何：向 Word 文档添加内容控件](../vsto/how-to-add-content-controls-to-word-documents.md)。

### <a name="to-protect-a-content-control-at-design-time"></a>若要在设计时保护内容控件

1. 在托管在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 设计器中的文档中，选择想要保护的内容控件。

2. 在 "**属性**" 窗口中，设置以下一个或两个属性：

    - 若要阻止用户编辑控件，请将**LockContents**设置为**True**。

    - 若要防止用户删除控件，请将**LockContentControl**设置为**True**。

3. 单击 **“确定”** 。

### <a name="to-protect-a-content-control-at-run-time"></a>若要在运行时保护内容控件

1. 将 `LockContents` 内容控件的属性设置为**true**可阻止用户编辑控件，并将 `LockContentControl` 属性设置为**true** ，以防止用户删除控件。

     下面的代码示例演示如何使用文档级项目的两个不同 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 对象的 <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContents%2A> 和 <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContentControl%2A> 属性。 若要运行此代码，将此代码添加到项目的 `ThisDocument` 类中，然后从 `AddProtectedContentControls` 事件处理程序调用 `ThisDocument_Startup` 方法。

     [!code-csharp[Trin_ContentControlHowToProtect#2](../vsto/codesnippet/CSharp/Trin_ContentControlHowToProtect/ThisDocument.cs#2)]
     [!code-vb[Trin_ContentControlHowToProtect#2](../vsto/codesnippet/VisualBasic/Trin_ContentControlHowToProtect/ThisDocument.vb#2)]

     下面的代码示例演示了如何使用 VSTO 外接程序项目的两个不同 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 对象的 <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContents%2A> 和 <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContentControl%2A> 属性。 若要运行此代码，将此代码添加到项目的 `ThisAddIn` 类中，然后从 `AddProtectedContentControls` 事件处理程序调用 `ThisAddIn_Startup` 方法。

     [!code-vb[Trin_WordAddInDynamicControls#14](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#14)]
     [!code-csharp[Trin_WordAddInDynamicControls#14](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#14)]

## <a name="protect-a-part-of-a-document-that-is-not-in-a-content-control"></a>保护不在内容控件中的文档的一部分
 可通过将文档的某一区域放置到 <xref:Microsoft.Office.Tools.Word.GroupContentControl> 中，阻止用户更改该区域。 这在以下应用场景中很有用：

- 想要保护不包含内容控件的区域。

- 想要保护其中已包含内容控件，但想要保护的文本或其他项不在内容控件中的区域。

> [!NOTE]
> 如果创建包含嵌入式内容控件的 <xref:Microsoft.Office.Tools.Word.GroupContentControl>，则不会自动保护嵌入的内容控件。 若要阻止用户编辑嵌入的内容控件，请使用控件的**LockContents**属性。

### <a name="to-protect-an-area-of-a-document-at-design-time"></a>若要在设计时保护文档的某一区域

1. 在托管在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 设计器中的文档中，选择想要保护的区域。

2. 在功能区上，单击 **“开发人员”** 选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅[如何：在功能区上显示 "开发人员" 选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

3. 在 "**控件**" 组中，单击 "**组**" 下拉按钮，然后单击 "**组**"。

     不会在你的项目的 `ThisDocument` 类中自动生成包含受保护区域的 <xref:Microsoft.Office.Tools.Word.GroupContentControl>。 表示组控件的边框会在设计时可见，但在运行时则不存在可见边框。

### <a name="to-protect-an-area-of-a-document-at-run-time"></a>若要在运行时保护文档的某一区域

1. 以编程方式选择想要保护的区域，然后再调用 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddGroupContentControl%2A> 方法来创建 <xref:Microsoft.Office.Tools.Word.GroupContentControl>。

     下面针对于文档级项目的代码示例将文本添加到文档中第一个段落中，选择第一个段落，然后实例化 <xref:Microsoft.Office.Tools.Word.GroupContentControl>。 若要运行此代码，将此代码添加到项目的 `ThisDocument` 类中，然后从 `ProtectFirstParagraph` 事件处理程序调用 `ThisDocument_Startup` 方法。

     [!code-csharp[Trin_ContentControlHowToProtect#1](../vsto/codesnippet/CSharp/Trin_ContentControlHowToProtect/ThisDocument.cs#1)]
     [!code-vb[Trin_ContentControlHowToProtect#1](../vsto/codesnippet/VisualBasic/Trin_ContentControlHowToProtect/ThisDocument.vb#1)]

     下面针对于 VSTO 外接程序项目的代码示例将文本添加到活动文档中第一个段落，选择第一个段落，然后实例化 <xref:Microsoft.Office.Tools.Word.GroupContentControl>。 若要运行此代码，将此代码添加到项目的 `ThisAddIn` 类中，然后从 `ProtectFirstParagraph` 事件处理程序调用 `ThisAddIn_Startup` 方法。

     [!code-vb[Trin_WordAddInDynamicControls#15](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#15)]
     [!code-csharp[Trin_WordAddInDynamicControls#15](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#15)]

## <a name="see-also"></a>请参阅
- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)
- [内容控件](../vsto/content-controls.md)
- [如何：向 Word 文档添加内容控件](../vsto/how-to-add-content-controls-to-word-documents.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
