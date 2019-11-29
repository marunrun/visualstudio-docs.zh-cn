---
title: 创建您的第一个 Excel 文档级自定义项
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, creating your first project
- Excel [Office development in Visual Studio], creating your first project
- document-level customizations [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8d45461c7dab250cd43d7a25d8693658c7b8e164
ms.sourcegitcommit: 3ba2968a4b44643482aadad4d50e1a55bb36b136
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74566981"
---
# <a name="walkthrough-create-your-first-document-level-customization-for-excel"></a>演练：创建您的第一个 Excel 文档级自定义项

  本介绍性演练演示如何创建 Microsoft Office Excel 的文档级自定义项。 仅在特定工作簿处于打开状态时，才可使用你在这种解决方案中创建的功能。 不能使用文档级自定义项进行应用程序范围的更改，例如在任何工作簿处于打开状态时显示新的功能区选项卡。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练阐释了以下任务：

- 创建 Excel 工作簿项目。

- 将文本添加到 Visual Studio 设计器中保存的工作表。

- 编写代码，使用 Excel 对象模型在自定义工作簿处于打开状态时向其中添加文本。

- 生成并运行项目，以对其进行测试。

- 清理已完成的项目，以便从开发计算机删除不必要的生成文件和安全设置。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件

 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)]或[!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目

### <a name="to-create-a-new-excel-workbook-project-in-visual-studio"></a>在 Visual Studio 中创建新的 Excel 工作簿项目

1. 启动[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。
::: moniker range="vs-2017"
3. 在模板窗格中，展开 **“Visual C#”** 或 **“Visual Basic”** ，然后展开 **“Office/SharePoint”** 。

4. 在展开的 " **Office/SharePoint** " 节点下，选择 " **VSTO 外接程序**" 节点。

5. 在项目模板列表中，选择 "Excel VSTO 工作簿" 项目。

6. 在 "**名称**" 框中，键入**FirstWorkbookCustomization**。

7. 单击“确定”。

8. 从 " **Visual Studio Tools for Office 项目向导**" 中选择 "**创建新文档**"，然后单击 **"确定"** 。
::: moniker-end
::: moniker range=">=vs-2019"
3. 在 "**创建新项目**" 对话框中，选择 " **Excel VSTO 工作簿**" 项目。

     [!INCLUDE[new-project-dialog-search](../vsto/includes/new-project-dialog-search-md.md)]

4. 单击 **“下一步”** 。

5. 在 "**配置新项目**" 对话框的 "**名称**" 框中键入**FirstWorkbookCustomization** ，然后单击 "**创建**"。

6. 从 " **Visual Studio Tools for Office 项目向导**" 中选择 "**创建新文档**"，然后单击 **"确定"** 。
::: moniker-end
   - [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建**FirstWorkbookCustomization**项目，并将以下文件添加到项目。

   - *FirstWorkbookCustomization*-表示项目中的 Excel 工作簿。 包含所有工作表和图表。

   - Sheet1 （用于 Visual Basic 的 *.vb*文件或 Visual C#的 .cs 文件）-一个工作表，该工作表提供工作簿中第一个工作表的设计图面和代码。 有关详细信息，请参阅[工作表主机项](../vsto/worksheet-host-item.md)。

   - Sheet2 （用于 Visual Basic 的 *.vb*文件或 Visual C#的 .cs 文件）-一个工作表，该工作表提供工作簿中第二个工作表的设计图面和代码。

   - Sheet3 （用于 Visual Basic 的 *.vb*文件或 Visual C#的 .cs 文件）-一个工作表，该工作表提供工作簿中第三个工作表的设计图面和代码。

   - ThisWorkbook （Visual C#的 Visual Basic 或 *.cs*文件的 *.vb*文件）-包含用于工作簿级自定义项的设计图面和代码。 有关详细信息，请参阅[工作簿主机项](../vsto/workbook-host-item.md)。

     将在设计器中自动打开 Sheet1 代码文件。

## <a name="close-and-reopen-worksheets-in-the-designer"></a>关闭并重新打开设计器中的工作表

 如果开发项目时有意或意外关闭设计器中的工作簿或工作表，可以重新打开它。

### <a name="to-close-and-reopen-a-worksheet-in-the-designer"></a>关闭并重新打开设计器中的工作表

1. 通过单击设计器窗口的 "**关闭**" 按钮（X）来关闭工作簿。

2. 在**解决方案资源管理器**中，右键单击 " **Sheet1** " 代码文件，然后单击 "**视图设计器**"。

     \- 或 -

     在**解决方案资源管理器**中，双击**Sheet1**代码文件。

## <a name="add-text-to-a-worksheet-in-the-designer"></a>向设计器中的工作表添加文本

 可以通过修改已在设计器中打开的工作表来设计自定义项的用户界面 (UI)。 例如，可以将文本添加到单元格、应用公式或添加 Excel 控件。 有关如何使用设计器的详细信息，请参阅[Visual Studio 环境中的 Office 项目](../vsto/office-projects-in-the-visual-studio-environment.md)。

### <a name="to-add-text-to-a-worksheet-by-using-the-designer"></a>使用设计器将文本添加到工作表

1. 在设计器中打开的工作表中，选择单元格**A1**，然后键入以下文本。

     **此文本是使用设计器添加的。**

> [!WARNING]
> 如果将此行文本添加到单元格**A2**，则它将被此示例中的其他代码覆盖。

## <a name="add-text-to-a-worksheet-programmatically"></a>以编程方式向工作表添加文本

 接下来，将代码添加到 Sheet1 代码文件。 新代码使用 Excel 对象模型向工作簿添加第二行文本。 默认情况下，Sheet1 代码文件包含以下生成代码：

- `Sheet1` 类的分部定义，用于表示工作表的编程模型，并提供对 Excel 对象模型的访问权限。 有关详细信息，请参见[工作表主机项](../vsto/worksheet-host-item.md)和[Word 对象模型概述](../vsto/word-object-model-overview.md)。 `Sheet1` 类的其余部分是在隐藏代码文件中定义的，不应修改该代码文件。

- `Sheet1_Startup` 和 `Sheet1_Shutdown` 事件处理程序。 Excel 加载和卸载自定义项时会调用这些事件处理程序。 使用这些事件处理程序，可在加载自定义项对其进行初始化，并在卸载时清理自定义项所使用的资源。 有关详细信息，请参阅[Office 项目中的事件](../vsto/events-in-office-projects.md)。

### <a name="to-add-a-second-line-of-text-to-the-worksheet-by-using-code"></a>使用代码向工作表添加第二行文本

1. 在**解决方案资源管理器**中，右键单击**Sheet1**，然后单击 "**查看代码**"。

     将在 Visual Studio 中打开代码文件。

2. 将 `Sheet1_Startup` 事件处理程序替换为以下代码。 当打开 Sheet1 时，此代码将向工作表添加第二行文本。

     [!code-csharp[Trin_ExcelWorkbookTutorial#1](../vsto/codesnippet/CSharp/Trin_ExcelWorkbookTutorial/Sheet1.cs#1)]
     [!code-vb[Trin_ExcelWorkbookTutorial#1](../vsto/codesnippet/VisualBasic/Trin_ExcelWorkbookTutorial/Sheet1.vb#1)]

## <a name="test-the-project"></a>测试项目

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按 **F5** 生成并运行项目。

     生成项目时，会将代码编译到与该工作簿相关联的程序集中。 Visual Studio 将该工作簿和程序集的副本放入项目的生成输出文件夹中，并将开发计算机上的安全设置配置为允许自定义项运行。 有关详细信息，请参阅[生成 Office 解决方案](../vsto/building-office-solutions.md)。

2. 验证工作簿中显示以下文本。

     **此文本是使用设计器添加的。**

     **This text was added by using code.**

3. 关闭工作簿。

## <a name="clean-up-the-project"></a>清理项目

 完成项目开发后，应删除生成输出文件夹中的文件和由生成过程创建的安全设置。

### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>在开发计算机上清理已完成的项目

1. 在 Visual Studio 中，在 **“生成”** 菜单上，单击 **“清理解决方案”** 。

## <a name="next-steps"></a>后续步骤

 既然你已经创建了一个基本的 Excel 文档级自定义项，就可以从下面这些主题中了解有关如何开发自定义项的详细信息：

- 可以在文档级自定义项中执行的常规编程任务：[程序文档级自定义项](../vsto/programming-document-level-customizations.md)。

- 特定于 Excel 的文档级自定义项的编程任务： [excel 解决方案](../vsto/excel-solutions.md)。

- 使用 Excel 的对象模型： [excel 对象模型概述](../vsto/excel-object-model-overview.md)。

- 自定义 Excel 的 UI，例如通过向功能区添加自定义选项卡或创建自己的操作窗格： [OFFICE UI 自定义](../vsto/office-ui-customization.md)。

- 使用 Visual Studio 中的 Office 开发工具提供的扩展 Excel 对象来执行不能使用 Excel 对象模型的任务（例如，在文档上承载托管控件，并使用 Windows 窗体数据绑定模型将 Excel 控件绑定到数据）：[使用扩展对象实现 Excel 自动化](../vsto/automating-excel-by-using-extended-objects.md)。

- 生成和调试 Excel 文档级自定义项：[生成 Office 解决方案](../vsto/building-office-solutions.md)。

- 部署 Excel 的文档级自定义项：[部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>另请参阅

- [Office 解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [Excel 解决方案](../vsto/excel-solutions.md)
- [程序文档级自定义项](../vsto/programming-document-level-customizations.md)
- [Excel 对象模型概述](../vsto/excel-object-model-overview.md)
- [使用扩展对象实现 Excel 自动化](../vsto/automating-excel-by-using-extended-objects.md)
- [Office UI 自定义](../vsto/office-ui-customization.md)
- [构建 Office 解决方案](../vsto/building-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [Office 项目模板概述](../vsto/office-project-templates-overview.md)
