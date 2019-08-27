---
title: 如何：管理操作窗格上的控件布局
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 264b7cd4d60ebc963d794e0ca06fc16fd5edc7d7
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445352"
---
# <a name="how-to-manage-control-layout-on-actions-panes"></a>如何：管理操作窗格上的控件布局
  操作窗格停靠到的文档或工作表右侧默认设置。但是，它可停靠到左侧、 顶部或底部。 如果使用多个用户控件，可以编写代码以正确堆栈操作窗格上的用户控件。 有关详细信息，请参阅[操作窗格概述](../vsto/actions-pane-overview.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 控件的堆叠顺序取决于操作窗格是否停靠垂直或水平。

> [!NOTE]
> 如果在用户调整在运行时操作窗格，可以设置要与操作窗格重设大小的控件。 你可以使用 Windows 窗体控件的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性将控件定位到操作窗格。 有关详细信息，请参阅[如何：Windows 窗体上的控件的定位点](/dotnet/framework/winforms/controls/how-to-anchor-controls-on-windows-forms)。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="to-set-the-stack-order-of-the-actions-pane-controls"></a>若要设置操作窗格控件的堆叠顺序

1. 打开包含操作窗格具有多个用户控件或嵌套的操作窗格控件的 Microsoft Office Word 文档级项目。 有关详细信息，请参阅[如何：将操作窗格添加到 Word 文档或 Excel 工作簿](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)。

2. 右键单击**ThisDocument.cs**或**ThisDocument.vb**中**解决方案资源管理器**，然后单击**查看代码**。

3. 在<xref:Microsoft.Office.Tools.ActionsPane.OrientationChanged>事件处理程序的操作窗格中，如果操作窗格的方向为水平的检查。

     [!code-csharp[Trin_VstcoreActionsPaneWord#30](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#30)]
     [!code-vb[Trin_VstcoreActionsPaneWord#30](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#30)]

4. 如果方向为水平，堆栈操作窗格控件从左侧;否则，从顶部开始放置它们。

     [!code-csharp[Trin_VstcoreActionsPaneWord#31](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#31)]
     [!code-vb[Trin_VstcoreActionsPaneWord#31](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#31)]

5. 在 C# 中，必须添加的事件处理程序`ActionsPane`到<xref:Microsoft.Office.Tools.Word.Document.Startup>事件处理程序。 有关创建事件处理程序的信息，请参阅[如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreActionsPaneWord#32](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#32)]

6. 运行该项目，并验证时操作窗格停靠在文档的顶部和控件的堆积从上到下的操作窗格停靠在文档的右侧时，操作窗格控件的堆叠从左到右。

## <a name="example"></a>示例
 [!code-csharp[Trin_VstcoreActionsPaneWord#29](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#29)]
 [!code-vb[Trin_VstcoreActionsPaneWord#29](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#29)]

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 控制与操作窗格，其中包含多个用户控件或嵌套的操作窗格的 Word 文档级项目。

## <a name="see-also"></a>请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [如何：将操作窗格添加到 Word 文档或 Excel 工作簿](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [如何：将操作窗格添加到 Word 文档或 Excel 工作簿](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [演练：从操作窗格的文档中插入文本](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [演练：从操作窗格的文档中插入文本](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
