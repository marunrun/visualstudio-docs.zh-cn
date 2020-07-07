---
title: 演练：创建自定义站点工作流活动 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, custom workflow activities
- site workflows [SharePoint development in Visual Studio]
- workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, site workflows
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: dc7eef8b0924be745de436e06acc36785b1cb99b
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016528"
---
# <a name="walkthrough-create-a-custom-site-workflow-activity"></a>演练：创建自定义站点工作流活动
  本演练演示如何使用为站点级工作流创建自定义活动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 （站点级工作流适用于整个站点，而不只是网站上的列表。）自定义活动将创建备份公告列表，然后将 "公告" 列表中的内容复制到其中。

 本演练演示了下列任务：

- 创建站点级工作流。

- 创建自定义工作流活动。

- 创建和删除 SharePoint 列表。

- 将项从一个列表复制到另一个列表。

- 在快速启动栏上显示列表。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 和 SharePoint 版本。

- Visual Studio。

## <a name="create-a-site-workflow-custom-activity-project"></a>创建站点工作流自定义活动项目
 首先，创建一个用于保存和测试自定义工作流活动的项目。

#### <a name="to-create-a-site-workflow-custom-activity-project"></a>创建站点工作流自定义活动项目

1. 在菜单栏上，选择 "**文件**"  >  "**新建**  >  **项目**" 以显示 "**新建项目**" 对话框。

2. 展开 " **Visual c #** " 或 " **Visual Basic**" 下的 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

3. 在 "**模板**" 窗格中，选择 " **SharePoint 2010 项目**" 模板。

4. 在 "**名称**" 框中，输入**AnnouncementBackup**，然后选择 "**确定"** 按钮。

     " **SharePoint 自定义向导**" 随即出现。

5. 在 "**指定用于调试的站点和安全级别**" 页上，选择 "**部署为场解决方案**" 选项按钮，然后选择 "**完成**" 按钮以接受 "信任级别" 和 "默认站点"。

     此步骤将解决方案的信任级别设置为场解决方案，这是工作流项目的唯一可用选项。

6. 在**解决方案资源管理器**中，选择 "项目" 节点，然后在菜单栏上选择 "**项目**" "  >  **添加新项**"。

7. 在 " **Visual c #** " 或 " **Visual Basic**下，展开" **SharePoint** "节点，然后选择" **2010** "节点。

8. 在 "**模板**" 窗格中，选择 "**顺序工作流（仅场解决方案）** " 模板，然后选择 "**添加**" 按钮。

     " **SharePoint 自定义向导**" 随即出现。

9. 在 "**指定用于调试的工作流名称**" 页上，接受默认名称（AnnouncementBackup-workflow1.xaml）。 将工作流模板类型更改为 "**站点工作流**"，然后选择 "**下一步**" 按钮。

10. 选择 "**完成**" 按钮以接受剩余的默认设置。

## <a name="add-a-custom-workflow-activity-class"></a>添加自定义工作流活动类
 接下来，将一个类添加到项目中，以包含自定义工作流活动的代码。

#### <a name="to-add-a-custom-workflow-activity-class"></a>添加自定义工作流活动类

1. 在菜单栏上，选择**Project**  >  "项目" "**添加新项**" 以显示 "**添加新项**" 对话框。

2. 在 "**已安装的模板**" 树视图中，选择 "**代码**" 节点，然后选择项目项模板列表中的 "**类**" 模板。 使用默认名称 Class1。 选择“添加”按钮。

3. 将 Class1 中的所有代码替换为以下内容：

     [!code-csharp[SP_AnnBackup#1](../sharepoint/codesnippet/CSharp/announcementbackup/class1.cs#1)]
     [!code-vb[SP_AnnBackup#1](../sharepoint/codesnippet/VisualBasic/announcementbackupvb/class1.vb#1)]

4. 保存项目，然后在菜单栏上选择 "**生成**" "生成  >  **解决方案**"。

     Class1 显示为 " **AnnouncementBackup 组件**" 选项卡上的 "**工具箱**" 中的自定义操作。

## <a name="add-the-custom-activity-to-the-site-workflow"></a>将自定义活动添加到网站工作流
 接下来，将活动添加到工作流以包含自定义代码。

#### <a name="to-add-a-custom-activity-to-the-site-workflow"></a>向站点工作流中添加自定义活动

1. 在 "设计" 视图的工作流设计器中打开 Workflow1.xaml。

2. 从**工具箱**中拖动 Class1，使其显示在 `onWorkflowActivated1` 活动下，或打开 Class1 的快捷菜单，选择 "**复制**"，打开活动下的行的快捷菜单 `onWorkflowActivated1` ，然后选择 "**粘贴**"。

3. 保存项目。

## <a name="test-the-site-workflow-custom-activity"></a>测试网站工作流自定义活动
 接下来，运行该项目并启动站点工作流。 自定义活动将创建备份公告列表，并将当前 "公告" 列表中的内容复制到其中。 此代码还会检查是否已存在备份列表，然后再创建一个。 如果备份列表已存在，则将其删除。 此代码还会在 SharePoint 站点的快速启动栏上添加指向新列表的链接。

#### <a name="to-test-the-site-workflow-custom-activity"></a>测试网站工作流自定义活动

1. 选择**F5**键以运行项目并将其部署到 SharePoint。

2. 在快速启动栏上，选择 "**列表**" 链接以显示 SharePoint 站点中可用的所有列表。 请注意，名为 "**公告**" 的公告只有一个列表。

3. 在 SharePoint 网页的顶部，选择 "**站点工作流**" 链接。

4. 在 "启动新工作流" 部分下，选择 " **AnnouncementBackup-workflow1.xaml** " 链接。 这将启动站点工作流，并在自定义操作中运行代码。

5. 在快速启动栏上，选择 "**公告备份**" 链接。 请注意，"**公告**" 列表中包含的所有公告都已复制到此新列表中。

## <a name="see-also"></a>另请参阅
- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
