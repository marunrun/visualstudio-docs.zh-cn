---
title: Office 文档上的 Windows 窗体控件的限制
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
ms.openlocfilehash: d5cb4bf5788e1d30933a807e2e97e064118fc076
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67823409"
---
# <a name="limitations-of-windows-forms-controls-on-office-documents"></a>Office 文档上的 Windows 窗体控件的限制

没有添加到 Microsoft Office Word 文档或 Microsoft Office Excel 工作表的 Windows 窗体控件和 Windows 窗体控件添加到 Windows 窗体之间的一些差异。 例如，添加<xref:Microsoft.Office.Tools.Word.Controls.Button>控制到文档中，属性，例如<xref:System.Windows.Forms.Control.Dock>， <xref:System.Windows.Forms.Control.Anchor>，和<xref:System.Windows.Forms.Control.TabIndex>不像您所料。

其中许多差异导致顺便提一下控件位于该 Windows 窗体上的文档。 当 Windows 窗体控件添加到文档，[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]嵌入然后承载 Windows 窗体控件在文档中的 ActiveX 控件。 在 Windows 窗体控件不嵌入在文档中直接。

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="limitations-of-methods-and-properties-of-windows-forms-controls"></a>Windows 窗体控件的方法和属性的限制

有多种方法和不起作用的相同的方式对文档以及它们会在 Windows 窗体上，因此，建议它们无法在使用 Windows 窗体控件的属性。 例如，如设置属性<xref:System.Windows.Forms.Control.Dock>和<xref:System.Windows.Forms.Control.Anchor>仅影响将控件与容器 ActiveX 控件，而不是文档的位置。 下面是不支持的方法和 Word 和 Excel 的 Windows 窗体控件的属性的列表：

- 不支持的 Excel 控件的属性：

  - <xref:System.Windows.Forms.Control.Anchor>
  - <xref:System.Windows.Forms.Control.Dock>
  - <xref:System.Windows.Forms.Control.Location>
  - <xref:System.Windows.Forms.Control.TabIndex>
  - <xref:System.Windows.Forms.Control.TabStop>
  - <xref:System.Windows.Forms.Control.TopLevelControl>

- 不受支持的方法和属性的 Word 控件：

  - <xref:System.Windows.Forms.Control.Hide%2A>
  - <xref:System.Windows.Forms.Control.Show%2A>
  - <xref:System.Windows.Forms.Control.Anchor>
  - <xref:System.Windows.Forms.Control.Dock>
  - <xref:System.Windows.Forms.Control.Location>
  - <xref:System.Windows.Forms.Control.TabIndex>
  - <xref:System.Windows.Forms.Control.TabStop>
  - <xref:System.Windows.Forms.Control.TopLevelControl>
  - <xref:System.Windows.Forms.Control.Visible>

您还不能设置<xref:System.Windows.Forms.Control.Left>或<xref:System.Windows.Forms.Control.Top>与 Word 文档的文本对齐的 Windows 窗体控件的属性。 添加 Windows 窗体控件，与在以下情况下的文本对齐：

- 可以以编程方式向 Word 文档添加控件，并使用指定的位置的范围的方法。

- 在设计时向 Word 文档添加 Windows 窗体控件。 可以通过修改控件在设计器中的对此进行更改。

## <a name="differences-in-windows-forms-controls-on-office-documents"></a>Office 文档上的 Windows 窗体控件之间的差异

Windows 窗体控件通常具有相同的行为上的 Office 文档上 Windows 窗体，但也存在一些差异。 下表描述了 Office 文档上的 Windows 窗体控件存在的差异。

|功能|差值|
|-------------------|----------------|
|控件 tab 键顺序|您不能通过在 Excel 工作表或 Word 文档上放置的控件选项卡。|
|控件分组|不能使用<xref:System.Windows.Forms.GroupBox>控件，以包含 Office 文档上的其他控件。 直接向文档添加多个单选按钮的单选按钮是不互相排斥。 可以编写代码以使单选按钮相互排斥;但是，首选的方法是向用户控件添加单选按钮，然后将用户控件添加到文档。 有关详细信息，请参阅的 Word 控件示例或 Excel 控件示例[Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)。|
|控件类型|使用文档上的 Windows 窗体控件包装在提供的一类[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]，使得的控件特定的其他功能的 Excel 工作表或 Word 文档。 例如，如果你有**按钮**对 Excel 工作表的 control 权限，请确保将类型指定为<xref:Microsoft.Office.Tools.Excel.Controls.Button>而非<xref:System.Windows.Forms.Button>时引用或将对象强制转换。|
|控件位置和大小|由属于容器 ActiveX 控件的属性确定的大小和位置的控件。 ActiveX 控件属性采用比等效的 Windows 窗体控件的属性的不同值。 当您将设置`Top`， `Left`， `Height`，或`Width`控件的属性，它用来衡量中点，而不是像素为单位。|
|在 Word 文档上的控件位置|如果将控件添加到基于流的布局，请记住，控件将随内容流动内容发生变化。 您不能将控件锚定到段落时将其从**工具箱**因为该控件添加到 Word 文档与文本对齐。 如果使用另一种方法来添加控件，如双击该控件，根据您已为插入图片设置单词选项插入控件。<br /><br /> 不能设置`Left`或`Top`是嵌入文字控件的属性。<br /><br /> 无法将控件放在页眉或页脚，还是在一个子文档。|
|控件事件|选中控件后，它会引发事件按以下顺序：<br /><br /> 1.  `Enter`<br />2.  `GotFocus`<br /><br /> 取消选择该控件，则它会引发事件按以下顺序：<br /><br /> 1.  `Leave`<br />2.  `Validating`<br />3.  `Validated`<br />4.  `LostFocus`|
|缩放控件|当为 100%以外的任何更改文档的缩放设置时，将禁用控件，尽管它们会对显示与文档一起缩放。 例如，如果您的文档位于 130%缩放时，单击一个按钮，它将显示一条消息已在控件被禁用，直到缩放设置为 100%。 将缩放比例更改为 100%时，控件将正常工作。|
|控件的属性值|尽管 Windows 窗体上控件的属性设置为一个整数值，它们将设置为单个 Word 文档上的控件。 在 Excel 中，控件的属性值设置为一个双精度值。 如果`Height`和`Width`工作表上控件的属性超过了工作表或屏幕的大小，将截断的值。|
|控件的大小调整|如果在调整大小的文档使用八个大小调整句柄之一上的控件中, 不会反映新的控件尺寸**属性**窗口后，才能看到该控件。|
|控制行为|拆分工作表窗口时，Excel 工作表上的控件可能行为异常。 例如，访问<xref:Microsoft.Office.Tools.Excel.Controls.TextBox>工作表上可能仅可在一个窗口中。|
|控制命名|不能使用保留的字来命名控件。 例如，如果您将添加<xref:Microsoft.Office.Tools.Excel.Controls.Button>到工作表并将名称更改为**系统**，生成项目时出现错误。|
|以编程方式添加控件|不使用控件的构造函数以将控件添加到你在运行时的文档。 请改用提供的帮助器方法[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。 例如，使用<xref:Microsoft.Office.Tools.Excel.ControlExtensions.AddButton%2A>方法向工作表中添加一个按钮。 如果你想要添加这些帮助器方法不支持的控件，则可以使用`AddControl`方法。 有关详细信息，请参阅[在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。|
|复制控件|如果将 Windows 窗体控件复制并粘贴到文档中在运行时，空容器 ActiveX 控件将粘贴到文档。 Windows 窗体控件不会出现在新的位置，并且代码隐藏原始控件不会复制到 ActiveX 控件的容器。|

## <a name="limitations-in-document-level-projects"></a>文档级项目中的限制

使用文档上的 Windows 窗体控件的某些限制是唯一的文档级项目。

### <a name="control-support-at-design-time"></a>在设计时控件支持

某些 Windows 窗体控件都将从中**工具箱**Excel 工作表或 Word 文档时在 Visual Studio 设计器中打开。 这是由于技术限制或因为功能已在 Word 或 Excel 内可用。 Excel 和 Word 项目支持的所有 Windows 窗体控件和其他组件中出现**工具箱**当文档具有焦点，而且还可以将第三方控件添加到工作表或文档。

> [!NOTE]
> 所有控件都将都从中**工具箱**受保护文档时。 文档保护有关的信息，请参阅[文档在文档级解决方案中的保护](../vsto/document-protection-in-document-level-solutions.md)。

> [!NOTE]
> 第三方控件都必须有<xref:System.Runtime.InteropServices.ComVisibleAttribute>属性设置为**true**若要在 Office 解决方案中使用。

以下控件和组件中不可**工具箱**:

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

### <a name="support-for-legacy-activex-controls"></a>旧式 ActiveX 控件的支持

如果创建使用现有的 Word 文档或 Excel 工作簿包含 ActiveX 控件的文档级 Office 项目时，ActiveX 控件的功能不会丢失;但是，不是支持将新的 ActiveX 控件添加到您从 Visual Studio 中的文档。 例如，如果您的 Word 文档都有一个按钮从**控制**工具箱中运行 Visual Basic Applications (VBA) 宏，它将继续运行宏，Office 项目中使用了文档之后。 但是，建议删除 ActiveX 控件和 VBA 宏并将它们替换为 Windows 窗体控件和托管代码。

## <a name="see-also"></a>请参阅

- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [Windows 窗体控件在 Office 文档概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [在运行时向 Office 文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
