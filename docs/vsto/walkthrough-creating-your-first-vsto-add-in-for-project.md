---
title: 演练：创建你的第一个 Project VSTO 外接程序
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- Project [Office development in Visual Studio], creating your first project
- add-ins [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4a84d295a47d3391f27e7101ad815dca0c910aa6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62981384"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-project"></a>演练：创建你的第一个 Project VSTO 外接程序
  本演练演示如何为 Microsoft Office 项目创建 VSTO 外接程序。 你在此类解决方案中创建的功能可用于应用程序本身，而与所打开的项目无关。 有关详细信息，请参阅 [Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)。

 [!INCLUDE[appliesto_projallapp](../vsto/includes/appliesto-projallapp-md.md)]

 本演练演示以下任务：

- 创建 Project VSTO 外接程序项目。

- 编写使用 Project 的对象模型以向新项目添加任务的代码。

- 生成并运行项目，以对其进行测试。

- 清理已完成的项目，使 VSTO 外接程序在开发计算机上不再自动运行。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Project_15_short](../vsto/includes/project-15-short-md.md)] 或 [!INCLUDE[Project_14_short](../vsto/includes/project-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目

### <a name="to-create-a-new-project-in-visual-studio"></a>若要在 Visual Studio 中创建新项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，再单击 **“项目”** 。

3. 在模板窗格中，展开 **“Visual C#”** 或 **“Visual Basic”**，然后展开 **“Office/SharePoint”**。

4. 在展开的 **“Office/SharePoint”** 节点下方，选择 **“Office 外接程序”** 节点。

5. 在项目模板列表中，选择 **“Project 2010 外接程序”** 或 **“Project 2013 外接程序”**。

6. 在 **“名称”** 框中，键入 **FirstProjectAddIn**。

7. 单击" **确定**"。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建 **FirstProjectAddIn** 项目，并在编辑器中打开 **ThisAddIn** 代码文件。

## <a name="write-code-that-adds-a-new-task-to-a-project"></a>编写向项目添加新任务的代码
 接下来，将代码添加到 ThisAddIn 代码文件。 新代码使用 Project 的对象模型向项目添加新任务。 默认情况下，ThisAddIn 代码文件包含以下生成的代码：

- `ThisAddIn` 类的部分定义。 此类提供代码的入口点，并提供对 Project 对象模型的访问权限。 有关详细信息，请参阅 [PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。类的其余部分 `ThisAddIn` 是在不应修改的隐藏代码文件中定义的。

- `ThisAddIn_Startup` 和 `ThisAddIn_Shutdown` 事件处理程序。 Project 加载和卸载 VSTO 外接程序时会调用这些事件处理程序。 使用这些事件处理程序，可在加载 VSTO 外接程序对其进行初始化，并在卸载 VSTO 外接程序时清理其使用的资源。 有关详细信息，请参阅 [Office 项目中的事件](../vsto/events-in-office-projects.md)。

### <a name="to-add-a-task-to-a-new-project"></a>若要向新的项目中添加任务

1. 在 ThisAddIn 代码文件中，将下面的代码添加到 `ThisAddIn` 类中。 此代码定义了 `Microsoft.Office.Interop.MSProject.Application` 类的 `NewProject` 事件的一个事件处理程序。

    当用户创建一个新项目时，此事件处理程序会向项目添加任务。

    [!code-vb[Trin_ProjectAddInTutorial#1](../vsto/codesnippet/VisualBasic/Trin_ProjectAddInTutorial/ThisAddIn.vb#1)]
    [!code-csharp[Trin_ProjectAddInTutorial#1](../vsto/codesnippet/CSharp/Trin_ProjectAddInTutorial/ThisAddIn.cs#1)]

   为了修改该项目，此代码示例使用了以下对象：

- `Application` 类的 `ThisAddIn` 字段。 `Application` 字段返回一个 `Microsoft.Office.Interop.MSProject.Application` 对象，该对象表示 Project 的当前实例。

- `pj`NewProject 事件的事件处理程序的参数。 `pj` 参数是一个 `Microsoft.Office.Interop.MSProject.Project` 对象，用于表示该项目。 有关详细信息，请参阅 [项目解决方案](../vsto/project-solutions.md)。

1. 如果你使用的是 C#，请将以下代码添加到 `ThisAddIn_Startup` 事件处理程序中。 此代码将 `Application_Newproject` 事件处理程序与 NewProject 事件连接。

     [!code-csharp[Trin_ProjectAddInTutorial#2](../vsto/codesnippet/CSharp/Trin_ProjectAddInTutorial/ThisAddIn.cs#2)]

## <a name="test-the-project"></a>测试项目
 生成和运行项目时，应验证新任务是否会显示在所得的新项目中。

### <a name="to-test-the-project"></a>测试项目

1. 按 **F5** 生成并运行项目。 Microsoft Project 启动并自动打开新的空白项目。

     生成项目时，代码会编译成一个程序集，此程序集包含在项目的生成输出文件夹中。 Visual Studio 还会创建一组注册表项，通过这些注册表项，Project 能够发现和加载 VSTO 外接程序，Visual Studio 还将开发计算机上的安全设置配置为允许 VSTO 外接程序运行。 有关详细信息，请参阅 [Office 解决方案生成过程概述](/previous-versions/visualstudio/visual-studio-2010/h2c9cdc0(v=vs.100))。

2. 验证新任务已添加到空白项目。

3. 验证以下文本是否出现在任务的 **“任务名称”** 字段中。

     **This text was added by using code.**

4. 关闭 Microsoft Project。

## <a name="clean-up-the-project"></a>清理项目
 完成项目开发后，请从开发计算机上删除 VSTO 外接程序程序集、注册表项和安全设置。 否则，每次在开发计算机上打开 Microsoft Project 时 VSTO 外接程序都会运行。

### <a name="to-clean-up-your-project"></a>清理项目

1. 在 Visual Studio 中，在 **“生成”** 菜单上，单击 **“清理解决方案”**。

## <a name="next-steps"></a>后续步骤
 既然你已经创建了一个基本的 Project VSTO 外接程序，就可以从下面这些主题中了解有关如何开发外 VSTO 外接程序的详细信息：

- 可在项目的 VSTO 外接程序中执行的常规编程任务： [PROGRAM VSTO 外](../vsto/programming-vsto-add-ins.md)接程序。

- 使用 Project 的对象模型： [项目解决方案](../vsto/project-solutions.md)。

- 生成和调试项目的 VSTO 外接程序： [生成 Office 解决方案](../vsto/building-office-solutions.md)。

- 部署 Project 的 VSTO 外接程序： [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>另请参阅
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [项目解决方案](../vsto/project-solutions.md)
- [构建 Office 解决方案](../vsto/building-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [Office 项目模板概述](../vsto/office-project-templates-overview.md)
