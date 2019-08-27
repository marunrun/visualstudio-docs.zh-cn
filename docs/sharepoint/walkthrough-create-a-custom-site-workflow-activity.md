---
title: 演练：创建自定义站点工作流活动 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: f717345689de9be640e03e9c7d81726a57d494b0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63008277"
---
# <a name="walkthrough-create-a-custom-site-workflow-activity"></a>演练：创建自定义站点工作流活动
  本演练演示如何创建自定义活动的站点级工作流使用[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 （站点级工作流应用于整个站点，而不仅仅是在站点上的列表。）自定义活动创建的备份通知列表，然后将公告列表的内容复制到其中。

 本演练演示了下列任务：

- 创建站点级工作流。

- 创建自定义工作流活动。

- 创建和删除 SharePoint 列表。

- 将项从一个列表复制到另一个。

- 在快速启动栏上显示列表。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- 支持的版本[!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)]和 SharePoint。

- Visual Studio。

## <a name="create-a-site-workflow-custom-activity-project"></a>创建站点工作流自定义活动项目
 首先，创建一个项目以保存并测试自定义工作流活动。

#### <a name="to-create-a-site-workflow-custom-activity-project"></a>若要创建站点工作流自定义活动项目

1. 在菜单栏上依次选择**文件** > **新建** > **项目**显示**新建项目**对话框。

2. 展开**SharePoint**节点下的**Visual C#** 或**Visual Basic**，然后选择**2010年**节点。

3. 在中**模板**窗格中，选择**SharePoint 2010 项目**模板。

4. 在中**名称**框中，输入**AnnouncementBackup**，然后选择**确定**按钮。

     **SharePoint 自定义向导**出现。

5. 上**指定用于调试的网站和安全级别**页上，选择**部署为场解决方案**选项按钮，然后选择**完成**按钮以接受信任级别和默认站点。

     此步骤会将该解决方案的信任级别设置为场解决方案，工作流项目的唯一可用的选项。

6. 在中**解决方案资源管理器**，选择项目节点，然后，在菜单栏上选择**项目** > **添加新项**。

7. 下**Visual C#** 或**Visual Basic**，展开**SharePoint**节点，然后选择**2010年**节点。

8. 在中**模板**窗格中，选择**顺序工作流 （仅场解决方案）** 模板，然后选择**添加**按钮。

     **SharePoint 自定义向导**出现。

9. 上**指定用于调试的工作流名称**页上，接受默认名称 (AnnouncementBackup-Workflow1)。 将工作流模板类型更改为**站点工作流**，然后选择**下一步**按钮。

10. 选择**完成**按钮以接受其余默认设置。

## <a name="add-a-custom-workflow-activity-class"></a>添加自定义工作流活动类
 接下来，将一个类添加到项目，以包含自定义工作流活动的代码。

#### <a name="to-add-a-custom-workflow-activity-class"></a>若要添加自定义工作流活动类

1. 在菜单栏上依次选择**项目** > **添加新项**以显示**添加新项**对话框。

2. 在中**已安装的模板**树视图中，选择**代码**节点，然后选择**类**项目项模板列表中的模板。 使用默认名称 Class1。 选择 **“添加”** 按钮。

3. 使用以下内容替换所有 Class1 中的代码：

     [!code-csharp[SP_AnnBackup#1](../sharepoint/codesnippet/CSharp/announcementbackup/class1.cs#1)]
     [!code-vb[SP_AnnBackup#1](../sharepoint/codesnippet/VisualBasic/announcementbackupvb/class1.vb#1)]

4. 保存该项目，，然后在菜单栏上选择**构建** > **生成解决方案**。

     Class1 将显示为中的自定义操作**工具箱**上**AnnouncementBackup 组件**选项卡。

## <a name="add-the-custom-activity-to-the-site-workflow"></a>将自定义活动添加到站点工作流
 接下来，将活动添加到工作流以包含自定义代码。

#### <a name="to-add-a-custom-activity-to-the-site-workflow"></a>若要将自定义活动添加到站点工作流

1. 在设计视图中的工作流设计器中打开 Workflow1。

2. 将从 Class1**工具箱**，以便它将显示在`onWorkflowActivated1`活动或为 Class1，打开快捷菜单，请选择**复制**，打开下方的行的快捷菜单`onWorkflowActivated1`活动，然后选择**粘贴**。

3. 保存项目。

## <a name="test-the-site-workflow-custom-activity"></a>测试站点工作流自定义活动
 接下来，运行该项目并启动站点工作流。 自定义活动创建一个备份的公告列表，并从当前的公告列表的内容复制到它。 该代码还检查备份列表是否已存在之前创建一个。 如果已存在一个备份列表，它删除。 该代码还将链接添加到 SharePoint 站点的快速启动栏上的新列表。

#### <a name="to-test-the-site-workflow-custom-activity"></a>若要测试站点工作流自定义活动

1. 选择**F5**键以运行该项目并将其部署到 SharePoint。

2. 在快速启动栏上依次选择**列出了**链接以显示所有 SharePoint 站点中提供的列表。 请注意，只有一个名为的公告列表**公告**。

3. 在 SharePoint 网页的顶部，选择**网站工作流**链接。

4. 在开始新工作流部分时，请选择**AnnouncementBackup-Workflow1**链接。 这将启动站点工作流并运行自定义操作中的代码。

5. 在快速启动栏上依次选择**公告备份**链接。 请注意，所有中包含的公告**公告**列表已复制到此新列表。

## <a name="see-also"></a>请参阅
- [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
