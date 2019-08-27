---
title: 如何：向 Office 文档添加 Windows 窗体控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], adding
- controls [Office development in Visual Studio], Windows Forms controls
- documents [Office development in Visual Studio], Windows Forms controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9241cb34ca380b2efe0b3c2ceb7f5d11376bef2f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63427493"
---
# <a name="how-to-add-windows-forms-controls-to-office-documents"></a>如何：向 Office 文档添加 Windows 窗体控件
  你可以在设计时在文档级项目中，将 Windows 窗体控件添加到 Microsoft Office Excel 和 Microsoft Office Word 文档。 在运行时，您可以在文档级自定义项和 VSTO 外接程序中添加控件。例如，你可以将 <xref:Microsoft.Office.Tools.Excel.Controls.ComboBox> 控件添加到工作表，以便用户可以从选项列表选择。

 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

 本主题介绍了以下任务：

- [在设计时添加控件](#designtime)

- [在运行时在文档级项目中添加控件](#runtimedoclevel)

- [在运行时在 VSTO 外接程序中添加控件](#runtimeaddin)

  ![视频链接](../vsto/media/playvideo.gif "链接至视频")相关的视频演示，请参阅[如何实现：将控件添加到文档图面在运行时？](http://go.microsoft.com/fwlink/?LinkId=132782).

## <a name="designtime"></a> 在设计时添加控件
 有几种方式在设计时向文档级项目中的文档添加 Windows 窗体控件。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-drag-a-windows-forms-control-to-the-document"></a>若要将 Windows 窗体控件拖到文档

1. 在 Visual Studio 中创建或打开 Excel 工作簿项目或 Word 文档项目，以使文档在设计器中可见。 有关创建项目的信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 在中**公共控件**选项卡**工具箱**，单击你想要添加，的控件并将其拖到文档。

    > [!NOTE]
    > 当在 Excel 中选择一个控件时， **“公式栏”** 中将显示 **=EMBED("WinForms.Control.Host","")**。 此文本是必需的并且不应删除。

### <a name="to-draw-a-windows-forms-control-on-the-document"></a>若要在文档中绘制 Windows 窗体控件

1. 在 Visual Studio 中创建或打开 Excel 工作簿项目或 Word 文档项目，以使文档在设计器中可见。 有关创建项目的信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 在中**公共控件**选项卡**工具箱**，单击你想要添加的控件。

3. 在文档中，单击希望要定位的控件的左上角位置，然后拖动到要定位的控件的右下角位置。

     该控件将按指定的位置和大小添加到文档。

    > [!NOTE]
    > 在 Excel 中选择一个控件，你会看到 **=EMBED("WinForms.Control.Host","")** 中**公式栏**。 此文本是必需的并且不应删除。

### <a name="to-add-a-windows-forms-control-to-the-document-by-single-clicking-the-control"></a>若要通过右键单击控件将 Windows 窗体控件添加到文档

1. 在 Visual Studio 中创建或打开 Excel 工作簿项目或 Word 文档项目，以使文档在设计器中可见。 有关创建项目的信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 在中**公共控件**选项卡**工具箱**，单击你想要添加的控件

3. 在文档中，单击希望要添加的控件的位置。

     该控件将以默认大小添加到文档。

    > [!NOTE]
    > 当在 Excel 中选择一个控件时， **“公式栏”** 中将显示 **=EMBED("WinForms.Control.Host","")**。 此文本是必需的并且不应删除。

### <a name="to-add-a-windows-forms-control-to-the-document-by-double-clicking-the-control"></a>若要通过双击控件将 Windows 窗体控件添加到文档

1. 在 Visual Studio 中创建或打开 Excel 工作簿项目或 Word 文档项目，以使文档在设计器中可见。 有关创建项目的信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 在中**公共控件**选项卡**工具箱**，双击你想要添加的控件。

     该控件将被添加到位于文档或活动窗格中心位置处的文档。

    > [!NOTE]
    > 当在 Excel 中选择一个控件时， **“公式栏”** 中将显示 **=EMBED("WinForms.Control.Host","")**。 此文本是必需的并且不应删除。

### <a name="to-add-a-windows-forms-control-to-the-document-by-pressing-the-enter-key"></a>若要向文档添加 Windows 窗体控件，通过按 Enter 键

1. 在 Visual Studio 中创建或打开 Excel 工作簿项目或 Word 文档项目，以使文档在设计器中可见。 有关创建项目的信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 在**公共控件**选项卡**工具箱**，单击你想要添加，然后按的控件**Enter**密钥。

     该控件将被添加到位于文档或活动窗格中心位置处的文档。

    > [!NOTE]
    > 当在 Excel 中选择一个控件时， **“公式栏”** 中将显示 **=EMBED("WinForms.Control.Host","")**。 此文本是必需的并且不应删除。

## <a name="runtimedoclevel"></a> 在运行时在文档级项目中添加控件
 以编程方式可以在运行时向文档添加 Windows 窗体控件。 在 Word 中，请使用 `ThisDocument` 类的 <xref:Microsoft.Office.Tools.Word.DocumentBase.Controls%2A> 属性的方法。 在 Excel 中，使用的方法<xref:Microsoft.Office.Tools.Excel.WorksheetBase.Controls%2A>的属性`Sheet` *n*类。 每种方法都具有好几个重载，使你能够以不同的方式指定控件的位置。

 当在运行时向文档添加 Windows 窗体控件时，控件文档关闭时不保存在文档中。 你可以在下次打开文档时重新创建该控件。 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

### <a name="to-add-a-windows-forms-control-at-runtime"></a>若要在运行时添加 Windows 窗体控件

1. 使用一种方法具有名称外\<*控制类*> (其中*控件类*是想要添加，例如在 Windows 窗体控件的类名<xref:Microsoft.Office.Tools.Word.ControlExtensions.AddButton%2A>)。

     下面的代码示例演示如何添加<xref:Microsoft.Office.Tools.Excel.Controls.Button>到单元格**C5**的`Sheet1`Excel 的文档级项目中。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#4](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#4)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#4](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#4)]

## <a name="runtimeaddin"></a> 在运行时在 VSTO 外接程序中添加控件
 您可以向任何打开的文档，在运行时以编程方式添加 Windows 窗体控件。 首先，生成一个基于打开的文档或工作表的主机项。 然后，在 Word 中，使用新主机项的 <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> 属性的方法。 然后，在 Excel 中，使用新主机项的 <xref:Microsoft.Office.Tools.Excel.Worksheet.Controls%2A> 属性的方法。 每种方法都具有好几个重载，使你能够以不同的方式指定控件的位置。

 当在运行时向文档添加 Windows 窗体控件时，控件文档关闭时不保存在文档中。 你可以在下次打开文档时重新创建该控件。 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

 在 VSTO 外接程序项目中生成主机项的详细信息，请参阅[扩展 Word 文档和 Excel 工作簿中运行时在 VSTO 加载项](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

### <a name="to-add-a-windows-forms-control-at-runtime"></a>若要在运行时添加 Windows 窗体控件

1. 使用一种方法具有名称外\<*控制类*> (其中*控件类*是想要添加，例如在 Windows 窗体控件的类名<xref:Microsoft.Office.Tools.Word.ControlExtensions.AddButton%2A>)。

    > [!NOTE]
    > 在 VSTO 外接程序项目面向[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]或更高版本，必须添加对的引用*Microsoft.Office.Tools.Excel.v4.0.Utilities.dll*或*Microsoft.Office.Tools.Word.v4.0.Utilities.dll*程序集才能访问外\<*控制类*> 方法。

     下面的代码示例演示了如何通过使用 Word VSTO 外接程序将 <xref:Microsoft.Office.Tools.Word.Controls.Button> 添加到活动文档的第一段。

     [!code-vb[Trin_WordAddInDynamicControls#7](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#7)]
     [!code-csharp[Trin_WordAddInDynamicControls#7](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#7)]

## <a name="see-also"></a>请参阅
- [Windows 窗体控件在 Office 文档概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [如何：调整工作表单元格中的控件的大小](../vsto/how-to-resize-controls-within-worksheet-cells.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
