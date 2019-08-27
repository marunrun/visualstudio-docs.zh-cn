---
title: Windows 窗体控件在 Office 文档概述
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- old data showing in error [Office development in Visual Studio]
- Windows Forms controls [Office development in Visual Studio], Word
- Windows Forms controls [Office development in Visual Studio], adding
- Windows Forms controls [Office development in Visual Studio], arranging
- data [Office development in Visual Studio], old data showing in error
- user controls [Office development in Visual Studio], Windows Forms
- Windows Forms controls [Office development in Visual Studio]
- Windows Forms controls [Office development in Visual Studio], removing
- application development [Office development in Visual Studio], Windows Forms controls
- controls [Office development in Visual Studio], Windows Forms controls
- Office [Office development in Visual Studio], Windows Forms controls
- Office documents [Office development in Visual Studio, controls
- documents [Office development in Visual Studio], Windows Forms controls
- document-level customizations [Office development in Visual Studio], Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], about Windows Forms controls
- Office applications [Office development in Visual Studio], Windows Forms
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 927451ed35ce4bbdfbff7531b2828b0571354f34
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445363"
---
# <a name="windows-forms-controls-on-office-documents-overview"></a>Windows 窗体控件在 Office 文档概述
  Windows 窗体控件是用户可与之交互以便输入或操作数据的对象。 在 Microsoft Office Excel 和 Microsoft Office Word 文档级项目中，您可以添加 Windows 窗体控件的文档或工作簿项目中在设计时，或以编程方式可以在运行时添加这些控件。 以编程方式可以向任何打开的文档或工作表在 VSTO 外接程序中的运行时添加这些控件，Excel 或 Word。

 有关详细信息，请参阅[如何：将 Windows 窗体控件添加到 Office 文档](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)。

 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="use-windows-forms-controls"></a>使用 Windows 窗体控件

可以将 Windows 窗体控件添加到文档以及可自定义用户界面 (UI) 元素中，可自定义用户界面元素包括操作窗格、自定义任务窗格和 Windows 窗体。 通常，Windows 窗体控件在文档上的行为与在其他这些 UI 元素上的行为相同，但是也存在一些差异。 有关信息，请参阅[限制的 Windows 窗体控件上的 Office 文档](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)。

将 Windows 窗体控件添加到文档还是添加到其他某个 UI 元素的决定，取决于多个因素。 设计解决方案的 UI 时，请考虑下表中描述的 Windows 窗体控件的用法。

在文档上。
- 希望始终显示控件时。

- 希望用户在文档中直接输入数据时，例如，在编辑图面已锁定的基于窗体的文档中。

- 希望控件与文档中的数据对齐显示时。 例如，如果正向列表对象的每一行添加按钮，你将希望这些按钮与每个列表项对齐。

在操作窗格或自定义任务窗格上。
- 希望为用户提供上下文信息时。

- 只希望结果（而非查询控件和数据）显示在文档中时。

- 希望确保控件不与文档一起打印时。

- 希望确保控件不会影响文档的视图时。

在 Windows 窗体上。
- 希望控制 UI 的大小时。

- 希望防止用户隐藏或删除控件时。

- 希望获取用户输入，并防止用户在输入被接收之前在文档中执行任何操作时。

## <a name="add-windows-forms-controls-programmatically"></a>以编程方式添加 Windows 窗体控件
 可以将 Windows 窗体控件添加到 Word 文档和 Excel 工作表在运行时。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 提供了用于添加最常用的 Windows 窗体控件的帮助程序方法。 利用这些帮助程序方法，可以快速向 Office 文档添加控件并访问这些控件的组合的 Windows 窗体控件功能及 Office 相关功能。

 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

## <a name="use-windows-forms-controls-in-document-level-projects"></a>在文档级项目中使用 Windows 窗体控件
 在文档上使用 Windows 窗体控件的某些方面是特定于文档级项目的，它们允许你使用 Visual Studio 设计器设计文档的 UI。

### <a name="create-custom-user-controls"></a>创建自定义用户控件
 可以将用户控件添加到项目中，然后将其添加到“工具箱” 。 然后可以将用户控件直接拖动到文档中，与向文档添加 Windows 窗体控件的操作一样。 在创建用户控件时，需要注意以下事项：

- 请勿创建 **sealed** 用户控件。 将控件拖到文档中时，Visual Studio 会生成一个从该用户控件派生的包装类，以扩展该用户控件并支持在文档上使用该用户控件。 如果该用户控件为 **sealed**，则 Visual Studio 不能生成包装类。

- 用户控件必须将 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性设置为 **true**。 在 Office 项目内创建的用户控件的此属性默认设置为 **true** ，但属于外部项目的用户控件可能没有将此属性设置为 **true**。

- 向文档添加了用户控件后，请不要在项目内重命名或删除 <xref:System.Windows.Forms.UserControl> 类。 如果需要更改用户控件的名称，必须首先将其从文档中删除，更改了名称后，再将其添加到文档中。

### <a name="arrange-controls-at-design-time"></a>在设计时排列控件
 如果在设计时将多个控件添加到 Word 和 Excel 文档中，则可以在 Visual Studio 中使用“Microsoft Office Word”  和“Microsoft Office Excel”  工具栏来快速设置所有选定控件的排列。 仅当文档或工作表在设计器中打开时，这些工具栏才可用。

 在设计器中选定多个控件后，可以使用这些工具栏上的以下按钮来排列这些控件：

- **左对齐**

- **居中对齐**

- **右对齐**

- **顶部对齐**

- **中间对齐**

- **底部对齐**

- **使水平间距相等**

- **使垂直间距相等**

> [!NOTE]
> 在 Word 项目中，仅当所选控件未与文本对齐时，这些按钮才启用。 默认情况下，在设计时添加到文档中的控件与文本对齐。

### <a name="prevent-old-data-from-appearing-in-excel-workbooks-during-loading"></a>禁止旧数据在加载期间在 Excel 工作簿中显示
 在设计时将 Windows 窗体控件添加到文档或工作表后，在用户关闭文档时，这些控件将保留在文档中。 在设计时添加的控件也称为 *静态控件*。

 打开一个包含静态控件的 Excel 工作簿后，该工作簿会在 ActiveX 控件中显示静态控件的位图，直到自定义项代码运行并加载实际控件。 Excel 创建此位图，并在每次保存工作簿时将位图存储在工作簿中。 位图显示上次保存工作簿时控件的外观，包括控件显示的所有数据。 有关包含 Windows 窗体控件和位图的 ActiveX 控件的详细信息，请参阅[限制的 Windows 窗体控件上的 Office 文档](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)。

 某些情况下，代码不会进行加载而仅显示位图，例如当用户在设计模式下打开工作簿时。 而且，如果用户在未安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 的计算机上打开工作簿，自定义项将无法运行以加载控件，因此只有控件的位图是可见的。 在保存工作簿并将其发送给其他用户之前，应总是从工作簿上的控件中删除个人信息，以确保不会意外泄漏你的个人信息。

### <a name="match-control-size-to-cell-size-on-an-excel-worksheet"></a>在 Excel 工作表的单元格大小匹配控件大小
 可以将控件设置为当父单元格的大小更改时自动重设大小。 有关详细信息，请参阅[如何：调整工作表单元格中的控件的大小](../vsto/how-to-resize-controls-within-worksheet-cells.md)。

### <a name="add-components-that-are-shared-by-all-worksheets"></a>添加由所有工作表共享的组件
 可以将希望在所有工作表之间共享的组件（如 <xref:System.Data.DataSet>）添加到工作簿设计器而不是工作表。 该组件将出现在组件栏中。

### <a name="formula-for-embedding-controls-on-an-excel-worksheet"></a>嵌入的 Excel 工作表上的控件的公式
 当在 Excel 中选择一个控件时， **“公式栏”** 中将显示 **=EMBED("WinForms.Control.Host","")**。 此文本是必需的并且不应删除。

### <a name="layout-style-of-controls-on-a-word-document"></a>Word 文档上的控件的布局样式
 如果在文档级项目中使用 Visual Studio 设计器向 Word 文档添加控件，该控件将与文本对齐。 若要更改控件的布局样式，请右击控件，然后单击“设置控件格式” 。 在“设置对象格式”  对话框的“布局”  页上，选择换行样式。

 通过使用不同时向在运行时的 Word 文档添加控件，可以指定新的控件的布局样式`Add` \<*控制类*> 方法重载<xref:Microsoft.Office.Tools.Word.ControlCollection>类：

- 若要使控件与文本对齐，请使用接受 <xref:Microsoft.Office.Interop.Word.Range> （用于指定该控件的位置）的重载。

- 若要将控件作为浮点形状添加到文档中，请使用接受此控件的左坐标和上坐标的重载。

  有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

  如果在 Visual Studio 设计器中打开 Word 模板，则模板上的非内联控件可能不可见，因为 Visual Studio 在“普通”  视图中打开该模板。 若要查看控件，请将视图更改为“打印布局” 。

### <a name="controls-outside-the-main-document-body"></a>主文档正文外控件
 页眉或页脚内、或子文档内不支持 Windows 窗体控件。

### <a name="add-components-at-design-time"></a>在设计时添加组件
 一些控件或组件在文档中不可见，而是显示在组件栏中。 Visual Studio 为每个文档窗口都提供了一个组件栏。 仅当文档中存在组件时，组件栏才会显示在屏幕上。

## <a name="see-also"></a>请参阅
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [Windows 窗体控件](/dotnet/framework/winforms/controls/index)
- [Office 文档上的 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
- [如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [如何：调整工作表单元格中的控件的大小](../vsto/how-to-resize-controls-within-worksheet-cells.md)
- [如何：打印时隐藏工作表上的控件](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)
- [演练：更改工作表格式设置使用 CheckBox 控件](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)
- [演练：更改文档格式设置使用 CheckBox 控件](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)
- [演练：在使用按钮的工作表中的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)
- [演练：在文本框中使用按钮在文档中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)
- [Office 文档上的 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
- [演练：更新的图表中使用单选按钮的文档](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)
- [演练：更新使用单选按钮的工作表中的图表](../vsto/walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons.md)
