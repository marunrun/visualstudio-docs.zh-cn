---
title: 如何：管理操作窗格上的控件布局
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes [Office development in Visual Studio], control layout
- controls [Office development in Visual Studio], layout on actions panes
- smart documents [Office development in Visual Studio], control layout
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b6df90847000560299b8b1a6f259ffa6e7df0729
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520142"
---
# <a name="how-to-manage-control-layout-on-actions-panes"></a>如何：管理操作窗格上的控件布局
  默认情况下，操作窗格停靠在文档或工作表的右侧;但是，可以将其停靠在左侧、顶部或底部。 如果使用多个用户控件，则可以编写代码以正确地在操作窗格上堆叠用户控件。 有关详细信息，请参阅[操作窗格概述](../vsto/actions-pane-overview.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 控件的堆栈顺序取决于操作窗格是垂直停靠还是水平停靠。

> [!NOTE]
> 如果用户在运行时调整操作窗格的大小，则可以将控件设置为在 "操作" 窗格中调整大小。 你可以使用 Windows 窗体控件的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性将控件定位到操作窗格。 有关详细信息，请参阅[如何：在 Windows 窗体上定位控件](/dotnet/framework/winforms/controls/how-to-anchor-controls-on-windows-forms)。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="to-set-the-stack-order-of-the-actions-pane-controls"></a>设置操作窗格控件的堆栈顺序

1. 打开包含包含多个用户控件或嵌套操作窗格控件的操作窗格 Microsoft Office Word 的文档级项目。 有关详细信息，请参阅[如何：将操作窗格添加到 Word 文档或 Excel 工作簿](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)。

2. 在**解决方案资源管理器**中右键单击 " **ThisDocument.cs** " 或 " **ThisDocument** "，然后单击 "**查看代码**"。

3. 在 <xref:Microsoft.Office.Tools.ActionsPane.OrientationChanged> 操作窗格的事件处理程序中，检查操作窗格的方向是否为水平。

     [!code-csharp[Trin_VstcoreActionsPaneWord#30](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#30)]
     [!code-vb[Trin_VstcoreActionsPaneWord#30](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#30)]

4. 如果方向是水平的，则从左边堆叠操作窗格控件;否则，请从顶部堆栈。

     [!code-csharp[Trin_VstcoreActionsPaneWord#31](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#31)]
     [!code-vb[Trin_VstcoreActionsPaneWord#31](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#31)]

5. 在 c # 中，必须向 `ActionsPane` 事件处理程序添加的事件处理程序 <xref:Microsoft.Office.Tools.Word.Document.Startup> 。 有关创建事件处理程序的信息，请参阅[如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreActionsPaneWord#32](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#32)]

6. 运行该项目并验证当操作窗格停靠在文档的顶部时，操作窗格控件是否从左向右堆积到右侧，当操作窗格停靠在文档的右侧时，这些控件将从上到下堆叠。

## <a name="example"></a>示例
 [!code-csharp[Trin_VstcoreActionsPaneWord#29](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#29)]
 [!code-vb[Trin_VstcoreActionsPaneWord#29](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#29)]

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 带有操作窗格的 Word 文档级项目，其中包含多个用户控件或嵌套操作窗格控件。

## <a name="see-also"></a>另请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [如何：向 Word 文档或 Excel 工作簿添加操作窗格](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [如何：向 Word 文档或 Excel 工作簿添加操作窗格](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [演练：将文本从操作窗格插入到文档中](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [演练：将文本从操作窗格插入到文档中](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
