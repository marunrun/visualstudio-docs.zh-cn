---
title: 演练：部署项目任务列表定义 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7ea7063ce432841e812312b7c7c36721a7d2d099
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62784206"
---
# <a name="walkthrough-deploy-a-project-task-list-definition"></a>演练：部署项目任务列表定义

本演练演示如何使用 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] 创建、自定义、调试和部署 SharePoint 列表以跟踪项目任务。

[!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio 2017 或 Azure DevOps 服务。

## <a name="create-a-sharepoint-list"></a>创建 SharePoint 列表

创建 SharePoint 列表项目，并将该列表定义与任务相关联。

1. 打开**新的项目**对话框框中，展开**SharePoint**节点，然后选择**2010年**节点。

2. 在中**模板**窗格中，选择**SharePoint 2010 项目**模板中，将项目命名**命名为 ProjectTaskList**，然后选择**确定**按钮。

     **SharePoint 自定义向导**出现。

3. 指定用于调试的本地 SharePoint 站点选择**部署为场解决方案**选项按钮，然后选择**完成**按钮。

4. 打开项目的快捷菜单，然后选择**外** > **新项**。

5. 在中**模板**窗格中，选择**列表**模板，然后选择**添加**按钮。

     **SharePoint 自定义向导**出现。

6. 在中**想要列表的显示名称？** 框中，输入**项目任务列表**。

7. 选择**创建基于现有列表类型的不可自定义列表**选项按钮，，然后在其列表中，选择**任务**，然后选择**完成**按钮。

     列表、 功能和包显示在**解决方案资源管理器**。

## <a name="add-an-event-receiver"></a>添加事件接收器

在任务列表中，可以添加自动设置任务的截止日期和说明的事件接收器。 以下过程作为事件接收方将简单的事件处理程序添加到列表实例。

1. 打开项目节点的快捷菜单中，选择**外**，然后选择**新项**。

2. 在 SharePoint 模板列表中，选择**事件接收器**模板，并将其**ProjectTaskListEventReceiver**。

     **SharePoint 自定义向导**出现。

3. 上**选择事件接收器设置**页上，选择**列表项事件**作为中的事件接收器类型**哪种类型的事件接收器是否**列表。

4. 在中**哪个项应为事件源**列表中，选择**任务**。

5. 在要处理的事件列表中，选择复选框旁边**已添加项**，然后选择**完成**按钮。

     新的事件接收方节点具有名为的代码文件添加到项目**ProjectTaskListEventReceiver**。

6. 将代码添加到`ItemAdded`中的方法**ProjectTaskListEventReceiver**代码文件。 每次添加一个新任务，截止日期和说明默认值添加到任务。 默认截止日期为 2009 年 7 月 1 日。

     [!code-vb[SPProjectTaskList#1](../sharepoint/codesnippet/VisualBasic/projecttasklist1/projecttasklisteventreceiver/projecttasklisteventreceiver.vb#1)]
     [!code-csharp[SPProjectTaskList#1](../sharepoint/codesnippet/CSharp/projecttasklist/projecttasklisteventreceiver/projecttasklisteventreceiver.cs#1)]

## <a name="customize-the-project-task-list-feature"></a>自定义项目任务列表功能

创建 SharePoint 解决方案时，Visual Studio 自动创建默认的功能项目项。 可以使用功能设计器自定义 SharePoint 站点的项目任务列表设置。

1. 在中**解决方案资源管理器**，展开**功能**。

2. 打开快捷菜单**Feature1**，然后选择**视图设计器**。

3. 在中**标题**框中，输入**项目任务列表功能**。

4. 在中**作用域**列表中，选择**Web**。

5. 在中**属性**窗口中，输入**1.0.0.0**的值作为**版本**属性。

## <a name="customize-the-project-task-list-package"></a>自定义项目任务列表的包

创建 SharePoint 项目时，Visual Studio 会自动添加到包的默认项目项包含的功能。 可以使用包设计器自定义 SharePoint 站点的项目任务列表设置。

1. 在中**解决方案资源管理器**，打开快捷菜单**包**，然后选择**视图设计器**。

2. 在中**名称**框中，输入**ProjectTaskListPackage**。

3. 选择**重置 Web 服务器**复选框。

## <a name="build-and-test-the-project-task-list"></a>生成和测试项目任务列表

运行项目时，将打开 SharePoint 站点。 但是，您必须手动导航到任务列表的位置。

1. 选择**F5**键生成并部署项目任务列表。

     SharePoint 网站将打开。

2. 选择**主页**选项卡。

3. 在左侧栏中，选择**项目任务列表**链接。

     项目任务列表页面将显示。

4. 在中**列表工具**选项卡上，选择**项**选项卡。

5. 在中**项**组中，选择**新项**按钮。

6. 在中**标题**文字框中，输入**Task1**。

7. 选择**保存**按钮。

     刷新站点后， **Task1**截止日期为 2009 年 7 月 1 日将显示任务。

8. 选择**Task1**。

     将显示该任务的详细的视图，并显示说明"这是一项关键任务。"

## <a name="deploy-the-project-task-list"></a>部署项目任务列表

生成和测试项目任务列表后，您可以将其部署到*本地系统*或*远程系统*。 本地系统是在其开发解决方案，在同一台计算机，而远程系统是另一台计算机。

### <a name="to-deploy-the-project-task-list-to-the-local-system"></a>若要对本地系统部署项目任务列表

在 Visual Studio 菜单栏上依次选择**构建** > **部署解决方案**。

Visual Studio 回收 IIS 应用程序池，收回解决方案的任何现有版本，复制解决方案包 (*.wsp*) 到 SharePoint，文件，然后激活其功能。 现在可以在 SharePoint 中使用该解决方案。 有关部署配置步骤的详细信息，请参阅[如何：编辑 SharePoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)。

### <a name="to-deploy-the-project-task-list-to-a-remote-system"></a>若要部署到远程系统的项目任务列表

1. 在 Visual Studio 菜单栏上依次选择**构建** > **发布**。

2. 在中**发布**对话框框中，选择**发布到文件系统**选项按钮。

     你可以在目标位置**发布**对话框中，通过选择省略号按钮![省略号图标](../sharepoint/media/ellipsisicon.gif "省略号图标")，然后导航到另一个位置。

3. 选择**发布**按钮。

     一个 *.wsp*为解决方案创建的文件。

4. 复制 *.wsp*到远程 SharePoint 系统的文件。

5. 使用 PowerShell`Add-SPUserSolution`命令以安装远程 SharePoint 安装上的包。 (对于场解决方案，使用`Add-SPSolution`命令。)

     例如 `Add-SPUserSolution C:\MyProjects\ProjectTaskList\ProjectTaskList\bin\Debug\ProjectTaskList.wsp`。

6. 使用 PowerShell`Install-SPUserSolution`命令来部署解决方案。 (对于场解决方案，使用`Install-SPSolution`命令。)

     例如 `Install-SPUserSolution -Identity ProjectTaskList.wsp -Site http://NewSiteName`。

     有关远程部署的详细信息，请参阅[使用的解决方案](http://go.microsoft.com/fwlink/?LinkId=217680)并[添加和部署解决方案使用 SharePoint 2010 中的 PowerShell](http://go.microsoft.com/fwlink/?LinkId=217682)。

## <a name="next-steps"></a>后续步骤

您可以了解有关如何自定义和部署 SharePoint 解决方案中的以下主题的详细信息：

- [演练：创建 SharePoint 网站栏、 内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)

- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)

- [Windows PowerShell for SharePoint Server 2010](http://go.microsoft.com/fwlink/?LinkId=217684)

## <a name="see-also"></a>请参阅
[打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
