---
title: 在 Visual Studio 环境中的 office 项目
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.WordDocument
- VST.ProjectItem.ExcelWorkbook
- VST.ProjectItem.ExcelTemplate
- VST.ProjectItem.ExcelSheet
- VST.ProjectItem.BlueprintCode
- VST.ProjectItem.Word
- VST.ProjectItem.Excel
- VST.ProjectItem.AddinProject
- Designer_Microsoft.VisualStudio.OfficeTools.Excel.Design.WorksheetDesigner
- VST.ProjectItem.ExtendedBluePrint
- VST.ProjectItem.WordTemplate
- Designer_Microsoft.VisualStudio.OfficeTools.Word.Design.DocumentDesigner
- VST.Designer.ExcelVST.Designer.Word
- VST.ProjectItem.ExtendedBlueprintCode
- VST.ProjectItem.BluePrint
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio]
- hidden files [Office development in Visual Studio]
- project files [Office development in Visual Studio], hidden
- Office development in Visual Studio, documents in Visual Studio
- design view, Excel
- designers, Office development in Visual Studio
- Office documents [Office development in Visual Studio]
- Office documents [Office development in Visual Studio], about documents in Visual Studio
- designers [Office development in Visual Studio]
- Word designer
- Word [Office development in Visual Studio], Word designer
- Visual Studio, Office documents in
- worksheets [Office development in Visual Studio]
- VST.Designer.ExcelVST.Designer.Word
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 65f3a3abfe7e49872c7131a247d74612200bf42a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978053"
---
# <a name="office-projects-in-the-visual-studio-environment"></a>在 Visual Studio 环境中的 office 项目
  Microsoft Office 项目的开发体验与 Visual Studio 中其他类型的项目（如 Windows 窗体项目）相似。 当你创建或打开 Office 项目时，项目项会出现在 **“解决方案资源管理器”** 中。 对于文档级项目，文档（即 Word 文档或 Excel 工作簿）将在 Visual Studio 中打开，该文档的行为就如同一个可视化设计器。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="project-items-in-solution-explorer"></a>在解决方案资源管理器中的项目项
 在文档级项目中， **“解决方案资源管理器”** 显示下列默认项：

- 由项目自定义的文档、工作簿和表的节点。 这些节点用作与文档、工作簿和表相关联的代码文件的容器。

- 与由项目自定义的文档、工作簿和表相关联的代码文件。 在 Word 项目中，代码文件与 Word 文档或模板相关联。 在 Excel 项目中，代码文件与 Excel 工作簿或模板相关联，并与工作簿或模板中的每个工作表和图表工作表相关联。

- 你不打算直接编辑的隐藏项目文件。 有关详细信息，请参阅[隐藏项目文件](#hiddenfiles)。

  在 VSTO 外接程序项目中，“解决方案资源管理器”  显示下列默认项：

- 应用程序节点。 此节点的名称与宿主应用程序相同，例如 **“Word”**、 **“Excel”** 或 **“Outlook”**。 应用程序节点包含 ThisAddIn 代码文件。 它还提供 **“宿主项的命名空间”** 属性。 有关此属性的详细信息，请参阅[Office 项目中的属性](../vsto/properties-in-office-projects.md)。

- ThisAddIn 代码文件。 此文件包含 VSTO 外接程序的 `ThisAddIn` 生成类。 有关此类的详细信息，请参阅[程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

- 你不打算直接编辑的隐藏项目文件。 有关详细信息，请参阅[隐藏项目文件](#hiddenfiles)。

### <a name="temporary-certificates"></a>临时证书
 Office 项目还包括名为 *Project Name*_TemporaryKey.pfx 的临时证书。 此证书用于在开发期间对项目的应用程序和部署清单进行签名。 有关详细信息，请参阅[向 Office 解决方案授予信任](../vsto/granting-trust-to-office-solutions.md)并[保护 Office 解决方案](../vsto/securing-office-solutions.md)。

### <a name="hiddenfiles"></a> 隐藏的项目文件
 默认情况下，某些项目文件是隐藏的。 这些文件由 Visual Studio 生成，它们因项目类型而异。 若要显示隐藏文件，请在 **“解决方案资源管理器”** 中，单击 **“显示所有文件”**。

 不要修改隐藏项目文件。 不支持直接更改这些文件，否则可能损坏你的项目。 每当文档中发生某些更改时，就会重新生成隐藏的项目文件。 如果你对隐藏的项目文件进行手动更改，这些更改将在下次文件重新生成时丢失。

## <a name="document-designer-in-document-level-projects"></a>在文档级项目中的文档设计器
 Excel 和 Word 的文档级项目提供一个设计器，该设计器承载与 Visual Studio 中的项目相关联的文档。 设计器使你可以在不必离开 Visual Studio 环境的情况下修改文档。

 若要在设计器中打开文档，请在 **“解决方案资源管理器”** 中双击与该文档相关联的代码文件。 例如，若要在 Excel 项目的设计器中打开工作表 **Sheet1** ，请双击 **Sheet1** 代码文件。

 在设计器中修改文档时，可以利用 Office 应用程序的原有功能。 例如，可以在文档或工作表中键入文本，也可以使用功能区执行诸如添加表格或图表之类的任务。 默认情况下，键盘快捷键映射默认为 Visual Studio 映射。 若要转而使用 Office 键盘快捷键映射，请更改 **“工具”** 菜单上 **“选项”** 对话框中 **“Microsoft Office 键盘设置”** 节点下的设置。

### <a name="controls-on-documents"></a>文档中的控件
 可以将宿主控件  和 Windows 窗体控件从 Visual Studio **“工具箱”** 拖到文档设计图面上。 宿主控件是可用于通过 Visual Studio 创建的 Office 项目的特殊版本的 Office 对象，例如 Word 内容控件和 Excel 范围。 宿主控件具有在对应 Office 对象中不可用的附加功能，例如数据绑定和附加事件。

 有关详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)并[Windows 窗体控件在 Office 文档概述](../vsto/windows-forms-controls-on-office-documents-overview.md)。

### <a name="excel-worksheets-and-workbooks-in-the-designer"></a>Excel 工作表和设计器中的工作簿
 当在设计器中打开工作表时，可以采用与在 Excel 中直接打开进行修改的相同方式来修改工作表。 当双击工作表单元格时，该单元格将切换到编辑模式。 如果您双击包含宿主控件的单元格，此时会打开代码编辑器和 Visual Studio 生成控件的默认事件处理程序。 若要导航到其他工作表，可以在设计器底部单击工作表选项卡。

 当在设计器中打开工作簿时，并没有设计图面。 工作簿的设计视图是填充设计器的大型组件栏。

 工作簿和工作簿中的每个工作表都有相关联的代码文件。 每个代码文件包含一个已生成的代表工作簿或工作表的宿主项  类。 有关详细信息，请参阅[通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)。

### <a name="word-documents-in-the-designer"></a>在设计器中的 Word 文档
 当在设计器中打开文档时，可以采用与在 Word 中直接打开进行修改的相同方式来修改文档。 如果双击文档中的一个单词时，将选中该单词。 但是，如果该单词位于宿主控件内部，便会打开代码编辑器，Visual Studio 生成控件的默认事件处理程序。

 文档具有关联的代码文件。 代码文件包含一个已生成的代表文档的宿主项  类。 有关详细信息，请参阅[文档宿主项](../vsto/document-host-item.md)。

### <a name="design-mode-vs-runtime-mode"></a>与运行时模式下的设计模式
 当文档在 Visual Studio 环境中打开时，它始终处于设计模式 。 某些任务（例如将宿主控件拖动到文档图面）只能在设计模式下执行。

 若要查看的文档中*运行时模式*，则必须打开该应用程序和 Visual Studio 外部文档。 也可以生成并运行项目，这样便会在 Visual Studio 外自动打开文档和应用程序。

## <a name="code-editor"></a>代码编辑器
 通过代码编辑器，可以查看和修改解决方案中的可见代码文件。 这些文件包含定义解决方案行为的代码。

 有关代码编辑器中的详细信息，请参阅[代码和文本编辑器中编写代码](../ide/writing-code-in-the-code-and-text-editor.md)。 有关如何在 Office 项目中编写代码的详细信息，请参阅[在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)。

## <a name="properties-window"></a>“属性”窗口
 **“属性”** 窗口显示 **“解决方案资源管理器”** 中选择的项目项的属性，以及设计器中选择的 UI 元素的属性，具体如文档级项目中的控件或文档的属性。 有些属性是特定于应用程序和文档的，而有些属性则是所有项目共有的。

## <a name="data-sources-window"></a>“数据源”窗口
 可以在文档级 Office 项目中使用 **“数据源”** 窗口将数据源拖到文档上，以及创建绑定到数据源的控件。 有关详细信息，请参阅[将控件绑定到 Visual Studio 中的数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。

## <a name="see-also"></a>请参阅

- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [Office 项目模板概述](../vsto/office-project-templates-overview.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Office 项目中的属性](../vsto/properties-in-office-projects.md)
