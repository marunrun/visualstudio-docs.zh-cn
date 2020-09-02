---
title: Office 文档 Windows 窗体控件的限制
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], ActiveX legacy
- ActiveX controls [Office development in Visual Studio]
- Windows Forms controls [Office development in Visual Studio], limitations
- controls [Office development in Visual Studio], Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], unsupported properties and methods
- Toolbox [Office development in Visual Studio], unsupported controls
- user controls [Office development in Visual Studio], grouping controls
- Windows Forms controls [Office development in Visual Studio], Toolbox
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 81a7da585f49b2a2d1f7df4df11d0c78b7a35d69
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "71251917"
---
# <a name="limitations-of-windows-forms-controls-on-office-documents"></a>Office 文档 Windows 窗体控件的限制

添加到 Microsoft Office Word 文档或 Microsoft Office Excel 工作表的 Windows 窗体控件与添加到 Windows 窗体的 Windows 窗体控件之间存在一些差异。 例如，将 <xref:Microsoft.Office.Tools.Word.Controls.Button> 控件添加到文档时，属性（例如 <xref:System.Windows.Forms.Control.Dock> 、 <xref:System.Windows.Forms.Control.Anchor> 和） <xref:System.Windows.Forms.Control.TabIndex> 不会像预期那样工作。

其中许多差异是由 Windows 窗体控件在文档上的宿主方式导致的。 将 Windows 窗体控件添加到文档中时，会将 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 一个 ActiveX Windows 窗体控件嵌入到文档中。 Windows 窗体控件不会直接嵌入到文档中。

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="limitations-of-methods-and-properties-of-windows-forms-controls"></a>Windows 窗体控件的方法和属性的限制

Windows 窗体控件有很多方法和属性，这些方法和属性在文档中的使用方式与在 Windows 窗体上的工作方式相同，因此建议不要使用这些方法和属性。 例如，设置属性（如 <xref:System.Windows.Forms.Control.Dock> 和） <xref:System.Windows.Forms.Control.Anchor> 只会影响控件对于容器 ActiveX 控件的位置，而不影响文档的位置。 下面列出了 Word 和 Excel Windows 窗体控件的不受支持的方法和属性：

- 不支持 Excel 控件的属性：

  - <xref:System.Windows.Forms.Control.Anchor>
  - <xref:System.Windows.Forms.Control.Dock>
  - <xref:System.Windows.Forms.Control.Location>
  - <xref:System.Windows.Forms.Control.TabIndex>
  - <xref:System.Windows.Forms.Control.TabStop>
  - <xref:System.Windows.Forms.Control.TopLevelControl>

- Word 控件的方法和属性不受支持：

  - <xref:System.Windows.Forms.Control.Hide%2A>
  - <xref:System.Windows.Forms.Control.Show%2A>
  - <xref:System.Windows.Forms.Control.Anchor>
  - <xref:System.Windows.Forms.Control.Dock>
  - <xref:System.Windows.Forms.Control.Location>
  - <xref:System.Windows.Forms.Control.TabIndex>
  - <xref:System.Windows.Forms.Control.TabStop>
  - <xref:System.Windows.Forms.Control.TopLevelControl>
  - <xref:System.Windows.Forms.Control.Visible>

还不能设置 <xref:System.Windows.Forms.Control.Left> <xref:System.Windows.Forms.Control.Top> Word 文档中包含文本的 Windows 窗体控件的或属性。 在以下情况下，将在文本行中添加 Windows 窗体控件：

- 以编程方式将控件添加到 Word 文档，并使用指定位置范围的方法。

- 在设计时向 Word 文档添加 Windows 窗体控件。 可以通过修改设计器中的控件来更改此项。

## <a name="differences-in-windows-forms-controls-on-office-documents"></a>Office 文档 Windows 窗体控件之间的差异

Windows 窗体控件在 Office 文档中的行为通常与 Windows 窗体上的行为相同，但存在一些差异。 下表描述了 Office 文档上 Windows 窗体控件存在的差异。

|功能|差异|
|-------------------|----------------|
|控件 tab 键顺序|不能通过 tab 键将控件放置在 Excel 工作表或 Word 文档中。|
|控件分组|不能使用 <xref:System.Windows.Forms.GroupBox> 控件在 Office 文档上包含其他控件。 当您将多个单选按钮直接添加到文档时，单选按钮并不是互相排斥的。 你可以编写代码以使单选按钮互斥;但是，首选方法是将单选按钮添加到用户控件，然后将该用户控件添加到文档中。 有关详细信息，请参阅 [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)中的 Word 控件示例或 Excel 控件示例。|
|控件类型|文档上使用的 Windows 窗体控件包装在由提供的类中 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ，该类为控件提供特定于 Excel 工作表或 Word 文档的附加功能。 例如，如果在 Excel 工作表上有一个 " **按钮** " 控件，请确保指定类型， <xref:Microsoft.Office.Tools.Excel.Controls.Button> 而不是 <xref:System.Windows.Forms.Button> 引用或强制转换对象。|
|控件位置和大小|控件的大小和位置由容器 ActiveX 控件中的属性确定。 ActiveX 控件属性采用与 Windows 窗体控件的等效属性不同的值。 当您设置 `Top` 控件的、 `Left` 、或属性时， `Height` `Width` 它将以磅而不是像素来度量。|
|控件在 Word 文档上的位置|如果将控件添加到基于流的布局中，请记住，当内容更改时，控件将与内容一起流动。 将控件从 " **工具箱** " 中拖动时，不能将其定位到某个段落，因为该控件已与文本一起添加到 Word 文档中。 如果使用另一种方法添加控件，如双击控件，则将根据为插入图片而设置的单词选项插入控件。<br /><br /> 不能设置 `Left` `Top` 与文本内联的控件的或属性。<br /><br /> 不能将控件放置在页眉或页脚中或子文档中。|
|控件事件|选择该控件后，它将按以下顺序引发事件：<br /><br /> 2.  `Enter`<br />pps-2.  `GotFocus`<br /><br /> 取消选择控件后，它将按以下顺序引发事件：<br /><br /> 2.  `Leave`<br />pps-2.  `Validating`<br />三维空间.  `Validated`<br />4.  `LostFocus`|
|控件缩放|如果将文档的缩放设置更改为100% 之外的任何内容，则会禁用控件，尽管它们看上去与文档一起缩放。 例如，如果您在文档处于130% 缩放时单击按钮，则它将显示一条消息，指示该控件已被禁用，直到 "缩放" 设置为100%。 将缩放更改为100% 时，控件将正常运行。|
|控件属性值|尽管 Windows 窗体上控件的属性设置为一个整数值，但对于 Word 文档中的控件，它们设置为单一。 在 Excel 中，将控件的属性值设置为双精度值。 如果 `Height` `Width` 工作表上的控件的和属性超出了工作表或屏幕的大小，则该值将被截断。|
|控件调整大小|如果使用八个大小调整控点之一调整文档上的控件大小，则在控件只有之前，新的控件尺寸不会反映在 " **属性** " 窗口中。|
|控制行为|拆分工作表窗口时，Excel 工作表上的控件的行为可能无法预测。 例如，对 <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> 工作表上的的访问可能只在一个窗口中可用。|
|控件命名|不能使用保留字来命名控件。 例如，如果将添加 <xref:Microsoft.Office.Tools.Excel.Controls.Button> 到工作表中并将名称更改为 **System**，生成项目时将发生错误。|
|以编程方式添加控件|不要使用控件的构造函数在运行时向文档添加控件。 相反，请使用提供的帮助器方法 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 例如，使用 <xref:Microsoft.Office.Tools.Excel.ControlExtensions.AddButton%2A> 方法将按钮添加到工作表。 如果要添加这些帮助器方法不支持的控件，可以使用 `AddControl` 方法。 有关详细信息，请参阅 [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。|
|复制控件|如果复制 Windows 窗体控件并在运行时将其粘贴到文档中，则会将空容器 ActiveX 控件粘贴到文档中。 Windows 窗体控件不会出现在新位置，并且原始控件的隐藏代码不会复制到容器 ActiveX 控件。|

## <a name="limitations-in-document-level-projects"></a>文档级项目中的限制

对文档使用 Windows 窗体控件的某些限制对于文档级项目是唯一的。

### <a name="control-support-at-design-time"></a>设计时的控件支持

当 Excel 工作表或 Word 文档在 Visual Studio 设计器中打开时，某些 Windows 窗体控件将从 **工具箱** 中移除。 这是因为技术限制或功能已在 Word 或 Excel 中可用。 Excel 和 Word 项目支持在文档具有焦点时在 **工具箱** 中显示的所有 Windows 窗体控件和其他组件，也可以将第三方控件添加到工作表或文档中。

> [!NOTE]
> 文档受到保护时，将从 **工具箱** 中删除所有控件。 有关文档保护的信息，请参阅文档 [级解决方案中的文档保护](../vsto/document-protection-in-document-level-solutions.md)。

> [!NOTE]
> 第三方控件必须将 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性设置为 **true** ，才能在 Office 解决方案中使用。

**工具箱**中没有以下控件和组件：

- <xref:System.Windows.Forms.BindingNavigator>

- <xref:System.Windows.Forms.ContextMenuStrip>

- <xref:System.Windows.Forms.DataGrid>

- <xref:System.DirectoryServices.DirectoryEntry>

- <xref:System.DirectoryServices.DirectorySearcher>

- <xref:System.Windows.Forms.ErrorProvider>

- <xref:System.Diagnostics.EventLog>

- <xref:System.IO.FileSystemWatcher>

- <xref:System.Windows.Forms.FlowLayoutPanel>

- <xref:System.Windows.Forms.GroupBox>

- <xref:System.Windows.Forms.MainMenu>

- <xref:System.Windows.Forms.MenuStrip>

- <xref:System.Messaging.MessageQueue>

- <xref:System.Windows.Forms.NotifyIcon>

- <xref:System.Windows.Forms.PageSetupDialog>

- <xref:System.Windows.Forms.Panel>

- <xref:System.Diagnostics.PerformanceCounter>

- <xref:System.Windows.Forms.PrintDialog>

- <xref:System.Drawing.Printing.PrintDocument>

- <xref:System.Windows.Forms.PrintPreviewControl>

- <xref:System.Diagnostics.Process>

- <xref:System.Windows.Forms.RichTextBox>

- <xref:System.IO.Ports.SerialPort>

- <xref:System.ServiceProcess.ServiceController>

- <xref:System.Windows.Forms.SplitContainer>

- <xref:System.Windows.Forms.Splitter>

- <xref:System.Windows.Forms.StatusBar>

- <xref:System.Windows.Forms.StatusStrip>

- <xref:System.Windows.Forms.TabControl>

- <xref:System.Windows.Forms.TableLayoutPanel>

- <xref:System.Timers.Timer>

- <xref:System.Windows.Forms.Timer>

- <xref:System.Windows.Forms.ToolBar>

- <xref:System.Windows.Forms.ToolStrip>

- <xref:System.Windows.Forms.ToolStripContainer>

- <xref:System.Windows.Forms.ToolStripDropDown>

- <xref:System.Windows.Forms.ToolStripDropDownMenu>

- <xref:System.Windows.Forms.ToolStripPanel>

### <a name="support-for-legacy-activex-controls"></a>支持旧版 ActiveX 控件

如果创建的文档级 Office 项目使用的是包含 ActiveX 控件的现有 Word 文档或 Excel 工作簿，则 ActiveX 控件的功能不会丢失;但是，不支持从 Visual Studio 中向文档添加新的 ActiveX 控件。 例如，如果 Word 文档的 " **控件** 工具箱" 中有一个按钮，该按钮运行 (VBA) 宏的 Visual Basic for Applications，则在 Office 项目中使用该文档后，该文档将继续运行该宏。 但是，建议删除 ActiveX 控件和 VBA 宏，并将其替换为 Windows 窗体控件和托管代码。

## <a name="see-also"></a>另请参阅

- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [Office 文档上的 Windows 窗体控件概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
