---
title: 演练：创建您的第一个 PowerPoint VSTO 外接程序
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- PowerPoint [Office development in Visual Studio], creating your first project
- add-ins [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9bba8095c1e79b8ab8addfd69afc1e89a50e3fce
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68871955"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-powerpoint"></a>演练：创建您的第一个 PowerPoint VSTO 外接程序
  本演练演示如何创建用于 Microsoft Office PowerPoint 的 VSTO 外接程序。 你在此类解决方案中创建的功能可用于应用程序本身，而与所打开的演示文稿无关。 有关详细信息, 请参阅[Office 解决方案开发&#40;概述&#41;VSTO](../vsto/office-solutions-development-overview-vsto.md)。

 [!INCLUDE[appliesto_pptallapp](../vsto/includes/appliesto-pptallapp-md.md)]

 本演练阐释了以下任务：

- 创建 PowerPoint 的 PowerPoint VSTO 外接程序。

- 编写使用 PowerPoint 对象模型来将文本框添加到每张新建幻灯片的代码。

- 生成并运行项目，以对其进行测试。

- 清理项目，使 VSTO 外接程序在开发计算机上不再自动运行。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- PowerPoint

## <a name="create-the-project"></a>创建项目

### <a name="to-create-a-new-project"></a>创建新项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。

3. 在模板窗格中，展开 **“Visual C#”** 或 **“Visual Basic”** ，然后展开 **“Office/SharePoint”** 。

4. 在展开的 **“Office/SharePoint”** 节点下方，选择 **“Office 外接程序”** 节点。

5. 在项目模板列表中，选择一个 PowerPoint VSTO 外接程序项目。

6. 在 "**名称**" 框中, 键入**FirstPowerPointAddIn**。

7. 单击 **“确定”** 。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]创建**FirstPowerPointAddIn**项目, 并在编辑器中打开**ThisAddIn**代码文件。

## <a name="write-code-that-adds-text-to-each-new-slide"></a>编写向每个新幻灯片添加文本的代码
 接下来，将代码添加到 ThisAddIn 代码文件。 新代码将使用 PowerPoint 对象模型来将文本框添加到每张新建幻灯片。 默认情况下，ThisAddIn 代码文件包含以下生成的代码：

- `ThisAddIn` 类的部分定义。 此类提供代码的入口点，并提供对 PowerPoint 对象模型的访问权限。 有关详细信息, 请参阅[PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。`ThisAddIn` 类的其余部分是在隐藏代码文件中定义的，不应修改该代码文件。

- `ThisAddIn_Startup` 和 `ThisAddIn_Shutdown` 事件处理程序。 PowerPoint 加载和卸载 VSTO 外接程序时会调用这些事件处理程序。 使用这些事件处理程序，可在加载 VSTO 外接程序对其进行初始化，并在卸载 VSTO 外接程序时清理其使用的资源。 有关详细信息, 请参阅[Office 项目中的事件](../vsto/events-in-office-projects.md)。

### <a name="to-add-a-text-box-to-each-new-slide"></a>若要将文本框添加到每张新建幻灯片中

1. 在 ThisAddIn 代码文件中，将下面的代码添加到 `ThisAddIn` 类中。 此代码为[应用程序](/previous-versions/office/developer/office-2010/ff764034(v=office.14))对象的[EApplication_Event. PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14))事件定义事件处理程序。

    当用户将新的幻灯片添加到活动演示文稿中时，此事件处理程序会将文本框添加到该新幻灯片的顶部，并添加文本到文本框中。

    [!code-vb[Trin_PowerPointAddInTutorial#1](../vsto/codesnippet/VisualBasic/Trin_PowerPointAddInTutorial/ThisAddIn.vb#1)]
    [!code-csharp[Trin_PowerPointAddInTutorial#1](../vsto/codesnippet/CSharp/Trin_PowerPointAddInTutorial/ThisAddIn.cs#1)]

2. 如果你使用的是 C#，请将以下代码添加到 `ThisAddIn_Startup` 事件处理程序中。 若要将`Application_PresentationNewSlide`事件处理程序与[EApplication_Event. PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14))事件连接, 此代码是必需的。

    [!code-csharp[Trin_PowerPointAddInTutorial#2](../vsto/codesnippet/CSharp/Trin_PowerPointAddInTutorial/ThisAddIn.cs#2)]

   若要修改每张新建幻灯片，之前的代码示例需使用以下对象：

- `Application` 类的 `ThisAddIn` 字段。 该`Application`字段返回一个[应用程序](/previous-versions/office/developer/office-2010/ff764034(v=office.14))对象, 该对象表示 PowerPoint 的当前实例。

- [EApplication_Event 事件](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14))的事件处理程序的参数。PresentationNewSlide事件的事件处理`Sld`程序。 `Sld`参数是一个表示新幻灯片的 [slide](/previous-versions/office/developer/office-2010/ff763417(v=office.14)) 对象。 有关详细信息, 请参阅[PowerPoint 解决方案](../vsto/powerpoint-solutions.md)。

## <a name="test-the-project"></a>测试项目
 当生成和运行项目时，请验证添加到演示文稿的新幻灯片中是否出现文本框。

### <a name="to-test-the-project"></a>测试项目

1. 按 **F5** 生成并运行项目。

     生成项目时，会将代码编译成一个程序集，此程序集放置在项目的生成输出文件夹中。 Visual Studio 还会创建一组注册表项，通过这些注册表项，PowerPoint 能够发现和加载 VSTO 外接程序，Visual Studio 还将开发计算机上的安全设置配置为允许 VSTO 外接程序运行。 有关详细信息, 请参阅[生成 Office 解决方案](../vsto/building-office-solutions.md)。

2. 在 PowerPoint 中，将新的幻灯片添加到活动演示文稿。

3. 验证下面的文本是否添加到幻灯片顶部的新建文本框中。

     **This text was added by using code.**

4. 关闭 PowerPoint。

## <a name="clean-up-the-project"></a>清理项目
 完成项目开发后，请从开发计算机上删除 VSTO 外接程序程序集、注册表项和安全设置。 否则，每次在开发计算机上打开 PowerPoint 时 VSTO 外接程序都会运行。

### <a name="to-clean-up-your-project"></a>清理项目

1. 在 Visual Studio 中，在 **“生成”** 菜单上，单击 **“清理解决方案”** 。

## <a name="next-steps"></a>后续步骤
 既然已经创建了一个基本的 PowerPoint VSTO 外接程序，就可以从下面这些主题中了解有关如何开发 VSTO 外接程序的详细信息：

- 可在 PowerPoint 的 VSTO 外接程序中执行的常规编程任务。 有关详细信息, 请参阅[PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

- 使用 PowerPoint 对象模型。 有关详细信息, 请参阅[PowerPoint 解决方案](../vsto/powerpoint-solutions.md)。

- 自定义 PowerPoint 的 UI，例如通过将自定义选项卡添加到功能区或创建你自己的自定义任务窗格。 有关详细信息, 请参阅[OFFICE UI 自定义](../vsto/office-ui-customization.md)。

- 生成和调试 PowerPoint VSTO 外接程序。 有关详细信息, 请参阅[生成 Office 解决方案](../vsto/building-office-solutions.md)。

- 部署 PowerPoint VSTO 外接程序。 有关详细信息, 请参阅[部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>请参阅
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [PowerPoint 解决方案](../vsto/powerpoint-solutions.md)
- [Office UI 自定义](../vsto/office-ui-customization.md)
- [构建 Office 解决方案](../vsto/building-office-solutions.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [Office 项目模板概述](../vsto/office-project-templates-overview.md)
